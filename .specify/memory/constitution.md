# Project Standards

## Code Quality

All business logic must be in service-layer functions, not in route handlers. No commented-out code. Type annotations on all public functions.

## Testing Requirements

**Minimal** — no automated tests required

Integration tests must cover every public API endpoint. Mocks only for external services.

## Error Handling

API responses must be validated at the boundary using schema validation. All 4xx/5xx responses must include a machine-readable error code in the response body. Exceptions logged with full context.

## Performance Constraints

No performance constraints for this project.

## UX Consistency

N/A — this is a backend service with no user-facing UI.