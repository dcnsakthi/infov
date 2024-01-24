Joining a table with round-robin distribution and hash distribution in Azure Synapse Analytics can utilize more memory due to the way data is distributed and the operations required to perform the join¹²³⁴⁵.

In a **round-robin distributed table**, rows are distributed evenly across all distributions, but the assignment of rows to distributions is random¹. Unlike hash-distributed tables, rows with equal values are not guaranteed to be assigned to the same distribution¹. As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query¹. This extra step can slow down your queries¹.

On the other hand, a **hash-distributed table** distributes table rows across the compute nodes by using a deterministic hash function to assign each row to one distribution¹. Since identical values always hash to the same distribution, Azure Synapse Analytics has built-in knowledge of the row locations¹. This knowledge is used to minimize data movement during queries, which improves query performance¹.

When you join a round-robin distributed table and a hash-distributed table, the system may need to reshuffle the data in the round-robin table to match the distribution of the hash-distributed table²³⁴⁵. This reshuffling operation, also known as data movement, can be resource-intensive and can consume a significant amount of memory²³⁴⁵.

Therefore, it's recommended to carefully choose the distribution type based on your workload and query patterns to minimize data movement and improve query performance¹²³⁴⁵.

Source: Conversation with Bing, 24/01/2024
(1) Distributed tables design guidance - Azure Synapse Analytics. https://learn.microsoft.com/en-us/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-distribute.
(2) How to minimize data movements (Compatible and Incompatible Joins). https://techcommunity.microsoft.com/t5/azure-synapse-analytics-blog/how-to-minimize-data-movements-compatible-and-incompatible-joins/ba-p/1807104.
(3) Distributions In Azure Synapse Analytics - C# Corner. https://www.c-sharpcorner.com/article/distributions-in-azure-synapse-analytics/.
(4) How to choose Right data distribution strategy for Azure Synapse .... https://rajanieshkaushikk.com/2020/09/09/how-to-choose-right-data-distribution-strategy-for-azure-synapse/.
(5) Strategy for Selecting Data Distribution in Azure Cloud Platform. https://medium.com/@jwbtmf/strategy-for-selecting-data-distribution-in-azure-cloud-platform-d34045fe172d.
