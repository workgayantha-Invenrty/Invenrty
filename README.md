# Weekly WIP Inventory (HTML tool)

Single file: `index.html`. No server, no AI, no internet needed to calculate (internet only for the optional Firebase history).

## Every week
1. Open `index.html` (double-click, or your GitHub Pages link).
2. **Load files**: drop the new *Production Status* file (+ the *Trims Issuing Report*, optional - information only).
   The BOM template is stored in the browser - drop it again only when a new style is added / a BOM changes.
3. **Open POs**: auto-selected (Remark empty, qty > 0, something cut, not fully shipped). New POs appear, shipped ones drop out. Tick / untick to override.
4. **Results** -> *Download Excel* and *Save to history*.

Same files always give the same numbers (no AI involved).

## Rules used
- WIP = Cut - Finishing, FG = Finishing - Shipped (open POs only)
- Stages are corrected so they never go backwards
- Value = standard cost per pair (PRD YY x Unit Cost Ex Work) by stage reached: Cutting / + Upper closing / + Lasting & Desma / + Finishes for FG. Packing excluded.
- Trims issued = information only (actual cost column, "Trims Not In BOM" sheet)
- Styles without a BOM -> "cost sheet missing", not valued. Add the style to the BOM template, drop it, the PO is costed.

## BOM template columns (any sheet, any order)
Style (or PO), Section (1 Cutting / 2 Upper closing / 3 Lasting & Desma / 4 Finishes / 5 Packing), Component, S-No, Description, UOM, PRD YY, Unit Cost USD (Ex Work), Loss % (optional).
If a PO column is present each PO keeps its own BOM; otherwise the style BOM is used.

## History
Saved per report date: totals + PO-wise rows. Nothing is ever deleted automatically - a PO that leaves the report stays in the **PO register** marked CLOSED.
History tab: saved weeks, trend chart, compare two weeks (new / closed POs, value change), export / import JSON.

## Cloud history with Firebase (optional)
1. console.firebase.google.com -> Add project (Spark plan is free).
2. Authentication -> Email/Password -> enable, add your user.
3. Firestore Database -> Create -> Rules -> paste `firestore.rules` -> Publish.
4. Project settings -> Web app -> copy `firebaseConfig` -> paste in the tool: *Cloud / Settings*.
5. Sign in, press *Sync now*. After that every "Save to history" is also uploaded.
6. GitHub Pages: Authentication -> Settings -> Authorized domains -> add `yourname.github.io`.

## GitHub Pages
Create a repo -> *Add files via upload*: `index.html`, `firestore.rules`, `README.md` -> Settings -> Pages -> Deploy from branch `main` / root.
Don't put real data in a public repo: the data lives in your browser / Firebase, not in the files.
