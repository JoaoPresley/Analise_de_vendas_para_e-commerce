# AI Copilot Instructions for Analise de Vendas para E-commerce

## Project Overview
This is a Jupyter notebook-based exploratory data analysis (EDA) project analyzing e-commerce sales data. The single entry point is `main.ipynb`, which generates synthetic sales data and performs statistical analysis using pandas, numpy, matplotlib, and seaborn.

## Architecture & Data Flow

### Core Data Pipeline
1. **Data Generation** (`main.ipynb` - cell 6, `dsa_gera_dados_ficticios()`)
   - Function generates synthetic sales records with nested product metadata (category, price)
   - Returns pandas DataFrame with schema: ID_Pedido, Data_Pedido, Nome_Produto, Categoria, Preco_Unitario, Quantidade, ID_Cliente, Cidade, Estado
   - Simulates Brazilian e-commerce for 7 major cities with 8 product SKUs across 4 categories

2. **Data Exploration** (cell 8)
   - DataFrame stored in kernel variable `df_vendas` (500 records by default)
   - Subsequent cells leverage this shared state for analysis

### Key Data Characteristics
- **Temporal**: Orders span from Jan 1, 2026 with ~5-day clustering (i/5 pattern in date generation)
- **Geographic**: Brazil-specific with state abbreviations (SP, RJ, MG, etc.)
- **Pricing Variation**: Mouse and Teclado products have dynamic 10% discount random application
- **Product Categories**: Eletrônicos, Acessórios, Hardware, Móveis (discrete classification)

## Development Workflow

### Environment Setup
- Python data science stack: pandas, numpy, matplotlib, seaborn
- Watermark library for versioning annotations (`%watermark` magic commands)
- `%matplotlib inline` for notebook-native visualization

### Notebook Execution Convention
- **Cell 1**: Install/update watermark
- **Cells 2-4**: Import libraries and display environment metadata
- **Cell 5**: Markdown section header (do not execute)
- **Cell 6**: Define `dsa_gera_dados_ficticios()` function - **must execute before cell 8**
- **Cell 7**: Markdown section header
- **Cell 8**: Generate and assign `df_vendas` - **entry point for analysis cells**
- **Cell 9**: Empty/scratch cell for user exploration

**Critical**: Ensure cell 6 executes before any analysis that depends on `df_vendas` (cell 8+).

## Project-Specific Patterns

### Function Naming Convention
- Prefix functions with `dsa_` (Data Science Academy convention from original curriculum)
- Example: `dsa_gera_dados_ficticios()` for data generation
- Follow this convention when extending analysis functions

### DataFrame Column Naming
- Snake_case with Portuguese names reflecting business domain
- Examples: `Nome_Produto`, `Preco_Unitario`, `Data_Pedido`, `ID_Cliente`
- Maintain Portuguese naming for consistency with existing codebase

### Visualization Style
- Use seaborn for statistical plots
- Apply `%matplotlib inline` for display in notebook
- Store figures or include plot configuration in analysis cells

## Common Extensions & Patterns

When expanding analysis:
1. **Add analysis cells after cell 8** that reference `df_vendas`
2. **Aggregation pattern**: Use `df_vendas.groupby(['Categoria', 'Estado']).agg({'Preco_Unitario': 'mean', 'Quantidade': 'sum'})`
3. **Temporal analysis**: Leverage `Data_Pedido` (datetime) for time-series grouping
4. **Regional insights**: Filter by `Estado` or aggregate by city using `Cidade` column
5. **Product performance**: Compare metrics across 8 product SKUs using `Nome_Produto`

## Key Files & Their Roles
- `main.ipynb`: Single source of truth for analysis code and documentation
- `README.md`: High-level project description
- `LICENSE`: Project licensing (preserved during development)

## Dependencies & Tools
- **pandas**: DataFrame manipulation and aggregation
- **numpy**: Numerical operations (random, integer generation)
- **matplotlib/seaborn**: Data visualization
- **datetime**: Temporal data handling
- **random**: Synthetic data randomization

No external data files required - all data is generated in-memory.
