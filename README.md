# Inventory Hub

SAP-integrated inventory management dashboard for tracking stock levels, planning reorders, and monitoring material movements.

![SAP](https://img.shields.io/badge/SAP-OData%20Integration-0070F2?logo=sap&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

**[Live Demo](https://opticalowners.github.io/inventory-hub/)**

## Overview

Inventory Hub is a self-contained single-file HTML application designed to connect with SAP ERP systems via OData APIs. It provides real-time visibility into inventory levels, automated reorder planning, demand forecasting, and ABC analysis — all within a unified dashboard.

## Features

- **Dashboard** — KPIs at a glance: total inventory value, critical/low stock alerts, turnover rates, incoming POs, and recent material movements.
- **Inventory Browser** — Full material master with search, multi-filter (category, status, plant), sortable columns, stock-level visualizations with safety/reorder thresholds, and detailed material drill-down.
- **Reorder Planning** — Auto-calculated suggested order quantities, estimated costs, lead time tracking, and one-click SAP Purchase Requisition generation.
- **Demand Forecast** — 30-day projected usage vs. current stock with depletion warnings.
- **ABC Analysis** — Value-based inventory classification to prioritize management effort.
- **Material Movements** — Document log mirroring SAP movement types (101, 261, 311, 562).
- **SAP Configuration** — Connection settings, OData endpoint management, and sync scheduling.

## SAP Integration Points

| SAP Service | OData Endpoint | Data |
|---|---|---|
| Material Master | `API_MATERIAL_STOCK_SRV` | Material attributes, groups, UoM |
| Stock Overview | `API_MATERIAL_STOCK_SRV` | On-hand, available, reserved, in-transit |
| Purchase Orders | `API_PURCHASEORDER_PROCESS_SRV` | Open POs, delivery dates, statuses |
| Material Documents | `API_MATERIAL_DOCUMENT_SRV` | Goods receipts, issues, transfers |
| MRP Results | `API_MRP_RESULTS_SRV` | Planned orders, requirements |
| Production Orders | `API_PRODUCTION_ORDERS_SRV` | Production scheduling |

## Getting Started

No build step or dependencies required. Just open the file:

1. Clone this repo
2. Open `inventory-hub.html` in any modern browser

```bash
git clone https://github.com/opticalowners/inventory-hub.git
cd inventory-hub
open inventory-hub.html
```

The application currently uses simulated data that mirrors real SAP material master structures (material groups, MRP types, storage locations, plants). Click **Sync from SAP** to regenerate sample data.

## Connecting to a Live SAP Instance

1. Navigate to the **SAP Config** tab
2. Enter your SAP host URL, client number, and credentials
3. The OData service endpoints are pre-configured for standard SAP APIs
4. Adjust sync schedules to match your requirements

To implement live data, replace the simulated data functions with actual OData API calls:

```javascript
// Example: Fetching materials from SAP
const fetchMaterials = async () => {
  const response = await fetch(
    `${SAP_HOST}/sap/opu/odata/sap/API_MATERIAL_STOCK_SRV/A_MaterialStock`,
    {
      headers: {
        'Authorization': `Basic ${btoa(`${username}:${password}`)}`,
        'Accept': 'application/json',
      },
    }
  );
  const data = await response.json();
  return data.d.results;
};
```

## Roadmap

- [ ] Live SAP OData API integration
- [ ] Role-based access control
- [ ] Export reports to Excel/PDF
- [ ] Email/Slack alerts for critical stock levels
- [ ] Batch processing for purchase requisitions
- [ ] Historical trend analysis and charts
- [ ] Multi-plant consolidated views

## License

MIT
