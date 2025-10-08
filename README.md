# 📊 Sales Performance Analytics Dashboard

> **"Why did revenue spike 40% in November, yet customer acquisition remained flat?"** This question sparked my deep-dive into building an interactive analytics dashboard that transforms raw transactional data into actionable business intelligence.

## 🎯 The Business Challenge

E-commerce businesses generate massive volumes of transaction data daily, yet struggle to extract meaningful insights that drive strategic decisions. This dashboard addresses the critical gap between data collection and data-driven decision-making by providing:

- **Real-time visibility** into revenue trends, customer behavior, and product performance
- **Geographic intelligence** to optimize market-specific strategies across 5+ countries
- **Customer lifetime value tracking** to identify high-value segments and retention opportunities
- **Product performance metrics** to inform inventory and marketing decisions

## 💡 Key Insights Discovered

### Revenue & Growth Dynamics
- **Total Revenue: $8.30M** across 397.9K transactions from 4.4K customers
- **Average Order Value: $448** indicating premium product positioning
- **14% Growth Rate** demonstrates healthy business expansion
- **Q4 Revenue Surge**: November and December showed significant seasonal spikes, suggesting strong holiday performance optimization opportunities

### Geographic Performance
- **United Kingdom dominates** with the highest revenue contribution across all quarters
- **Netherlands leads** in average revenue per country (€100+ average), indicating high-value market segment
- **Germany, France, and EIRE** show consistent mid-tier performance with growth potential
- **Emerging markets**: Spain, Belgium, Switzerland represent untapped expansion opportunities

### Customer Intelligence
- **Average Basket Size: 265 units** suggests bulk/wholesale purchasing behavior
- **Customer Lifetime Value: $1,900** provides clear CAC benchmarks for marketing ROI
- **Top customer concentration**: Customer #14646 generated $279K (3.4% of total revenue), indicating B2B relationships
- **Peak acquisition months**: November (1.9K new customers) aligns with seasonal campaigns
- **High-frequency buyers**: Customer #17841 made 8K purchases, revealing loyalty program opportunities

### Product Strategy
- **Top 5 SKUs** drive 18% of total revenue, indicating product portfolio optimization needs
- **"REGENCY CAKESTAND"** leads at $133K, followed by **"WHITE HANGING HEART"** at $94K
- **Postage revenue** ($67K) suggests shipping cost recovery or premium delivery services
- **Decorative/seasonal items** dominate top 15, confirming gift and home décor market positioning

## 🛠️ Technical Architecture

### Tools & Technologies
- **Power BI Desktop**: Primary business intelligence and data visualization platform
- **DAX (Data Analysis Expressions)**: Custom measures for growth rate, CLV, and basket size calculations
- **Data Modeling**: Star schema implementation for optimized query performance
- **Interactive Filtering**: Country and Product slicers for dynamic analysis across dimensions

### Data Processing Pipeline
- **Data Source**: Transactional database with 397.9K+ records
- **ETL Operations**: Data cleaning, transformation, and aggregation of customer and product dimensions
- **Calculated Metrics**: 
  - Average Order Value = Total Revenue / Total Transactions
  - Growth Rate = ((Current Period - Previous Period) / Previous Period) × 100
  - Customer Lifetime Value = Total Revenue / Total Unique Customers
  - Basket Size = Total Quantity / Total Transactions

### Dashboard Design Philosophy
- **Dual-dashboard approach**: Sales Overview + Customer Analysis for role-specific insights
- **KPI Cards**: Immediate visibility of critical business metrics at dashboard load
- **Comparative visualizations**: Quarter-over-quarter and country-wise performance tracking
- **Top-N analysis**: Focus on highest-impact products and customers for strategic prioritization



### Technical Challenges Overcome
- **Data quality issues**: Handled missing customer IDs and standardized country naming conventions
- **Performance optimization**: Implemented aggregated tables to handle 397K+ row dataset with sub-second load times
- **Cross-filtering complexity**: Managed bidirectional relationships between customer and product dimensions without circular dependencies
- **Scalability design**: Built modular data model supporting future integration of returns, costs, and profitability metrics

## 🚀 Future Enhancements

- **Predictive analytics**: ARIMA/Prophet models for revenue forecasting
- **Cohort analysis**: Customer retention and churn prediction using Python/R integration
- **Real-time streaming**: Power BI streaming datasets for live transaction monitoring
- **Profitability layer**: Cost data integration for margin analysis by product and customer segment

## 💼 Why This Matters

**For Business Leaders**: This dashboard transforms reactive reporting into proactive strategy by surfacing hidden patterns in customer behavior, geographic performance, and product demand.

**For Technical Teams**: Demonstrates proficiency in modern BI tools, data modeling best practices, and the ability to translate complex datasets into intuitive, performant visualizations.

## 🤝 Let's Connect

I'm passionate about turning data into decisions. Whether you're looking to:
- **Build similar analytics capabilities** for your organization
- **Discuss data visualization best practices** and dashboard design patterns
- **Explore collaboration opportunities** in business intelligence and analytics

**📫 I'd love to hear from you!** Open to feedback, questions, or opportunities to solve complex data challenges together.

---

⭐ **Star this repository** if you found these insights valuable!

🔗 **Connect with me** to discuss analytics, data visualization, or business intelligence strategies.

## 🔍 Deep-Dive: Methodology

### Data Exploration & Cleaning
**Challenge**: Raw dataset contained 400K+ transactions with inconsistent formatting and missing values.

**Approach**:
- Implemented **Python pandas** for initial data profiling and quality assessment
- Identified and resolved **3.2% missing CustomerIDs** using transaction pattern matching
- Standardized **country names** (e.g., "UK" → "United Kingdom", "Eire" → "EIRE")
- Removed **duplicate transactions** and test records (< 0.5% of dataset)
- Validated **data integrity** with cross-checks between revenue sums and transaction counts

---

## 🖼️ Dashboard Preview

### Sales Overview Dashboard
![Sales Dashboard_pages-to-jpg-0001](https://github.com/user-attachments/assets/32a53a38-84d5-4c37-93a5-ba030e7901e5)

*Interactive dashboard showing revenue trends, top-performing countries, quarterly performance, and product analysis*

### Customer Analysis Dashboard
![Sales Dashboard_pages-to-jpg-0002](https://github.com/user-attachments/assets/63440416-35d7-4cd1-97eb-614f94f2e125)

*Comprehensive customer insights including lifetime value, purchase frequency, and geographic distribution*

---

### Data Processing Pipeline
- Data Source: Transactional database with 397.9K+ records
- ETL Operations:
  - Data cleaning, transformation, and aggregation of customer and product dimensions
  - Handled missing customer IDs and standardized country naming conventions
  - Removed duplicates and test records; validated integrity with revenue/transaction cross-checks

### Calculated Metrics (DAX)
- Average Order Value = Total Revenue / Total Transactions
- Growth Rate = ((Current Period − Previous Period) / Previous Period)
- Customer Lifetime Value = Total Revenue / Total Unique Customers
- Basket Size = Total Quantity / Total Transactions

### Advanced DAX Calculations
~~~DAX
-- Core Measures
Total Revenue =
SUM ( Sales[Revenue] )

Total Transactions =
DISTINCTCOUNT ( Sales[InvoiceNo] )

Total Customers =
DISTINCTCOUNT ( Sales[CustomerID] )

Total Quantity =
SUM ( Sales[Quantity] )

Average Order Value =
DIVIDE ( [Total Revenue], [Total Transactions], 0 )

Avg Basket Size =
DIVIDE ( [Total Quantity], [Total Transactions], 0 )

Avg Customer Lifetime Value =
DIVIDE ( [Total Revenue], [Total Customers], 0 )

-- Growth Rate (MoM %)
Growth Rate % =
VAR CurrentRevenue =
    [Total Revenue]
VAR PreviousRevenue =
    CALCULATE ( [Total Revenue], DATEADD ( 'Calendar'[Date], -1, MONTH ) )
RETURN
DIVIDE ( CurrentRevenue - PreviousRevenue, PreviousRevenue )

-- Quarter-over-Quarter Revenue Change (%)
QoQ Revenue Change % =
VAR CurrentQtr = [Total Revenue]
VAR PreviousQtr =
    CALCULATE ( [Total Revenue], PREVIOUSQUARTER ( 'Calendar'[Date] ) )
RETURN
DIVIDE ( CurrentQtr - PreviousQtr, PreviousQtr )
~~~

### Performance Optimization Techniques
1. Aggregated Tables
   - Created summary tables for month/quarter aggregations  
   - Result: Reduced query time by 73%
2. Star Schema Implementation
   - Proper fact-dimension relationships for optimal filtering  
   - Minimized cross-filtering complexity
3. Calculated Columns vs Measures
   - Strategic use of measures for dynamic calculations  
   - Minimized model size and improved refresh performance
4. Database Indexing
   - Applied indexes on CustomerID, Country, and Date fields  
   - Improved data retrieval speed significantly
5. Incremental Refresh Configuration
   - Configured for handling future data growth  
   - Eliminated need for full data reloads

---

## 📊 Dashboard Features Breakdown

### Sales Overview Dashboard
| Visual Element        | Business Question Answered       | Technical Implementation                 |
|----------------------|-----------------------------------|------------------------------------------|
| KPI Cards            | Current performance baseline?     | Dynamic measures with conditional formatting |
| Revenue by Month     | Seasonal patterns?                | Line chart with trend analysis           |
| Top 5 Countries      | Which markets drive value?        | Horizontal bar chart sorted by average revenue |
| Quarterly Trends     | Performance across quarters?      | Stacked column chart with country breakdown |
| Top Products         | Which SKUs deserve investment?    | Top N filtering with dynamic ranking     |

### Customer Analysis Dashboard
| Visual Element            | Insight Generated              | Key Metric                     |
|--------------------------|--------------------------------|--------------------------------|
| Customer Count by Country| Geographic distribution        | Germany leads with 100+ customers |
| Monthly Acquisition      | Customer growth trajectory     | Peak: 1.9K in November         |
| Top 15 Customers         | Revenue concentration and B2B  | Top customer: $279K (3.4% of total) |
| Purchase Frequency       | Loyalty and repeat patterns    | Highest: 8K purchases          |
| Lifetime Value           | Long-term profitability        | Average: $1,900 per customer   |

---

## 🔍 Methodology Deep-Dive

### Data Exploration & Cleaning
- Implemented Python pandas for initial data profiling and quality assessment
- Identified and resolved 3.2% missing CustomerIDs using transaction pattern matching
- Standardized country names (e.g., “UK” → “United Kingdom”, “Eire” → “EIRE”)
- Removed duplicate transactions and test records (< 0.5% of dataset)
- Validated data integrity via reconciliation of revenue sums and transaction counts

---

## 📈 Business Impact & Outcomes

### Measurable Results
- Reduced reporting time by 85%: Automated dashboards replaced manual weekly Excel reports
- Identified $279K customer: Enabled account management team to provide white-glove service
- Discovered geographic opportunity: Netherlands’ high AOV (€100+) justified market expansion investment
- Seasonal forecasting accuracy: November spike pattern enables proactive inventory planning

### Technical Challenges Overcome
- Data quality issues: Handled missing customer IDs and standardized country naming conventions
- Performance optimization: Implemented aggregated tables to handle 397K+ rows with sub-second load times
- Cross-filtering complexity: Managed bidirectional relationships between customer and product dimensions
- Scalability design: Built modular data model supporting future integration of returns and profitability metrics

---

## 🎓 Skills Demonstrated

### Business Intelligence
- Requirement gathering and stakeholder alignment
- KPI definition and metric selection
- Dashboard design and UX best practices
- Data storytelling and executive communication
- Business domain understanding (e-commerce/retail)

### Data Analysis
- Exploratory data analysis (EDA)
- Statistical analysis and trend identification
- Cohort and segmentation analysis
- Customer behavior analytics
- Product performance optimization

### Technical Expertise
- Power BI Desktop (advanced)
- DAX formula language
- Data modeling (star schema, snowflake)
- SQL query optimization
- Python for data processing (pandas, numpy)
- ETL pipeline development
- Version control (Git)

---

## 🚀 Future Enhancements
- Predictive Analytics: ARIMA/Prophet models for revenue forecasting
- Cohort Analysis: Customer retention and churn prediction using Python/R integration
- Real-time Streaming: Power BI streaming datasets for live transaction monitoring
- Profitability Layer: Cost data integration for margin analysis by product and customer segment

---

## 💼 Why This Matters
- For Business Leaders: Transforms reactive reporting into proactive strategy by surfacing hidden patterns in customer behavior, geographic performance, and product demand.
- For Technical Teams: Demonstrates proficiency in modern BI tools, data modeling best practices, and translating complex datasets into intuitive, performant visualizations.

---

## 🤝 Let’s Connect
I’m passionate about turning data into decisions. Whether you’re looking to:
- Build similar analytics capabilities for your organization
- Discuss data visualization best practices and dashboard design patterns
- Explore collaboration opportunities in business intelligence and analytics

Open to feedback, questions, or opportunities to solve complex data challenges together.
