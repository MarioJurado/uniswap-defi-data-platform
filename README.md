# Uniswap DeFi Data Platform
### Introdution
This project provides a data architecture designed to extract and analyze Uniswap data, offering a tool for DeFi enthusiasts who want a deeper understanding of what's happening on-chain.

I've always been interested in DeFi and how the vast amount of data is handled behind the scenes, since the UX rarely shows the full picture. So I decided to build something on my own, while practicing my data engineering skills along the way.

This project is just a Proof of Concept. It took me around 3-4 months, working on it in my free time outside my full-time job as a Data Engineer.

This documentation is meant to provide context for non-technical readers as well, so it's not a deep technical reference, even though I'll go into detail on some parts.

I hope you enjoy it, and feel free to suggest improvements, fork it, or contribute if you'd like.  
Thank you.

---
### Project overview (why incremental batches, tech stack, job yaml, Excalidraw architecture)
![](docs/images/Uniswap_architecture.png)

### Medallion architecture explanation (layers, medatada orchestration)
#### · Orchestration
#### · Bronze
#### · Silver
#### · Gold
---
### Uniswap Data Model
#### · Factory
#### · Pools
#### · Tokens
#### · Ticks
#### · Swaps
#### · Positions
#### · Mints
#### · Burns
---
### Dashboard showcase
#### Access URL
**[Uniswap_DeFi_Dashboard](https://dbc-d5e8e1ea-6197.cloud.databricks.com/dashboardsv3/01f1511eafc51536930b59045bada187/published?o=2923669840284238)**

#### Liquidity Events
![](docs/images/Liqudity_Events_page.png)

#### Liquidity Providers
![](docs/images/Liquidity_Providers_page.png)

#### Pools
![](docs/images/Pools_page.png)

#### Swaps
![](docs/images/Swaps_page.png)

#### Tokens
![](docs/images/Tokens_page.png)
---
### How to run it

---
### Challenges and learnings

---
### Future improvements
This PoC was designed to cover only Uniswap V3 data on the Ethereum chain, and as explained above, it runs as an incremental batch load twice a week.

The next steps on the roadmap would be implementing the other Uniswap protocol versions (mainly V2 and V4) and extracting data from other chains as well.

Additionally, I'd like to deploy a version using Lakeflow Spark Declarative Pipelines to make it near real-time, providing more accurate analysis.

---
### Contact me 
Reach me out at:  
mariojuradogalan@outlook.com  
or via LinkedIn:  
[LinkedIn profile](https://www.linkedin.com/in/mariojuradogalan/)






