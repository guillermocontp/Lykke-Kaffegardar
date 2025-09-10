# Lykke-Kaffegårdar
Lykke Kaffegårdar technical data pipeline demonstration


## 1. Executive Summary
Lykke Kaffegårdar is Sweden’s fastest-growing sustainable coffee project, now expanding across multiple European markets. As the company prepares to scale its e-commerce from ~2M SEK annually to a tenfold increase, it faces a key challenge: ensuring consistent, reliable data insights across partners and markets. Fragmented reporting and limited visibility into customer behavior, product performance, and partner operations currently hinder decision-making and revenue growth.

This report outlines how Lykke can address these challenges by adopting a lightweight but scalable analytics approach. Instead of investing in a full-scale data warehouse at this stage, we recommend beginning with a Business Intelligence (BI) solution such as Power BI. This allows Lykke to connect existing systems (Shopify, Fortnox, GA4, PSPs, and logistics platforms), define and track core KPIs, and build clear, actionable dashboards for decision-makers.

Our proposed approach balances immediate needs—simple, reliable insights to guide growth—with long-term scalability. By establishing unified KPI tracking, identifying high-potential markets and customer segments, and creating a foundation for data-informed decisions, Lykke can drive sustainable revenue growth while maintaining its mission: *to save the future of coffee and coffee farmers.*


## 2. Current Situation & Challenges

### 2.1 Current Systems Overview
Lykke currently operates its e-commerce and business processes through a combination of specialized systems that each serve a distinct function. These systems are connected in varying degrees, and together they support sales, logistics, finance, and marketing operations.

- **Shopify**: Central e-commerce platform for online sales, products, and customers.

- **Recharge** (Shopify plugin): Manages subscriptions, integrated with Shopify orders.

- **Payment Service Providers** (Stripe, Klarna, PayPal, etc.): Process customer payments, fees, and refunds.

- **Fortnox** (B2B): ERP/accounting system for wholesale operations (invoices, customer accounts). Data flows into Actigate for reporting.

- **Actigate**: Business intelligence and integration layer, pulling data from Fortnox and providing consolidated financial/operational insights.

- **Webshipper** (B2C): Shipping automation system for consumer orders. Connects Shopify to freight carriers for fulfillment and tracking.

- **Freights** (PostNord, DHL): Shipping carriers that deliver orders to customers, receiving instructions from Webshipper.

- **Linklog** (WMS): Warehouse Management System (if still used alongside Webshipper, likely for stock/returns).

- **GA4** (Google Analytics): Tracks marketing performance, customer traffic, and site behavior.

- **Klaviyo** (Shopify app): Marketing automation tool for email/SMS, customer segmentation, and campaign performance.


In practice, these systems work together as follows: Shopify acts as the central hub, connecting to subscription services (Recharge), payment processing (PSPs), logistics (Linklog and Freights), finance (Fortnox), and analytics (GA4). Currently, insights are often accessed through the individual dashboards of each tool or via manual exports.  

![Current data flow diagram](images/current_data_flow.png)

At present, the complexity is further increased by the fact that each local partner operates its own webshop rather than sharing a single platform. This means that while the systems in use are largely the same across markets, they are managed separately. Data is therefore generated and stored in parallel silos, with variations in processes and reporting between partners. As Lykke expands, this decentralized structure will make it harder to gain a consistent overview of operations and customer behavior across markets.  

---

### 2.2 Challenges  
The current setup presents several challenges for Lykke’s growth ambitions:  

- **Fragmented data**: Information is spread across Shopify, Recharge, PSPs, Linklog, Fortnox, GA4, and local partner systems. Without integration, analysis requires manual consolidation, which is time-consuming and error-prone.  
- **Lack of unified KPIs across markets**: Each system provides metrics, but they are not standardized or easily comparable across geographies and partners. This makes it difficult to answer strategic questions such as which products, markets, or customer segments drive the most value.  
- **Limited visibility for decision-making**: Because insights are siloed within individual tools, management lacks a holistic view of performance. This hampers the ability to identify growth levers, monitor efficiency, and proactively address issues as the business scales.  

*Together, these challenges highlight the need for a more unified and scalable analytics approach, one that enables Lykke to consistently track performance and make data-informed decisions across all markets.*


## 3. Business Needs

To guide Lykke's expansion, we need a clear set of strategic KPIs to act as our North Star. But before we define that ultimate destination, we must first map out our starting point. Every successful growth strategy is built on a solid data foundation, so our "data journey" will begin by exploring the powerful insights we can unlock right now. We'll start by using the tools and data you already have—your Shopify order history and Fortnox financial records—to build a foundational understanding of the business. By first mastering what this data tells us, we can then build a clear and actionable path toward the high-level metrics that will truly drive your growth.

### 3.1 The Journey from Operational Metrics to Strategic Growth

Your consolidated Orders data file is the pulse of your e-commerce store. It captures every customer interaction, every product sold, and every discount claimed. This is the frontline of your business, and it provides the first layer of critical insights. (named `orders data LTM AUG 2025` when you shared it with us)

#### **What We Can Track Today (The Customer's Viewpoint)**

From this single file, you can understand your business from the customer's perspective. You can answer crucial questions about sales and marketing effectiveness:

  * **What are our Top-Selling Products?** By summing the `Lineitem quantity` for each `Lineitem name`, you can see exactly which coffee beans or capsules your customers love the most.
  * **What is our Average Order Value (AOV)?** By taking the average of the `Total` column for each unique order (`Name`), you can track how much the typical customer spends in one transaction.
  * **How Effective Are Our Discounts?** By analyzing the `Discount Code` and `Discount Amount` columns, you can see which promotions are most popular and how much revenue you are giving up to drive those sales.

These KPIs are essential. They tell you what's happening on your website and help you answer the question: **"What are our customers buying and why?"**


### Moving forward: Strategic KPIs

Right now, with your Fortnox data, you have a powerful lens into the daily health of your business. (the file is `article data fortnox 2024-2025`)

#### **Phase 1: What We Can Track Today**

From this file, you can immediately pull essential operational KPIs. These are your foundational metrics, your ship's instruments that tell you your current speed and heading:

* **Sales by Units (`Summa_Enheter`):** You can see which coffee—like the "Uganda UFO 250g"—is flying off the shelves. This is perfect for managing inventory and knowing what's popular.
* **Gross Profit Margin:** By calculating `(TB / Summa_SEK_inkl_rabatt) * 100`, you know how much profit you make on the coffee beans themselves after their direct cost. It answers the question: "Is our pricing correct for the product?"
* **Top Products by Revenue (`Summa_SEK_inkl_rabatt`):** This shows you which products are bringing in the most money. It’s a great way to identify your star performers at a glance.

These KPIs are vital. They help you answer the question: **"How are we doing right now?"**

But as you grow, a more important question emerges: **"Where should we invest our time and money to grow faster and more profitably?"** This is where the limitations of these initial KPIs start to show.

#### **Phase 2: The Strategic Shift – The Missing Piece of the Puzzle**

Imagine you run a "20% Off" promotion using the `Discount Code` "SUMMERDEAL". Your `Orders Data` file shows a massive spike in sales for your "UFO 250g coffee." It looks like a huge success.

The immediate conclusion is to run more 20% off promotions.

But this data is missing two critical pieces of financial information:
1.  **The cost of the coffee beans themselves (COGS).**
2.  **The cost of getting that customer to your website to make the purchase.**

To make strategic decisions, you must evolve from answering "What did we sell?" to answering the real question: **"After all variable costs, did this sale actually make us money?"**

#### **Phase 3: Putting it into Practice for Growth**

To calculate a truly accurate Contribution Margin, you must account for all the variable costs that go into making a specific sale. These costs come from different parts of your business, primarily the product cost itself (from Fortnox) and the marketing cost required to bring that customer to your store (from platforms like Google Analytics).

In our example, we use the Customer Acquisition Cost (CAC) to represent this marketing spend. This metric is so crucial that it's one of the four strategic KPIs we recommend, and we explain how to calculate it in detail later. While you could calculate a margin using only the product cost, the result would be incomplete. By including the cost to acquire the customer, you get the real, actionable truth about your profitability.


To make the Contribution Margin your strategic guide, the goal is to create a single, powerful view that combines three essential pieces of data for every sale:

1.  **The Sale Itself:** From your `Orders Data` file, you know what was sold, at what price, and with what discount.
2.  **The Product Cost:** By linking that sale to your `Article data fortnox` file using the product SKU, you can attach the specific Cost of Goods Sold (COGS) for that item.
3.  **The Acquisition Cost:** By pulling in data from Shopify or Google Analytics, you identify the marketing channel that brought in the customer (e.g., a paid ad, an email campaign, or an organic search) and assign the advertising cost associated with that sale.

When you bring these three datasets together, you create a complete picture. This allows you to calculate the true **Contribution Margin** for every single order, giving you a precise measure of profitability. 

#### Example
Let's revisit our "SUMMERDEAL" scenario, but now we'll look at two customers who made the *exact same purchase* but came from different channels.(**The numbers written here are not taken from the data file and are only used for this example!**)

**First, we find the product margin:**
* **Net Price of "UFO 250g" (after 20% off):** 87.80 SEK
* **COGS (from Fortnox):** -91.92 SEK
* **Product Margin:** **-4.12 SEK** (This sale is already unprofitable before marketing costs)

Now, let's factor in the **Customer Acquisition Cost (CAC)**.

**Customer A: Acquired via a Google Ad**
This customer clicked a paid search ad to find your site.
* **Product Margin:** -4.12 SEK
* **Cost of Google Ad Click (CAC):** -35.00 SEK
* **True Contribution Margin: -39.12 SEK**

**Customer B: Acquired via Organic Search**
This customer found you through an unpaid Google search result.
* **Product Margin:** -4.12 SEK
* **Cost of Acquisition (CAC):** -0.00 SEK
* **True Contribution Margin: -4.12 SEK**

**The Revelation:**

Your "successful" promotion is a significant financial drain, especially when driven by paid ads. You are paying **39.12 SEK** for every customer you acquire through that channel with that discount. This insight is transformative because it shifts your focus from product-level profitability to **channel and customer profitability**.


Your strategy now evolves. Instead of just pushing popular products, you make data-driven decisions to improve profitability:
* **Optimize Ad Spend:** Stop running ads for the "SUMMERDEAL" promotion, or reduce the discount for paid traffic to ensure every sale is profitable.
* **Invest in SEO:** Since the organic channel delivers profitable (or less unprofitable) customers, you can invest more in content and SEO to attract them for free.
* **Focus on High-Value Channels:** Analyze which channels bring you customers who not only buy profitably on their first order but also come back for more, leading to a high **Customer Lifetime Value (CLV)**.

By connecting your sales, financial, and marketing data, you evolve from tracking product sales to engineering customer profitability. This is the key to building a truly sustainable and scalable coffee company.


### 3.2 A Simple Framework for Profitable Growth

Now that we've seen how to connect your sales and financial data, the final step is to build a clear framework that uses these insights to guide your growth. Instead of getting lost in dozens of metrics, the goal is to focus on a few "North Star" KPIs that tell you if the business is truly healthy and moving in the right direction.

Four key questions will define your success:

* **Are we growing our customer base?** (*Acquisition / Growth*) *New Customers per Month* — measures expansion of the customer base.
* **Are our customers coming back for more?** (*Retention / Loyalty*) *Customer Retention Rate (CRR)* — signals the ability to build lasting relationships and repeat purchases. 
* **Is the lifetime value of a customer greater than what we pay to acquire them?** (*Sustainable Profitability*) *CLV/CAC Ratio* — ensures that the value of customers outweighs acquisition costs.
* **Does every sale actually make us money after all variable costs?** (*Unit Profitability*, our **Contribution Margin %**)— shows whether each sale contributes positively after product, marketing, and variable costs.

### Core KPIs: where to find them in your files?

| **KPI** | Type | Data source | Columns needed | Available in existing datasets? | Why relevant |
|---------|------|-------------|----------------|---------------------------------|--------------|
| **New Customers per Month** | Core – Acquisition | Shopify (Orders_data_LTM + Shopify sessions) | `customer_id`, `order_date` (derive `first_order_date` by `MIN(order_date)` per `customer_id`), `sessions` | Yes | Direct measure of B2C customer base expansion; primary growth signal. |
| **Customer Retention Rate (CRR)** | Core – Loyalty | Shopify (Orders_data_LTM) + Recharge | Shopify: `customer_id`, all `order_date`s to track repurchase windows; Recharge: `subscription_id`, `status`, `start_date`, `end_date` | Yes | Shows ability to keep customers buying; key to sustainable growth. |
| **CLV / CAC Ratio** | Core – Profitability | Shopify (Orders_data_LTM) + Recharge + Ads/Klaviyo | **CLV:** `customer_id`, `order_total`/`subtotal`, order cadence; Recharge recurring revenue & tenure. **CAC:** marketing `spend` and `new_customers_acquired` by campaign/channel | Partial (needs ad spend) | Ensures lifetime value exceeds acquisition cost so growth is economically viable. |
| **Contribution Margin %** | Core – Profitability | Shopify (Orders_data_LTM) + Linklog + PSPs (+ internal product cost per SKU) | `revenue`, `discounts`, per-order `shipping_cost` (Linklog/Webshipper), `psp_fee` (Stripe/Klarna/PayPal), `COGS_per_SKU` | Partial (needs shipping/fees/COGS detail) | Validates unit economics; scaling only makes sense if each order is contribution-positive. |


Think of these as your ultimate destination. To understand the journey, you'll use a dashboard of **supporting metrics**—like **Average Order Value (AOV)**, **Conversion Rate**, and **Purchase Frequency**. These secondary KPIs are your diagnostic tools. They don't define success on their own, but they brilliantly explain *why* your core metrics are changing. For example, if retention drops, a glance at purchase frequency might tell you the story. We have added many supporting KPIs and how to find them in the Anex. 

With this framework in place, you can focus on pulling the three main **levers of growth**:

* **Markets:** Where are our most profitable customers, and which new regions should we target?
* **Products:** Which coffees create loyal fans and encourage bigger orders?
* **Customers:** Who are our best customers, and how do we find more people like them?

The final piece is to bring this to life in simple, reliable dashboards. Since you'll operate a central e-commerce site with local partners handling fulfillment, these dashboards must show both the global picture and a partner-level breakdown. This ensures that strong growth in one market doesn't hide underperformance in another, keeping the system fair, transparent, and aligned for shared success.


### 3.3 Industry Benchmarks (2024–2025)

Lykke’s e-commerce KPIs can be further understood by comparing them with industry benchmarks from leading sources:

**Nudge — Key E-commerce Benchmarks 2025**  
- Conversion Rate: **1.58%**  
- Average Order Value (AOV): **$121.37**  
- Cart Abandonment Rate: **70.19%**  
- Customer Retention Rate (CRR): **38%**  
- CLV/CAC Ratio: **≥ 3:1** (a healthy business ensures CLV is at least 3x CAC)  
- Return Rate: **20–30%**  
- Customer Satisfaction (CSAT): **70–80%**  

**Shopify — Customer Retention by Industry (2025)**  
- E-commerce Retention Rate: **30%**  

**Ecommercedb — Sweden (Beverages eCommerce, 2024)**  
- Add-to-Cart Rate: **12.3%**  
- Cart Abandonment Rate: **70.7%**  
- Conversion Rate: **3.6%**  
- Average Order Value (AOV): **$119**  
- Discount Rate: **10.2%**  
- Return Rate: **3.0%**  

These figures provide a **reference point** for setting expectations. For instance, if Lykke’s conversion rate significantly underperforms vs. 3.6% (Swedish beverages), it indicates friction in the purchase funnel. Similarly, tracking CLV/CAC against the 3:1 guideline ensures sustainable growth. Over time, Lykke’s own benchmarks will be more valuable for guiding decisions than external averages.

### 3.4 A/B Testing: The Engine for Smart Growth

Our data journey so far has focused on connecting your sales and financial reports to create a clear, accurate picture of your business performance. This gives you a powerful understanding of **what has happened**—which products are most profitable, which sales are most valuable, and where your core strengths lie.

The next logical step in this journey is to use these insights to actively shape what happens **next**. This is where we shift from analyzing the past to experimenting for the future, and the most effective and data-driven tool for this is A/B testing. It’s how you take an insight and turn it into a measurable improvement.
As you can see, A/B testing is a powerful engine for turning insights into measurable growth. To help you get started on this path, we will provide a list of recommended and easy-to-use A/B testing tools in the appendix as well as some terminology. 

#### **what is A/B testing?**

At its core, **A/B testing** is a simple method of comparing two versions of something to see which one performs better. Think of it as asking your customers a direct question—"Do you prefer this headline or *that* one?"—and letting their clicks and purchases give you the definitive answer.

The beauty of A/B testing is its simplicity and cyclical nature. Modern e-commerce and marketing tools make it incredibly easy to set up tests without needing a developer. This allows you to get into a powerful rhythm: **Test, Learn, Repeat**. You run a small experiment, learn from the results, implement the winning version, and then move on to the next idea. It's the engine of continuous improvement.

Let's build a narrative. Lykke is planning a new marketing campaign with one clear goal: **convert more first-time website visitors into paying customers.** You have a budget for ads, but you want to make sure the website experience itself is as effective as possible. Here’s how you’d use A/B testing to do it.

#### **Step 1: The Signal (The "Aha!" Moment in Your Data)**

Your journey starts in **Google Analytics**. While reviewing your reports, you notice a clear pattern: a high number of new visitors come to your site from social media, they browse the popular "Best Sellers" collection, add a bag of coffee to their cart... but then a large percentage leave the site without completing the purchase.

This is a **signal**. Your data is showing you exactly where the hesitation is happening. The interest is there, but something is stopping them from taking that final step.

#### **Step 2: The Hypothesis (The "What If...?" Question)**

Based on this signal, your team forms a simple, testable idea:

> "We believe that offering a compelling welcome incentive to first-time visitors will reduce cart abandonment and increase our conversion rate. We hypothesize that a **'Free Shipping on Your First Order'** offer will be more effective than a percentage discount."

#### **Step 3: The Test (The A/B/C Experiment)**

Instead of just guessing, you run an experiment. Using an A/B testing tool integrated with your site, you create three versions of the new visitor experience, which will be shown randomly to different users for two weeks:

* **Version A (The Control):** Your website as it is today. No special offer is shown.
* **Version B (The "Free Shipping" Variant):** A banner appears for new visitors that says, *"Welcome to Lykke! Enjoy Free Shipping On Your First Order."*
* **Version C (The "Discount" Variant):** A similar banner appears, but it offers *"Welcome! Get 15% Off Your First Bag of Coffee."*

The tool will automatically handle splitting the traffic and tracking the one metric that matters for this test: the **new customer conversion rate**.


#### **Step 4: The Result (The Data-Driven Decision)**

After two weeks, the results are in, and they are crystal clear.

* **Version A (No Offer):** Had a new customer conversion rate of **1.8%**.
* **Version B (Free Shipping):** Had a new customer conversion rate of **3.1%**.
* **Version C (15% Off):** Had a new customer conversion rate of **2.4%**.

The data has spoken. The **"Free Shipping"** offer is the decisive winner, nearly doubling your conversion rate compared to doing nothing. You now have concrete proof, not just an opinion, that this is the best offer to attract new customers. You confidently roll out the "Free Shipping" banner to 100% of new visitors, knowing it will drive more sales and make your marketing ad spend far more efficient.

And the process continues. Your next test might be to see if a different headline on that banner can push the conversion rate from 3.1% even higher. This is how you build a powerful, repeatable engine for growth.


## 4. A Unified Analytics Strategy for Lykke

### 4.1 The Strategic Center for Your Growth: A Unified View in Power BI

You've successfully built a business with excellent products and a loyal customer base. Currently, your operational data resides in powerful, specialized platforms: Shopify for sales, Fortnox for finances, Linklog for logistics, and Google Analytics for web traffic. While each platform provides its own reports, analyzing them in isolation presents challenges. It requires manual effort to connect the dots, makes it difficult to get a holistic view of performance, and can lead to inconsistent metrics.

Together, these challenges highlight the need for a more unified and scalable analytics approach, one that enables Lykke to consistently track performance and make data-informed decisions across all markets. To accelerate your B2C e-commerce growth, you require a clear framework for core KPI tracking.

This is where a business intelligence platform like Microsoft Power BI becomes the strategic center of your growth. By consolidating data from all your essential systems into one place, Power BI transforms your disparate data points into a clear, interactive, and always up-to-date view of your business health.

### 4.2 A Crucial Step: Turning Raw Data into Business Wisdom with Data Modeling

Before your data appears in a Power BI dashboard, it goes through a vital, transformative step called **Data Modeling**. It is arguably the most valuable part of this entire process.

![Consolidation](/images/image_consolidation.png)

Think of your raw data from Shopify, Fortnox, and other platforms as high-quality, raw ingredients: flour, eggs, sugar, and coffee beans. By themselves, they are individual components. You can look at each one, but their true potential is only unlocked when you combine them according to a well-defined recipe.

**Data modeling is that recipe.**

It is the process where we define the business logic to intelligently connect, clean, and enrich your raw data. It's where we transform technical information into a format that reflects how you actually run your business:


**It Connects the Dots:** It links an order from Shopify with its corresponding shipping costs from Linklog and the marketing spend from Google Analytics that generated the sale.

**It Creates Powerful New Metrics:** It allows us to calculate enriched data points that don't exist in any single system. For example, we can take Revenue from Shopify and subtract Cost of Goods from Fortnox to create a new, essential metric: Gross Profit per Product.

**It Standardizes Your Business Language:** It ensures that a "sale," a "customer," or a "region" is defined consistently across all reports. It translates cryptic field names (like `ga:source`) into plain English (Marketing Source).


### 4.3 The Strategic Advantages of a Unified Data Model

![the proposed prototype](/images/warehhouse.png)

By consolidating and modeling your data, we transform it from a simple technical utility into a powerful strategic asset. This provides several key advantages for Lykke:

**Unlock Deeper Insights:** You can finally answer critical, cross-functional questions:

- What is the true profit margin on our best-selling product after factoring in specific costs from Fortnox and shipping fees from Linklog?
- Which Google Analytics marketing campaign is driving the most profitable customers on Shopify?

**Establish a Single Source of Truth:** By defining business logic centrally, every report and dashboard is built on the same trusted, consistent foundation. 

**Automate Reporting and Empower Your Team:** This approach replaces time-consuming manual data collection with automated, reliable dashboards that are always up-to-date. The clean, intuitive data model makes it easy for anyone on your team to explore information through interactive reports and create their own analyses without needing deep technical skills.

**Build a Scalable Foundation for Growth:** This model is a flexible asset that can easily grow with your business. As you add new data sources in the future, like an in-store sales system, they can be integrated into the existing framework, enriching your insights without requiring you to start over.

Ultimately, this unified approach ensures your final dashboards are not just informative, but are a reliable tool for making truly insightful, data-driven decisions.





## 5. Technical Description

To achieve this consolidated view in Power BI, we must connect to your various platforms and bring the data together. There are two primary architectural approaches to accomplish this. The choice we make will depend on our long-term goals for scalability and data ownership.

### Option 1: The Scalable Warehouse Approach

Think of a data warehouse as a central, organized library for all of Lykke's historical data. In this model, data is first extracted from your sources, cleaned, and stored in this central hub. Power BI then connects to this pristine, well-organized data to create reports.

**The necessary components are:**

- **Data Ingestion Tool:** Built-in or custom tools to pull data from your sources directly into Power BI.
- **Cloud Data Warehouse:** A highly scalable database (e.g., Snowflake, Google BigQuery) that stores and processes the data.
- **Power BI:** The visualization tool that connects to the warehouse.

### Option 2: The Direct Connection Approach

In this model, Power BI connects directly to each of your platforms. Its built-in data preparation tool, Power Query, is then used to pull, combine, and clean the data within Power BI itself. 

**The necessary components are:**

- **Data Ingestion Tool:** Built-in or custom tools to pull data from your sources directly into Power BI.
- **Power BI (with Power Query):** Serves as the all-in-one tool for ingestion, data modeling, and visualization.


### 5.1 How Data is Ingested

Creating a unified dashboard requires an automated and secure method to pull data from various platforms like Shopify and Fortnox. This process is handled by communicating with each platform's **API (Application Programming Interface)**.

An API can be understood as a dedicated waiter in a restaurant. Instead of entering the kitchen (a platform's complex internal system), a structured order for data is given to the waiter (the API). The waiter communicates with the kitchen and returns with the specific information requested. This provides a secure and standardized way for different software systems to exchange data.

To communicate with these APIs, **connectors** are used. For popular platforms, pre-built, standard connectors are often available. For systems where a standard connector doesn't exist, a custom development is performed. 

![description of connectors as part of the architecture](/images/connector.png)

The general approach is to use available connectors wherever possible and build custom ones where necessary to link all required systems seamlessly.
This is a summary of the data sources that Lykke uses:


**E-commerce & Customer Data**
- **Shopify**: Connects directly to Power BI through a native connector or via scheduled CSV/API exports. Provides key data on orders, customers, products, and revenue.
- **Recharge** (subscriptions): Data is stored within Shopify orders but can also be accessed through Recharge’s API. Enables subscription-specific analysis, such as recurring revenue and churn.

**Payments & Finance**
- **Payment Service Providers**: Transaction data can be imported via CSV exports or API connectors into Power BI. This makes it possible to track payment volumes, fees, and refund rates.
- **Fortnox** (ERP for B2B): Finance and wholesale data can be accessed in two ways. 
One is to connect direct to Power BI: possible via Fortnox API or third-party connectors, but requires ongoing setup and maintenance. The other option is via Actigate: already structures and consolidates Fortnox data into business-ready reports, reducing complexity.
For Lykke, using Actigate as the middle layer is more practical, as it minimizes technical overhead while ensuring financial data is consistent and reliable.

**Logistics & Fulfilment**
- **Webshipper** (B2C shipping automation): Connects to Power BI through API or exports. Provides data on shipping lead times, carrier performance, and fulfillment efficiency.
- **Freights** (PostNord, DHL): Shipment details are consolidated in Webshipper, so Power BI consumes these metrics indirectly.
- **Linklog** (WMS): If still in use, stock and returns data can be added to Power BI through CSV exports or API feeds.

**Marketing & Traffic**
- **Google Analytics 4** (GA4): Connects via a native Power BI connector or through BigQuery/CSV exports. Brings in website traffic, conversion funnels, and acquisition insights.
- **Klaviyo** (email/SMS automation): Data can be connected via API or exports into Power BI. This enables analysis of campaign performance, customer segmentation, and re-engagement metrics.


**Key Takeaway:** While standard platforms like Shopify and Google Analytics are easy to connect, more specialized systems like Fortnox and Linklog will likely require custom development work.

### 5.2 Choosing the Right Path for Lykke

Each architecture is optimized for different goals. The right choice for Lykke is a strategic decision that balances short-term speed with long-term scalability and data ownership. Below is a framework to help guide this decision.

| **Consideration** | **Direct Connection to Power BI** | **Scalable Warehouse Approach** |
|---|---|---|
| **Speed to First Dashboard** | 🚀 Faster. Ideal for getting initial insights quickly. | Slower. Requires more upfront setup of the warehouse. |
| **Initial Cost** | 💰 Lower. Primarily the cost of Power BI licenses. | Higher. Includes costs for the warehouse and ingestion tools. |
| **Scalability & Future-Proofing** | Limited. Can become complex and slow as you add more data sources or increase data volume. | ✅ High. Built to easily handle new data sources, larger volumes, and future needs (like AI). |
| **Data Ownership** | Data is modeled and stored within Power BI's ecosystem. | You own and control a central, independent copy of your data in the warehouse. |


### 5.3 Challenges and Mitigation Strategies

#### Limited Historical Data Retention
APIs such as Shopify typically provide only limited transaction history (often 90 days). Without intervention, this restricts Lykke’s ability to run longer-term analyses or compare performance across years. Lykke has two practical options to address this:

- **Manual exports** (low-cost approach): Each month, a team member exports the relevant data (e.g., Shopify orders, Fortnox transactions, GA4 traffic) and saves the file in a shared Dropbox folder. Power BI can connect directly to Dropbox, automatically reading and stacking all new files into one historical dataset. This creates a reliable “data archive” without extra costs. The limitation is that the process depends on discipline — someone must remember to do the export each month.
- **Connectors** (automated approach): Third-party connectors (e.g., Supermetrics, Stitch, Funnel.io) can automatically pull both historical and ongoing data into Power BI. This removes the risk of missed exports and keeps dashboards continuously up to date. However, connectors involve recurring subscription costs, so Lykke will need to weigh the benefit of automation against the additional expense.

#### Data Consistency Across Local Partners
As Lykke expands into new markets and adds more local partners, consistency across data fields becomes critical. Product codes, order categories, and financial reporting structures must be aligned to ensure reliable cross-market comparisons. Power BI will not automatically enforce this consistency — it requires Lykke to define clear rules and assign responsibility for checking and maintaining alignment.

- **Set consistency rules**: Define clear standards for product codes, order categories, and reporting fields when onboarding new partners.
- **Assign ownership**: Designate a team member responsible for regularly checking that exports are aligned and dashboards remain reliable.

#### Scaling Reporting Across Partners
Power BI is well suited to managing multiple markets, but each new partner requires setting up additional connections and may involve adjustments to the data model. This means that scaling reporting is less about technical automation and more about disciplined governance, ensuring that each new market follows the same data standards and processes.

- **Document and standardize processes**: Ensure that onboarding new partners includes a checklist for reporting setup.
- **Regular data checks**: Have the assigned data owner review dashboards when new partners are added, making sure KPIs remain comparable across markets.
- **Consider connectors selectively**: For frequently used data sources, a connector may reduce effort by automating repetitive setup, even if this adds some cost.


## 6 Unified Roadmap: From Decision to an Analytics platform.

This new roadmap is a single, unified plan. It begins with the crucial strategic decision about our architecture, which will then dictate the specific tasks in the subsequent phases.

### Phase 1: Strategy & Architectural Decision (1-2 Weeks)

**Activities:** Finalize the core KPIs for the first dashboards. Conduct a workshop to review the pros and cons of the "Direct Connection" vs. "Warehouse" architectures.

**Deliverable:** A signed-off project plan with the officially chosen architecture.

### Phase 2: Foundation & Setup (1-3 Weeks)

**Activities:** Based on the decision in Phase 1, we will either configure the Power BI workspace for direct connections or provision and set up the cloud data warehouse and ingestion tools.

**Deliverable:** A fully configured technical environment ready for development.

### Phase 3: Pipeline Development & Data Modeling (4-6 Weeks)

**Activities:** Connect to all data sources (Shopify, Fortnox, etc.), including any necessary custom development. Build the core data model that cleans, combines, and enriches the data into a "single source of truth."

**Deliverable:** A robust and automated data pipeline feeding analysis-ready data.

### Phase 4: Visualization & Training (2-3 Weeks)

**Activities:** Build the interactive dashboards in Power BI. Validate the metrics and visuals with your team to ensure they are clear and actionable. Conduct training sessions on how to use and interpret the dashboards.

**Deliverable:** A suite of validated, insightful dashboards and a trained user base.

### Phase 5: Go-Live & Handover (1 Week)

**Activities:** Deploy the final dashboards for company-wide use. Provide final documentation and establish a plan for ongoing support and maintenance.

**Deliverable:** The official launch of Lykke's new analytics platform.


---


 


----------------------------------------------------------------------------------------

## Appendix 1 – KPI Framework for Lykke B2C E-commerce

### 1. Objectives and Sub-objectives

To align Lykke’s e-commerce strategy with measurable outcomes, we structured the analysis around three main objectives and their sub-objectives:

- **Acquisition / Growth** → Expand the customer base through efficient marketing.
- **Retention / Loyalty** → Strengthen customer relationships and repeat purchases.
- **Profitability** → Ensure sustainable unit economics and long-term business health.

---

### 2. Core and Supporting KPIs

#### ACQUISITION / GROWTH
- **Core KPI**
  - **New Customers per Month** → Direct measure of customer base expansion.
- **Supporting KPIs**
  - Website Traffic → Indicates reach but does not prove customer growth.
  - Conversion Rate → Explains efficiency of the acquisition funnel.
  - Add-to-Cart Rate → Shows how effectively product pages generate buying intent.
  - Cart Abandonment Rate → Diagnoses checkout friction or price sensitivity.
  - CTR on Ads/Email → Tactical marketing diagnostic, not strategic.

---

#### RETENTION / LOYALTY
- **Core KPI**
  - **Customer Retention Rate (CRR)** → Captures long-term loyalty and repeat engagement.
- **Supporting KPIs**
  - Repeat Purchase Rate → Narrower view than CRR (focuses only on 2+ orders).
  - Purchase Frequency → Helps explain shifts in CLV.
  - Return Rate → Explains potential dissatisfaction and impacts contribution margin.
  - NPS / CSAT → Subjective leading indicators, not direct proof of revenue.
  - Engagement Metrics (e.g., email open rates) → Operational rather than strategic.

---

#### PROFITABILITY
- **Core KPIs**
  - **CLV/CAC Ratio** → Ensures customer lifetime value exceeds acquisition cost.
  - **Contribution Margin (%)** → Validates unit-level profitability after product, marketing, and variable costs.
- **Supporting KPIs**
  - AOV (Average Order Value) → Driver of CLV and margin, but insufficient on its own.
  - Gross Margin (%) → Too partial, excludes marketing and shipping costs.
  - Discount Rate → Helps explain changes in AOV and profitability.
  - EBITDA / Operating Profit Margin → Relevant at later stages; less actionable in early growth.
  - Cash Burn / Runway → Critical for financing decisions, not day-to-day operations.

---

#### SUMMARY

- **Core KPIs** answer the question: *“Are we succeeding?”*
- **Supporting KPIs** clarify: *“What is driving our success or setbacks?”*

This layered framework ensures that Lykke focuses on the most critical indicators of e-commerce growth and profitability, while maintaining the diagnostic tools needed for decision-making and continuous improvement.


## Appendix 2 – How to track the KPIs

To track and grow Lykke’s B2C e-commerce performance, we distinguish between two categories of KPIs.  
First, the **core KPIs** represent the most strategic measures of success and directly connect to Lykke’s growth objectives in B2C.  
Second, the **supporting KPIs** act as diagnostic levers that explain why the core KPIs improve or decline, helping identify the underlying drivers of change.  
This are explained and found linking data from different platforms, in the way is explained in the table.


### Core KPIs

| **KPI** | Type | Data source | Columns needed | Available in existing datasets? | Why relevant |
|---------|------|-------------|----------------|---------------------------------|--------------|
| **New Customers per Month** | Core – Acquisition | Shopify (Orders_data_LTM + Shopify sessions) | `customer_id`, `order_date` (derive `first_order_date` by `MIN(order_date)` per `customer_id`), `sessions` | Yes | Direct measure of B2C customer base expansion; primary growth signal. |
| **Customer Retention Rate (CRR)** | Core – Loyalty | Shopify (Orders_data_LTM) + Recharge | Shopify: `customer_id`, all `order_date`s to track repurchase windows; Recharge: `subscription_id`, `status`, `start_date`, `end_date` | Yes | Shows ability to keep customers buying; key to sustainable growth. |
| **CLV / CAC Ratio** | Core – Profitability | Shopify (Orders_data_LTM) + Recharge + Ads/Klaviyo | **CLV:** `customer_id`, `order_total`/`subtotal`, order cadence; Recharge recurring revenue & tenure. **CAC:** marketing `spend` and `new_customers_acquired` by campaign/channel | Partial (needs ad spend) | Ensures lifetime value exceeds acquisition cost so growth is economically viable. |
| **Contribution Margin %** | Core – Profitability | Shopify (Orders_data_LTM) + Linklog + PSPs (+ internal product cost per SKU) | `revenue`, `discounts`, per-order `shipping_cost` (Linklog/Webshipper), `psp_fee` (Stripe/Klarna/PayPal), `COGS_per_SKU` | Partial (needs shipping/fees/COGS detail) | Validates unit economics; scaling only makes sense if each order is contribution-positive. |

---

### Supporting KPIs

| **KPI** | Type | Data source | Columns needed | Available in existing datasets? | Why relevant |
|---------|------|-------------|----------------|---------------------------------|--------------|
| **Website Traffic** | Supporting – Acquisition | Shopify sessions (GA4 if connected) | `sessions`, `source/medium` (channel attribution) | Yes (Shopify); GA4 optional | Explains reach; contextualizes new customers and conversion rate. |
| **Conversion Rate (visitor → buyer)** | Supporting – Acquisition | Shopify sessions + Orders_data_LTM | `sessions`, `orders` | Yes | Explains funnel efficiency from traffic to orders. |
| **Add-to-Cart Rate** | Supporting – Acquisition | Shopify (cart events) or GA4 (ecommerce events) | `sessions`, `add_to_cart` events (or `items_added_to_cart`) | Partial (depends on event tracking in extracts) | Early funnel efficiency; indicates product interest before checkout. |
| **Cart Abandonment Rate** | Supporting – Acquisition | Shopify checkout/cart data | `carts_created`, `checkouts`, `orders_placed` (or `abandoned_checkouts`) | Partial (needs cart/checkout events) | Diagnoses checkout friction/price sensitivity impacting conversion. |
| **CAC (Customer Acquisition Cost)** | Supporting – Acquisition/Profitability | Ads platforms (Meta/Google) + Klaviyo | `spend` by channel/campaign, `new_customers_acquired` | No | Driver of CLV/CAC ratio; reveals whether ratio changes are cost- or value-driven. |
| **Repeat Purchase Rate** | Supporting – Loyalty | Shopify (Orders_data_LTM) | `customer_id`, order counts per period | Yes | Simplified loyalty metric; explains movements in CRR. |
| **Purchase Frequency** | Supporting – Loyalty | Shopify (Orders_data_LTM) | `customer_id`, `order_date` (compute orders per customer per period) | Yes | Core driver of CLV alongside AOV. |
| **Return Rate** | Supporting – Loyalty/Profitability | Linklog (logistics/returns) | `returns`, `shipments` (optionally `return_reason`) | Yes | Impacts contribution margin and satisfaction; high returns depress profitability. |
| **Discount Rate** | Supporting – Profitability | Produkt_export + Orders_data_LTM | `Compare At Price`, `Price`, `discount_code`/`discount_amount` | Yes | Heavy discounting may lift conversion but compress AOV/margins. |
| **AOV (Average Order Value)** | Supporting – Profitability | Shopify (Orders_data_LTM) | `order_id`, `order_total`/`subtotal` | Yes | Direct lever for CLV and unit economics. |
| **Gross Margin % (per product/order)** | Supporting – Profitability | Shopify (Orders_data_LTM) + internal product costs | `revenue`, `COGS_per_SKU` | Partial (needs cost file) | Important profitability driver; incomplete without shipping/marketing. |
| **Email Engagement (open/click)** | Supporting – Loyalty | Klaviyo | `open_rate`, `click_rate`, `campaign_id` | No | Leading indicator for retention; helps optimize lifecycle campaigns. |
| **NPS / CSAT** | Supporting – Loyalty | Surveys/CRM | survey responses, `score`, `timestamp` | No | Predicts churn/retention; complements behavioral metrics. |


---

### Extra KPIs (acknowledged but not prioritized)

Finally, we also acknowledge a set of **extra KPIs**: these are metrics that appear in the datasets and can be calculated, but they are not identified as strategically relevant for growth at this stage. They are included for completeness, in case they become useful for future analysis or operational monitoring.

| **KPI** | Type | Data source | Columns needed | Available in existing datasets? | Why relevant |
|---------|------|-------------|----------------|---------------------------------|--------------|
| **Product Breadth (# SKUs)** | Extra – Operational/Diagnostic | Produkt_export_Aug_2025 | distinct `Handle` (SKU) | Yes | Assortment size; helpful context, not a growth driver by itself. |
| **Product Availability Rate** | Extra – Operational/Diagnostic | Produkt_export_Aug_2025 | `Variant Inventory Qty` > 0 per SKU | Yes | Stock health indicator; indirectly affects conversion/retention. |
| **Average Product Price** | Extra – Operational/Diagnostic | Produkt_export_Aug_2025 | `Variant Price` | Yes | Price positioning context; informs discounting strategy. |
| **On-Time Delivery Rate** | Extra – Operational/Diagnostic | Linklog | `ship_date`, `expected_delivery_date` (or SLA date) | Yes | Service quality signal; supports retention but is a step removed from core KPIs. |
| **Subscription Mix (% of revenue)** | Extra – Diagnostic | Orders_data_LTM + Recharge | order/subscription flag, subscription revenue by period | Partial (needs clear mapping) | Context on revenue resilience from recurring vs one-time. |
| **Channel CAC (by channel)** | Extra – Diagnostic (granular) | Ads platforms + Klaviyo | `spend` by channel, `new_customers_acquired` by channel | No | Granular optimization once high-level CAC is established. |


### Current KPIs to track
This are KPIs that can be extracted directly from your reporting, Fortnox, shopify or google analytics

### KPIs from Financial Data (`Article data fortnox...`)

This file provides a high-level view of your product and category profitability.

| KPI Name | What It Measures | Why It's Important | Columns to Use |
| :--- | :--- | :--- | :--- |
| **Gross Profit Margin** 📈 | The percentage of revenue left after the cost of goods sold (COGS). | It's the primary indicator of your core business profitability and pricing efficiency. | `Summa_SEK_inkl_rabatt`, `COGS` |
| **Contribution Margin (TB)** 💰 | The amount each product contributes to covering fixed costs and generating profit. | It helps identify your most valuable products, guiding strategic focus. | `Name`, `Category`, `TB` |
| **Sales by Revenue & Volume** 📊 | Which products and categories generate the most revenue and sell the most units. | Essential for inventory management and understanding your main revenue drivers. | `Name`, `Category`, `Summa_SEK_inkl_rabatt`, `Summa_Enheter` |

***

### KPIs from E-commerce Data (`Orders Data...`)

This file provides a detailed look at individual customer transactions and sales activity.

| KPI Name | What It Measures | Why It's Important | Columns to Use |
| :--- | :--- | :--- | :--- |
| **Average Order Value (AOV)** 🛒 | The average amount a customer spends in a single order. | Increasing AOV is a key lever for growing revenue without needing more traffic. | `Name` (as Order ID), `Total` |
| **Top Selling Products** 🏆 | Which specific items are purchased most frequently and generate the most gross revenue. | It guides marketing efforts, website merchandising, and day-to-day inventory. | `Lineitem name`, `Lineitem quantity`, `Lineitem price` |
| **Discount Performance** 🏷️ | The usage and total value of different discount codes. | Helps you understand which promotions are most popular with your customers. | `Discount Code`, `Discount Amount` |

---

Of course. Assuming you have a standard e-commerce setup in Google Analytics (GA4), here is a table of the most valuable KPIs you can track.

### KPIs from Google Analytics Data

This data provides a comprehensive view of your website's **audience, user acquisition, and on-site behavior**.

| KPI Name | What It Measures | Why It's Important | 
| :--- | :--- | :--- | 
| **Users / Sessions** 👥 | The number of unique visitors and total visits to your site. | It's the most fundamental measure of your website's reach and audience size. | 
| **Traffic Acquisition** 🚦 | Which marketing channels (e.g., Organic Search, Paid Search, Social) are driving traffic to your site. | It tells you which marketing efforts are working, allowing you to optimize your budget and focus. | 
| **Engagement Rate** 📈 | The percentage of sessions where a user was actively engaged (stayed \>10s, had a conversion, or viewed 2+ pages). | It's a key indicator of content quality and audience relevance. A low rate can signal a disconnect with visitors. | 
| **E-commerce Conversion Rate** 🎯 | The percentage of sessions that result in a purchase. | This is the ultimate measure of your website's effectiveness at turning visitors into customers. | 
| **Total Revenue** 💰 | The total monetary value of all purchases made through the website. | It's the bottom-line metric for measuring the direct financial success of your e-commerce channel. |
| **Cost Per Acquisition (CPA)** 💸 | The average cost to acquire one paying customer from a specific marketing channel. | It directly connects marketing spend to results, helping you ensure your campaigns are profitable. | 



## Key A/B Testing Terms Explained

### 1. Sample Size
This is simply the number of users who need to be included in your test to get a reliable result.

* **In our story:** Before launching the "Welcome Offer" campaign, a testing tool would tell you that you need a certain number of new visitors (e.g., 10,000 per version) to participate. This large **sample size** ensures that the final conversion rates aren't just the result of random luck, making your data trustworthy.

### 2. Minimum Detectable Effect (MDE)
This is the smallest improvement you're interested in detecting. It answers the question, "How big of a change would make this test worthwhile?"

* **In our story:** You might decide that you'll only implement a new offer if it increases the conversion rate by at least **0.5%**. This is your **Minimum Detectable Effect**. You're telling the tool not to bother you with tiny, insignificant changes. Setting a realistic MDE is crucial, as trying to detect a very small effect requires a much larger sample size.

### 3. Statistical Confidence (or Significance)
This is a measure of how certain you can be that your results are not a random fluke. It's usually expressed as a percentage (e.g., 95% confidence).

* **In our story:** When the test concluded that "Free Shipping" was the winner, the tool would report a **statistical confidence** level of, say, 98%. This means you can be 98% sure that the increase in sales was directly caused by the free shipping offer and that if you ran the same test again, you would see the same result. It's the mathematical proof that gives you the confidence to roll out the winning version to everyone.