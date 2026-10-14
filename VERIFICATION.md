# Verification results

## Passed

- 53 unit, SQLite integration, and API tests passed.
- A separate live HTTP smoke check passed against Uvicorn: HTML/static file
  delivery and create, read, update, delete through actual network requests.
- Offline browser checks passed for list rendering and create-form setup.
  Desktop and mobile layouts were rendered and visually inspected. Those checks
  used sample data, not a live browser-to-server connection.
- JavaScript syntax validation and Python compilation passed.
- All five E2E tests were collected successfully.

Reproduce the verified backend test suite:

```bash
python -m pytest tests/unit tests/integration tests/api -q
```

## Not verified

The five E2E tests were attempted, but the build environment's managed Chromium
browser blocked URL navigation with `net::ERR_BLOCKED_BY_ADMINISTRATOR` before
any application interaction. These are not reported as passing E2E tests.
No browser policy was changed. Run the included E2E tests locally using the
commands in README.md.

Dependency verification used the installed packages in the build environment;
a fresh package installation could not be checked because its package-index
network access was unavailable. Direct dependencies are pinned to the versions
used for the checks.

## Environment used

| Component | Version |
| --- | --- |
| Python | 3.13.5 |
| SQLite | 3.46.1 |
| FastAPI | 0.128.2 |
| Uvicorn | 0.48.0 |
| Pydantic | 2.13.5 |
| pytest | 9.0.2 |
| HTTPX | 0.28.1 |
| Playwright | 1.57.0 |

The application is intended for Python 3.11 or newer. Other Python versions and
operating systems were not exercised in this build environment.
