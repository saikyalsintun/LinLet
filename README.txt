# Money Transfer Fee Calculator

## Files
- `index.html`: mobile-friendly website interface
- `Code.gs`: Google Apps Script backend and Google Sheets logging

## Google Sheet setup
Spreadsheet ID is already set in `Code.gs`.
Create these tabs with exact names:
1. `cost_detail` — headers: `phone number | cost | Status | Date`
2. `total` — can be empty; the script generates the monthly summary.

## Install
1. Open the linked Google Spreadsheet.
2. Choose Extensions → Apps Script.
3. Create an HTML file named `index` and paste `index.html`.
4. Paste `Code.gs` into the Apps Script editor.
5. Save.
6. In Apps Script, select `doGet` and deploy as a Web app (Execute as: Me; access setting appropriate for your intended users).
7. Authorize the script when prompted.
8. Open the newly deployed Web App URL on your phone. If you update code later, deploy a new version of the web app.

The previously supplied `/exec` URL may belong to an earlier deployment. The new deployment URL is the one to use after adding this code.

## Current fee assumptions (please verify)
- Cash Out: amount up to 20,000 costs 100; 20,001–30,000 costs 200; 30,001–50,000 costs 300; 50,001–100,000 costs 500.
- Cash Out above 100,000: rate is 500 per 100,000 until below 3,000,000; 450 per 100,000 from 3,000,000 to below 5,000,000; 400 per 100,000 at 5,000,000 and above. Formula fees are the multiplier is first rounded to 2 decimal places, then the resulting fee is rounded UP to the next 100. Thus 450,000 gives 2,300.
- Cash In: fee is 100 per started 100,000 (e.g. 100,000=100; 100,001=200; 200,000=200).
- The phrase about 8,000–9,000 was interpreted as the usual 100 fee, not as charging the full transfer amount.

## Notes
- Monthly totals are rebuilt from `cost_detail` on every save. `total` shows month, cash-in fees, cash-out fees, combined fees, and transaction count.
- The script stores the Date as a real spreadsheet date so month grouping works.
- Restrict web-app access appropriately because the app writes to your financial transaction sheet.
