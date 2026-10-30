# ERP Procure-to-Pay Lab

Receive a purchase order in partial deliveries, inspect stock movements and reconcile an invoice against price and receipt evidence.

**Español:** Compras e inventarios: recepción parcial, control de duplicados y conciliación de orden, recepción y factura.

[Live demonstration](https://krissortegal83.github.io/erp-process-lab/) · [All projects](https://krissortegal83.github.io/)

## Business case

Purchase orders, warehouse receipts and supplier invoices often disagree. Paying before reconciling quantities and prices creates avoidable operational risk.

## Design decision

Use unique receipt references, block over-receipts and hold invoices when the received quantity or agreed unit price does not support them.

## Guided demonstration

1. Receive 6 units with reference GRN-001. Try the same reference again.
2. Evaluate the 10-unit invoice: it is held because only 6 units arrived.
3. Receive 4 units using GRN-002. Evaluate again: the invoice matches.

## Acceptance criteria

- Stock changes once per unique receipt.
- Over-receipts and fractional units are blocked.
- Quantity and price discrepancies produce explicit hold reasons.

## Implementation

`index.html` → shared `assets/lab-ui.mjs` → pure functions in `assets/business-rules.mjs` → in-memory state and downloadable JSON/Markdown. Business rules are tested with Node’s built-in test runner. No installation, vendor account, backend or paid service is required for the deployed demo.

## Scope and production considerations

One SKU and one PO, whole units, MXN, tax excluded, exact price matching. Independent functional model; no Epicor, Dynamics 365, accounting posting or payment connection.

A production pilot requires authenticated users, appropriate permissions, durable storage, integration contract testing, monitoring, data governance, operational ownership and acceptance. Metrics are scenario outputs, not historical client results.

## Validation

Run `npm test` from the repository root. Run `python -m http.server 8000`, then open this folder in the browser to test the scenario and exports. See [catalog quality evidence](https://github.com/krissortegal83/enterprise-solutions-lab/blob/main/docs/QUALITY.md).

## Authorship and provenance

Independent project created for Christian Ortega Lugo’s portfolio using AI-assisted implementation. Fictional organizations and records only. It is not an employer deliverable, endorsement, vendor certification or claim of deployed client outcomes. The professional owner should review and be prepared to explain the design and limitations.

## Run independently

Use Python 3 to serve the demo and Node.js 22+ to run its tests. No package installation is required.

```bash
python -m http.server 8000
# Open http://localhost:8000
npm run check
npm test
```

## Repository layout

- `index.html`: interactive demo.
- `assets/`: presentation and business rules.
- `tests/`: scenarios and failure cases.
- `docs/ORIGEN.md`: provenance and maintenance.
- `.github/workflows/`: automated checks and deployment.

## En español

Compras e inventarios: comprueba que lo pedido, recibido y facturado coincide. Puedes probar la demo sin registro. Los controles y la documentación técnica están en inglés para facilitar la colaboración internacional.
