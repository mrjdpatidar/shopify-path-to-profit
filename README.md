# Path‑To‑Profit – Shopify Analytics & Advertising Dashboard

## Overview

**Path‑To‑Profit** is a custom Shopify application that aggregates data from three major advertising and analytics platforms—**Shopify analytics**, **Google Ads**, and **Meta (Facebook) Ads**—and presents the combined insights on a unified, interactive dashboard.

### What the app does

- **Shopify Data Collection**
  - Retrieves orders, products, customers and traffic‑source information directly from the Shopify store via the Shopify REST API.
  - Stores the raw data in a local MySQL database for fast querying.

- **Google Ads Integration**
  - Connects to a Google Ads account (OAuth flow) and pulls campaign spend, impressions, clicks and conversion metrics.
  - Normalises the data so that spend can be compared against Shopify revenue.

- **Meta (Facebook) Ads Integration**
  - Authenticates with the Meta Marketing API, fetches ad‑set spend, impressions and results.
  - Aligns Meta ad performance with the same time‑frames used for Shopify orders.

- **Unified Dashboard**
  - Combines the three data sources into a single view where store owners can:
    - See total revenue vs. advertising spend (Google + Meta).
    - Compare cost‑per‑acquisition (CPA) across platforms.
    - Track the performance of individual channels (organic, paid‑search, paid‑social).
    - Visualise trends over selectable date ranges (last 7 days, month‑to‑date, custom).
  - Provides drill‑down tables for **Orders**, **Products**, **Customers**, **Google Campaigns**, **Meta Campaigns**, and **Traffic Sources**.
  - Offers export functionality (CSV/Excel) for offline analysis.

### Key Features

1. **Real‑time Sync** – Background jobs (`SyncShopifyOrdersJob`, `SyncShopifyProductsJob`, `SyncShopifyCustomersJob`, `GoogleSyncService`, `MetaSyncService`) run on demand or on a configurable interval (`SYNC_INTERVAL`).
2. **Secure JWT Authentication** – The backend issues short‑lived JWTs after a successful Shopify App Bridge session, allowing the frontend to call the API securely.
3. **Scalable Architecture** – Laravel handles the API/queue layer, while the Next.js frontend provides a fast, responsive SPA.
4. **Extensible Data Model** – New ad‑platforms or custom metrics can be added by extending the existing service classes and updating the dashboard components.
5. **Role‑Based Access** – Admin users can view all stores; store‑specific users only see data for their own shop.

## How It Works (Technical Flow)

```mermaid
flowchart TD
    subgraph Shopify
        A[Shop Owner installs app] --> B[OAuth flow → obtain access token]
        B --> C[App Bridge session token]
        C --> D[Frontend sends token to backend]
    end
    D --> E[Backend validates token → issues JWT]
    E --> F[Frontend stores JWT]
    F --> G[API calls]
    G --> H[Laravel Controllers]
    H --> I[Services (ShopifySync, GoogleSync, MetaSync)]
    I --> J[Database (MySQL)]
    J --> K[Dashboard UI (Next.js)]
    K --> L[Visual charts & tables]
```

## Credits & Contact

**Company:** Drunall Technologies

**Portfolio contact:** Jagdish Patidar — Founder & CEO

- [Drunall Technologies](https://www.drunall.com/)
- [Jagdish Patidar — Portfolio](https://jdpatidar.com/)
- [LinkedIn](https://www.linkedin.com/in/jdpatidar/)

For workforce management, attendance integration, payroll, or custom business software requirements, connect through the links above.

