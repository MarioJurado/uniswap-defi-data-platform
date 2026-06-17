# Uniswap DeFi Data Platform
## Introdution
This project provides a data architecture designed to extract and analyze Uniswap data, offering a tool for DeFi enthusiasts who want a deeper understanding of what's happening on-chain.

I've always been interested in DeFi and how the vast amount of data is handled behind the scenes, since the UX rarely shows the full picture. So I decided to build something on my own, while practicing my data engineering skills along the way.

This project is just a Proof of Concept. It took me around 3-4 months, working on it in my free time outside my full-time job as a Data Engineer.

This documentation is meant to provide context for non-technical readers as well, so it's not a deep technical reference, even though I'll go into detail on some parts.

I hope you enjoy it, and feel free to suggest improvements, fork it, or contribute if you'd like.  
Thank you.

---
## Project overview
This section covers the scope, technologies used, high-level architecture of the platform and some other topics related to the decision-making behind the project.

#### · Scope
As a Proof of Concept, the scope of this project was to build an end-to-end data platform extracting data only from Uniswap version 3 (rather than version 2) and only from the Ethereum mainnet, for these reasons:
- Version 3 introduced a key feature that makes it especially interesting: Concentrated Liquidity.
- Ethereum mainnet is where most of the value is locked, so I decided to leave other chains out of scope for now.

Additionally, the scope is limited to analyzing everything related to the existing liquidity within a pool. This includes tokens, swaps between them, ticks, liquidity events such as mints and burns, and liquidity providers data (the owners of the liquidity within a pool). Everything else is excluded.

#### · Tech stack
These are the main technologies I used to develop the project: 

- **Databricks Free Edition** as the development platform
- **Uniswap V3 Subgraph** (via The Graph) as the main data source
- **PySpark** and **SparkSQL** as the primary languages
- **GraphQL** to query the Subgraph API
- **Delta Lake** to store all tables
- **Unity Catalog** to govern and manage them

#### · Architecture diagram

![](docs/images/Uniswap_architecture.png)

#### · Diagram walkthrough
The orchestration starts with a Databricks Job triggered twice a week, which runs the Main Orchestrator. This component sets up the environment and determines which layers need to be executed. It then triggers the Layer Orchestrator, which runs each layer sequentially: Bronze, Silver, and finally Gold. Once the Gold layer is ready, the data can be explored through the Dashboard.

#### · Load strategy, compute and partitioning
**Loads:** To bring some context, The Graph's Free Plan provides 100,000 free queries, so I decided to run the pipeline twice a week. This meant I couldn't retrieve all the data on every run, so incremental loads were the only viable option for the Bronze layer entities, retrieving only new rows and appending them to the existing ones, building the full history over time. The platform already provides differential loads using a sort of primary key to identify rows, which are then merged with the existing data.

For the Silver and Gold layers, all existing data is reprocessed on every run, since the size of the Bronze layer entities isn't large enough to make a meaningful difference between a full load and a differential one.

I'd like to highlight that for some entities, such as Swaps, I had to prune the extraction by filtering only swaps from relevant pools (selecting only those with decent amount of total value locked, a minimum number of swaps, and so on) to avoid overloading the query threshold. This is tackled below.

**Compute:** Databricks Free Edition only supports Serverless compute, so I wasn't able to deploy a cluster to optimize the processing workloads. 

**Partitioning:** There was no need to partition any table, since, again, the size of the tables was small enough to be handled efficiently by Delta Lake. As an example, the Swaps table is around ~5GB. The actual bottleneck was the number of API queries, not the storage layer. Databricks recommends not partitioning tables smaller than 500GB, so there's still a long way to go before that becomes a concern.

---
## Medallion architecture explanation
#### · Orchestration
#### · Bronze
#### · Silver
#### · Gold
---
## Uniswap Data Model
#### · Factory
#### · Pools
#### · Tokens
#### · Ticks
#### · Swaps
#### · Positions
#### · Mints
#### · Burns
---
## Dashboard showcase
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
## How to run it
xxxxxxxx

---
## Challenges and learnings
xxxxxxxxxxxx

---
## Future improvements
This PoC was designed to cover only Uniswap V3 data on the Ethereum chain, and as explained above, it runs as an incremental batch load twice a week.

The next steps on the roadmap would be implementing the other Uniswap protocol versions (mainly V2 and V4) and extracting data from other chains as well.

Additionally, I'd like to deploy a version using Lakeflow Spark Declarative Pipelines to make it near real-time, providing more accurate analysis.

---
## Contact me 
Either you liked my project, you want to ask anything, contribute or anything else, you can reach me out at:  
mariojuradogalan@outlook.com  
or via LinkedIn:  
[LinkedIn profile](https://www.linkedin.com/in/mariojuradogalan/)






