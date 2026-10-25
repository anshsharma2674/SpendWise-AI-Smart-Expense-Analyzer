# Testing record

This record distinguishes checks actually run from manual scenarios that still require a browser. No feature is marked passed solely because it is implemented.

## Automated / static checks

| Check | Result |
|---|---|
| JavaScript syntax parse (`node --check` on the application script) | Passed |
| HTML parsed with Python `HTMLParser`; duplicate IDs checked; required files present | Passed |

## Feature verification checklist

The following interactions require execution in a browser and have not yet been manually verified:

| Test case | Result |
|---|---|
| Add transaction and verify totals | Not run |
| Edit transaction and verify affected displays | Not run |
| Delete transaction with confirmation | Not run |
| CSV header/row validation and quoted commas | Not run |
| CSV preview, duplicate handling, cancel, and confirmed import | Not run |
| CSV transaction export and report export | Not run |
| Dashboard calculations and zero-income savings rate | Not run |
| Budget statuses below 80%, at/above 80%, and above 100% | Not run |
| Savings goal progress and optional date estimate | Not run |
| Month filtering and missing prior-month comparison | Not run |
| Currency formatting and no-conversion behavior | Not run |
| Dark Mode, Light Mode, and System Default | Not run |
| OS theme change while System Default is selected | Not run |
| Theme persistence after refresh | Not run |
| Statistical insight explanations and anomaly sparse-data handling | Not run |
| Forecast with insufficient and sufficient history | Not run |
| Delete all app data | Not run |
| Demo mode replacement confirmation and calculations | Not run |
| Responsive layouts at mobile, tablet, and desktop widths | Not run |
| Invalid form inputs and long descriptions | Not run |
| Browser storage unavailable/full error behavior | Not run |
| Chart CDN unavailable fallback | Not run |

## Manual browser procedure

Open `index.html`, load fictional demo data, then work through the checklist above. Inspect all views in each appearance mode and at narrow mobile width. Verify browser storage errors by disabling storage or filling it only in a disposable test profile. Do not use actual sensitive financial records for screenshots or tests.
