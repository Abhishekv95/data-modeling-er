Investment Portfolio Analysis System. This system will manage portfolios, investments, asset classes, performance indicators, benchmarks, and financial metrics, providing a structure for tracking and analyzing investment performance.

Main Entities and Relationships
User

Attributes: user_id (PK), username, password_hash, email, account_type (admin/investor), created_at, updated_at
Relationships:
Has many Portfolios
Portfolio

Attributes: portfolio_id (PK), user_id (FK), name, creation_date, total_value, risk_profile, updated_at
Relationships:
Belongs to User
Has many Investments
Has many PerformanceMetrics
Associated with Benchmarks
Investment

Attributes: investment_id (PK), portfolio_id (FK), asset_id (FK), quantity, purchase_price, current_value, purchase_date, updated_at
Relationships:
Belongs to Portfolio
Refers to Asset
Asset

Attributes: asset_id (PK), ticker_symbol, asset_name, asset_class_id (FK), market_price, currency, exchange, created_at, updated_at
Relationships:
Belongs to AssetClass
Has many Investments
Has associated PerformanceIndicators
AssetClass

Attributes: asset_class_id (PK), name (e.g., equity, bond, commodity), description, risk_level
Relationships:
Has many Assets
PerformanceMetric

Attributes: performance_metric_id (PK), portfolio_id (FK), metric_name (e.g., ROI, Sharpe Ratio), value, calculation_date
Relationships:
Belongs to Portfolio
PerformanceIndicator

Attributes: indicator_id (PK), asset_id (FK), indicator_name (e.g., 1-year return, volatility), value, calculation_date
Relationships:
Belongs to Asset
Benchmark

Attributes: benchmark_id (PK), name, index_type (e.g., S&P 500), description, created_at
Relationships:
Has many BenchmarkValues
Can be associated with multiple Portfolios
BenchmarkValue

Attributes: benchmark_value_id (PK), benchmark_id (FK), date, value
Relationships:
Belongs to Benchmark
FinancialMetric

Attributes: financial_metric_id (PK), portfolio_id (FK), metric_name (e.g., net worth, debt ratio), value, as_of_date
Relationships:
Belongs to Portfolio
ER Diagram Design Notes
Portfolios and Investments: Each portfolio can hold multiple investments across various asset classes, and each investment is tracked for value changes.
Asset Class and Performance Indicators: Assets belong to an asset class (e.g., stocks, bonds) and have associated performance indicators for detailed analysis.
Performance Metrics: Portfolios track multiple performance metrics, allowing for insights into risk, return, and efficiency.
Benchmarks: Benchmarks allow comparison with relevant indices, enhancing performance analysis.
Financial Metrics: Each portfolio has associated financial metrics to track aspects such as debt and overall portfolio worth.
