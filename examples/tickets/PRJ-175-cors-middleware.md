---
id: PRJ-175
title: Add CORS middleware to the adapter so a browser client can reach it
status: done
tier: standard
phase: 8
complexity: S
dependencies: []
claimed_by: engine-maintainer
claimed_at: 2026-08-21
blocked_at:
closed_at: 2026-08-21
---

# PRJ-175 — Add CORS middleware to the adapter so a browser client can reach it

## Context

`client/to-engine/008` reports that `runtime/api.py` sends no
`Access-Control-*` headers, so no browser can call it: a preflight
`OPTIONS /games` returns `405`, and a real `POST /games` succeeds with no
CORS headers, which the browser then discards. Neither test suite catches
this because both drive the adapter through clients that never enforce
same-origin policy (FastAPI `TestClient`, node `fetch`). ADR-0018 decides the
policy: wildcard origins, no credentials, HTTP only. This ticket carries the
implementation.

## Specification

### Files

- `runtime/api.py` — add `fastapi.middleware.cors.CORSMiddleware` to
  `create_app()`.
- `tests/integration/test_api.py` — add a preflight-`OPTIONS` test.

### Public surface

No new public functions or types. `create_app()`'s returned `FastAPI`
instance gains CORS middleware; its signature is unchanged.

```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["GET", "POST", "OPTIONS"],
    allow_headers=["content-type"],
)
```

### Behaviour

- Every HTTP response from the adapter carries
  `Access-Control-Allow-Origin: *`.
- `OPTIONS` requests carrying `Access-Control-Request-Method` against any
  existing route return a 2xx (not `405`) with `Access-Control-Allow-Origin`
  and `Access-Control-Allow-Methods` present.
- `allow_credentials` stays at its default (`False`) — do not set it,
  per ADR-0018 (wildcard + credentials is not legal CORS).
- The WebSocket route (`/ws`) is untouched. `CORSMiddleware` does not govern
  it; no change in behaviour is expected or required there.

## Acceptance criteria

1. AC1: A preflight `OPTIONS /games` request with
   `Access-Control-Request-Method: POST` and an `Origin` header returns a 2xx
   response carrying `Access-Control-Allow-Origin: *` (or an origin-echoing
   equivalent) and `Access-Control-Allow-Methods` including `POST`.
2. AC2: A real `POST /games` request carrying an `Origin` header returns its
   normal `201` body *and* an `Access-Control-Allow-Origin` header.
3. AC3: Every existing `tests/integration/test_api.py` assertion continues to
   pass unmodified — CORS headers are additive, not a behaviour change to any
   existing response.
4. AC4: `allow_credentials` is not set to `True` anywhere in `create_app()`.

## Out of scope

- Narrowing origins to an explicit allowlist (ADR-0018 Alternative 1 —
  rejected for now).
- Any change to the WebSocket route's origin handling (ADR-0018
  Alternative 3 — rejected for now, revisit only if the HTTP policy ever
  narrows past wildcard).
- Auth, credentialed requests, or any session/cookie concern — none exist on
  this adapter today (ADR-0011 non-goals).
- Reversing or replacing the client's Vite dev-server proxy — that is the
  client's own choice to keep or drop once this ships.

## References

- ADR-0018 (the CORS policy decision this ticket implements)
- ADR-0011 (Phase 8 scope — the adapter's non-goals; CORS is not among them)
- ADR-0016 point 4 (every endpoint is ungated, and that is a decision)
- `client/to-engine/008`, `client/to-client/010`

## Notes

The test-suite gap the report calls out — that `TestClient` and node
`fetch` are both structurally incapable of noticing a missing CORS header —
is exactly why AC1 needs a real preflight assertion rather than a passing
existing test. FastAPI's `TestClient` still allows asserting response
headers on an `OPTIONS` request the same way as any other request; no browser
is needed for the test.

## PR Description

**Ticket:** PRJ-175
**Tier:** standard

### Summary

`client/to-engine/008` found that `runtime/api.py` sends no
`Access-Control-*` headers, so no browser client can reach the adapter — a
preflight `OPTIONS /games` came back `405`, and a real `POST /games`
succeeded with no CORS headers, which a browser then discards. Neither
existing test suite could catch it, since FastAPI's `TestClient` and node's
`fetch` both skip same-origin enforcement. ADR-0018 decided the policy —
wildcard origins, no credentials, HTTP only — and this ticket implements it:
`CORSMiddleware` added to `create_app()`, plus two new integration tests
that issue a real preflight and a real request and assert the header is
present on both.

### Acceptance criteria

1. AC1 — met. `test_preflight_options_carries_cors_headers` sends a real
   `OPTIONS /games` with `Access-Control-Request-Method: POST` and an
   `Origin` header; asserts a 2xx response with
   `Access-Control-Allow-Origin: *` and `POST` in
   `Access-Control-Allow-Methods`.
2. AC2 — met. `test_real_request_also_carries_the_cors_header` sends a real
   `POST /games` with an `Origin` header; asserts the normal `201` body and
   `Access-Control-Allow-Origin: *` on the response.
3. AC3 — met. Full `tests/integration/test_api.py` run: 53 passed, 0
   failed — every pre-existing assertion unchanged.
4. AC4 — met. `allow_credentials` is not set anywhere in `create_app()`
   (verified by inspection of the diff; only `allow_origins`,
   `allow_methods`, `allow_headers` are passed).

### Out of scope

Everything the ticket's Out of scope section listed was left alone: no
origin allowlist, no WebSocket origin check, no auth/credentials work, no
change to the client's Vite proxy (that remains the client's own call).

### How to verify

```
git checkout PRJ-175-cors-middleware
pytest tests/integration/test_api.py -q
ruff check . && ruff format --check . && mypy --strict core content ai runtime
pytest --cov --cov-report=term-missing -q
```

All four gates pass on this branch: 53/53 integration tests, ruff clean,
mypy strict clean on 130 source files, full suite 4763 passed with 99%
overall coverage (unchanged from the pre-change baseline; the one uncovered
line in `runtime/api.py` — 669, the WebSocket disconnect `finally` cleanup
— predates this change and is untouched by it).

### Risks / follow-ups

- The HTTP/WebSocket CORS asymmetry (HTTP now states a policy, `/ws` states
  none) is documented in ADR-0018 and the module docstring but not closed.
  Not a regression — the WebSocket already connected regardless of origin
  before this ticket — but worth a follow-up if the HTTP policy ever
  narrows past wildcard.
- Wildcard origins mean any page on any origin can drive any game whose id
  it knows. Not a new exposure (ADR-0016 already made every endpoint
  ungated), but worth re-examining together with CORS the day the adapter
  gains real auth, since wildcard + credentials would stop being legal at
  that point.
