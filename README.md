# Sales Analytics Workspace

A Microsoft Fabric workspace that generates mock sales data, builds a lakehouse and semantic model, and delivers a Power BI sales dashboard.

## Workspace Items

| Item | Type | Purpose |
|------|------|---------|
| **Notebook_MockData** | Notebook | Populates mock Delta tables in SalesLakehouse (ProductCategory, Product, Customer, SalesOrderHeader, SalesOrderDetail) |
| **SalesLakehouse** | Lakehouse | Delta Lake storage for all sales tables |
| **SalesModel** | Semantic Model | DirectLake semantic model with 4 relationships across 5 tables |
| **Notebook_Sales** | Notebook | Interactive Spark SQL analytics: top customers, monthly trend, category revenue, best sellers, territory breakdown, customer segmentation |
| **Notebook_SampleQueries** | Notebook | Analytical sample queries: revenue by category, monthly trends, top customers, best sellers, territory analysis, customer segmentation, YoY comparison |
| **SalesReport** | Power BI Report | Sales Dashboard with Revenue by Category, Monthly Sales Trend, and Revenue by Territory visuals |
| **SalesSQL** | SQL Database | Fabric SQL database with AdventureWorks SalesLT schema (Customer, Product, SalesOrderHeader, SalesOrderDetail, Address tables) |

## Data Model

```
ProductCategory ←── Product ←── SalesOrderDetail ──→ SalesOrderHeader ──→ Customer
```

### Tables
- **ProductCategory** – 4 categories (Bikes, Components, Clothing, Accessories)
- **Product** – 15 products with cost and pricing
- **Customer** – 15 customers across US cities
- **SalesOrderHeader** – 30 orders spanning 2024–2025 with territory and totals
- **SalesOrderDetail** – 63 line items with quantity, unit price, and line total

## Deployment

Artifacts are deployed via `fabric-cicd`. Environment-specific IDs are parameterised in `config/parameter.yml`.

```
DEV  workspace: 334687d9-c5a3-4af6-a9b1-9c02bad79934
QA   workspace: 9b6c012c-1c20-4807-9feb-a7703a7671bd
PROD workspace: 7d836180-43af-494d-80e9-de50ed5f8529
```

## Usage

1. Deploy the workspace using `deploy.ps1`
2. Run **Notebook_MockData** to seed all Delta tables in SalesLakehouse
3. Refresh **SalesModel** to pick up the new data
4. Open **SalesReport** to explore the Sales Dashboard
5. Run **Notebook_Sales** or **Notebook_SampleQueries** for ad-hoc analytical queries
6. Connect to **SalesSQL** for SQL-based querying via the Fabric SQL endpoint
