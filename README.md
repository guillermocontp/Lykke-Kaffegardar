# Lykke-Kaffegårdar
Lykke Kaffegårdar technical data pipeline demonstration


## 1. Executive Summary
Lykke Kaffegårdar is Sweden’s fastest-growing sustainable coffee project, now expanding across multiple European markets. As the company prepares to scale its e-commerce from ~2M SEK annually to a tenfold increase, it faces a key challenge: ensuring consistent, reliable data insights across partners and markets. Fragmented reporting and limited visibility into customer behavior, product performance, and partner operations currently hinder decision-making and revenue growth.

This report outlines how Lykke can address these challenges by adopting a lightweight but scalable analytics approach. Instead of investing in a full-scale data warehouse at this stage, we recommend beginning with a Business Intelligence (BI) solution such as Power BI. This allows Lykke to connect existing systems (Shopify, Fortnox, GA4, PSPs, and logistics platforms), define and track core KPIs, and build clear, actionable dashboards for decision-makers.

Our proposed approach balances immediate needs—simple, reliable insights to guide growth—with long-term scalability. By establishing unified KPI tracking, identifying high-potential markets and customer segments, and creating a foundation for data-informed decisions, Lykke can drive sustainable revenue growth while maintaining its mission: *to save the future of coffee and coffee farmers.*




## 2. Current Situation & Challenges

### Current Systems Overview
Lykke currently operates its e-commerce and business processes through a combination of specialized systems that each serve a distinct function. These systems are connected in varying degrees, and together they support sales, logistics, finance, and marketing operations.

**Shopify** – The central e-commerce platform, managing online sales, products, customers, and orders. It is the core system through which all transactions are initiated.

**Recharge (Shopify plugin)** – Handles subscription services (e.g., recurring coffee deliveries), integrated within Shopify so that subscription orders flow seamlessly into the order management system.

**Payment Service Providers** (Stripe, Klarna, PayPal, etc.) – Process all customer payments at checkout, including handling fees, refunds, and payouts. These connect directly to Shopify and are essential for financial reconciliation.

**Linklog** (Warehouse Management System) – Manages inventory, picking, packing, and fulfillment. Receives order data from Shopify and passes delivery details to shipping partners.

**Freights** (Shipping carriers such as PostNord, DHL, Budbee) – Deliver customer orders. They receive instructions from Linklog and provide tracking information back to the system.

**Fortnox** – The accounting and ERP system, consolidating financial data from Shopify and the PSPs to manage bookkeeping, invoicing, and compliance.

**GA4 (Google Analytics)** – Tracks customer behavior and marketing performance on Lykke’s e-commerce site, providing insights into traffic sources, conversion funnels, and campaign effectiveness.

In practice, these systems work together as follows: Shopify acts as the central hub, connecting to subscription services (Recharge), payment processing (PSPs), logistics (Linklog and Freights), finance (Fortnox), and analytics (GA4). Currently, insights are often accessed through the individual dashboards of each tool or via manual exports.  

![Current data flow diagram](images/current_data_flow.png)

At present, the complexity is further increased by the fact that each local partner operates its own webshop rather than sharing a single platform. This means that while the systems in use are largely the same across markets, they are managed separately. Data is therefore generated and stored in parallel silos, with variations in processes and reporting between partners. As Lykke expands, this decentralized structure will make it harder to gain a consistent overview of operations and customer behavior across markets.  

---

### 2.2 Challenges  
The current setup presents several challenges for Lykke’s growth ambitions:  

- **Fragmented data** – Information is spread across Shopify, Recharge, PSPs, Linklog, Fortnox, GA4, and local partner systems. Without integration, analysis requires manual consolidation, which is time-consuming and error-prone.  
- **Lack of unified KPIs across markets** – Each system provides metrics, but they are not standardized or easily comparable across geographies and partners. This makes it difficult to answer strategic questions such as which products, markets, or customer segments drive the most value.  
- **Limited visibility for decision-making** – Because insights are siloed within individual tools, management lacks a holistic view of performance. This hampers the ability to identify growth levers, monitor efficiency, and proactively address issues as the business scales.  

*Together, these challenges highlight the need for a more unified and scalable analytics approach, one that enables Lykke to consistently track performance and make data-informed decisions across all markets.*

---

## 3. Business Needs
Lykke needs to:
- Track **core KPIs** (sales, customer segments, inventory, partner performance).
- Identify **growth levers** (which markets, which products, which customers).  
  *(Team 7 & 15’s contributions here)*  
- Build **simple but reliable dashboards** for ongoing decision-making.

---

## 4. Recommended Analytics Approach  

### 4.1 Evaluation of Strategic Options  

**Enterprise Data Warehouse (Snowflake/dbt, etc.)**  
An enterprise data warehouse is a centralized platform designed to store, transform, and integrate very large and complex datasets from multiple systems. Tools like Snowflake and dbt enable companies to build robust pipelines, apply advanced transformations, and scale analytics as data volumes grow.  

- **Benefits**:  
  - Provides a single source of truth by consolidating all systems into one structured environment.  
  - Enables advanced analytics, machine learning, and automation.  
  - Strong governance and data quality management.  

- **Limitations for Lykke**:  
  - High upfront cost and technical overhead, requiring dedicated data engineering resources.  
  - Longer implementation timeline before insights are available.  
  - Would add more complexity than value for Lykke’s setup: even as the company scales across more markets, the overall data volume will remain relatively small (sales, products, partners). The challenge is **data consistency across markets**, not “big data.”  
  - In practice, an enterprise warehouse would add complexity and costs without creating proportional value for Lykke.  

---  

**Lightweight Business Intelligence tool (Power BI, Looker Studio)**  
A lightweight BI approach connects directly to existing data sources (e.g., Shopify, Fortnox, GA4) without building a full warehouse. Power BI allows the creation of interactive dashboards, applying basic transformations and modeling within the tool itself.  

- **Pros**:  
  - Faster to implement and more cost-effective compared to a full data warehouse.  
  - Allows teams to start tracking KPIs and visualizing data quickly.  
  - Direct connectors for most of Lykke’s current systems reduce the need for heavy engineering.  
  - Flexible and user-friendly for non-technical users, supporting self-service reporting.  

- **Cons**:  
  - Data remains fragmented unless connectors and models are carefully maintained.  
  - Limited history and depth of analysis compared to a warehouse.  
  - Scalability challenges: as Lykke grows and adds markets, dashboards will require oversight to ensure accuracy and consistency.  





































### 4.2 Most Suitable Approach for Lykke
- Power BI as the right fit.  
- Lykke’s challenge = **data consistency**, not massive data volume.  
- Power BI provides a **pragmatic and scalable solution** for their context.  






















---

## 5. Power BI Implementation Considerations
### 5.1 How Power BI Works for Lykke
- Connects to Shopify, Fortnox, GA4 (via APIs or exports).  
- Imports data into its internal model.  
- Provides one central dashboard where managers see all key metrics across markets.  

### 5.2 Challenges of This Approach
- Limited historical data retention (90 days).  
- Data consistency issues with more local partners.  
- Effort of scaling reporting (new setup per partner).  

**Mitigation strategies:**  
- Define consistency rules.  
- Assign ownership of data checks.  
- Use archiving to preserve historical snapshots.  
- Consider third-party connectors (noting cost trade-offs).  

---

## 6. Roadmap
**Short-term (0–3 months):**  
- Build a prototype dashboard in Power BI with Shopify & Fortnox data.  
- Agree on core KPIs.  
- Provide training.  

**Mid-term (3–9 months):**  
- Expand dashboard to PSPs & shipping/fulfillment data.  
- Standardize partner reporting templates.  
- Set up data archiving practices.  

**Long-term (9–18 months):**  
- Roll out dashboards for new markets.  
- Formalize governance (KPI definitions + ownership).  
- Add connectors or light automation to reduce manual effort.  

---

## 7. Conclusion & Next Steps
- Clear summary of findings.  
- Expected business impact.  
- Suggested next steps for Lykke.  
 


----------------------------------------------------------------------------------------









































----------------------------------------------------------------------------------------

# Basic Markdown Formatting

# Title (H1)
## Section (H2)
### Subsection (H3)
#### Sub-subsection (H4)

*italic*   or   _italic_
**bold**   or   __bold__
~~strikethrough~~

- Bullet point
- Another one
  - Nested bullet

1. Numbered list
2. Second item
   1. Sub-item

[Link text](https://example.com)
![Alt text for image](path_or_url_to_image)

### Tables
| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Row 1    | Data     | More     |
| Row 2    | Data     | More     |

### Code blocks
`inline code`

```python
# multi-line code block
print("Hello World")


**Blockquotes (for highlighting quotes/insights):**
```md
> This is a highlighted quote or note.


