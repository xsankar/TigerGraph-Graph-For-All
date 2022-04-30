#  Graph For A Better Token Economy
**Contributors and Contact Information: [Krishna sankar @ksankar ]**

## Problem Statement 
* Virtual Assets (Crypto coins, NFTs, ...) enable under represented population
* ... But the platforms are not as secure as they need to be. There should be a better way to enable the masses and usher the new improved kinder-gentler Web 3.0 & crypto currency platform

[Link to YouTube video](https://youtu.be/1v9GJOV_pag)

## Description
* Immutable, Distributed, Unanimous & Secure DLT & Blockchain stack for Crypto currency & Web 3.0. While the other properties are well implemented, security is still a challenge
* Specifically, this project addresses the detection of Fraud Rings (e.g., Money Laundering) & Camouflaged Fraud (e.g., Fake Product Reviews)
* We will need a graph substrate as an important component of the Web 3.0 platform; definitely for the crypto currency stack.

## Approach
* Tackle one of the complex fraud pattern in a scalable, extensible way

## Challenges
* Payment network is very different from social or other networks
 * Temporal, monotonic time
 * Not symmetric
 * Other attributes (like amount) matters
 * Many of the concepts like connected components and page rank do not mean much
* Money Laundering Layering is not just one cycle
 * But multiple ordered cycles with a fraud actor at the helm
* Detecting fraud ring is literally finding the proverbial needle in a haystack
 * Class imbalance, Long Fraud Chains

## Approach a.k.a How we built it
1. Layered approach with well defined pipeline stages
 * Overlay fraud rings progressively
 * Narrow down and organize the vertices as we progress
 * Always keep time sequencing in the processing
2. Customize relevant gsql graph algorithms
 * e.g., Rocha-Thatte Cycle Detection, but it is unordered 
 * Also need to combine cycles and find the fraud actor at the helm
3. Add runtime attributes to vertices
 * That will help the processing downstream the pipeline
4, Start with a simple schema and add more elements as required
5. Stay in TigerGraph as much as possible (more later)

## Accomplishments that we're proud of
* Constructing multi-cycle fraud ring using graph algorithms
* The possibilities the platform provides - and we have a lot more ideas !

## What we learned
1. Graph representation is appropriate for DLT/Blockchain Fraud Detection
 * TigerGraph is a feature rich, flexible & scalable Graph Database well suited for this problem
 * But it requires disciplined thinking,  at times different than what we are used to  ! 
2. Spend time thinking about & understanding the problem
3. Make simplified assumptions and relax them as you progress (Layered approach)
4. Think Graphs & more specifically Parallel Graphs ? It will take a little time to get used to that concept
 * Read, write & learn the patterns from the GSQL Graph Algorithms  and the GSQL code
5. Draw graph diagrams to visualize the problem - Draw the happy path 1st & then edge cases
6. Create datasets depicting multiple scenarios ? 1st use a small dataset to test the algorithms
7. Do as much in TigerGraph as possible, staying true to the platform
 * It is tempting to process a list outside (say in python), after a quick GSQL algorithm; don?t stop there, persist (using GSQL) until you have exhausted all graph ideas

## What's next for Graph For A Better Token Economy 
### This is only the beginning !
1. Scale ! Load Bitcoin/Ethereum blockchains and apply the algorithms
 * Cross-Ledger tracking of fraud rings 
2. Fine grained temporals
 * There could be many such rings by the same actors, so need to separate the rings by time
  * solution : time tree ?If you need to filter use vertices? ? TigerGraph pragma
 * Opportunity for Payment Networks in TigerGraph Graph Algorithms
3. More expressive Graph schema with derived runtime attributes, especially to track cross-ledger behaviors
4. Explore Graph Motif extraction, Weighted Graphs
5. Graph Neural Networks leveraging the extended dynamic attributes
6. Entity Resolution
 * Need to understand heavy spans & differentiate between Exchanges, Tumblers, Mixers - Add Vertex type based customized logic
 * Probably via highest measure of eigenvalue centrality

## Thanks for the opportunity, Enjoyed the journey a lot !!

## Details
 - **Data**: We used a test dataset to develop the project. We are working on applying the method to the bitcoin data
 - **Technology Stack**: For now pure TigerGraph. For GNN we will use python and Jupyter notebooks

## Installation

This project can be run fully in TigerGraph environment via the GraphStudio
1. Clone repository
7. Read through the file TG_Graph_For_All.pdf
   * It has the problem, sample fraud ring graphs and other details
2. Either import the .tar.gz file or create everything from scratch
2. Use the "Import An Existing Solution" in graph Studio to import the export_054284246.tar.gz
   1. Select the Tumbler 
   1. Go To Write Queries
   1. Run the query "ordered-payment-cycle"
   1. Check the visualization - Select the "tree" visualization type on the right hand bottom
   1. Inspect the JSON by selecting the {}
2. Only do the following if you want to create from scratch
2. Create Schema - Details are in the TG_Graph_For_All.pdf Page 8 and 9.
3. Map the Data - data file transactions.csv
   1. Only the account vertex and the send edge need to be mapped and loaded. Rest of the vertices and edges are for the future
4. Load the data - data file transactions.csv
5. Copy the two GSQL in Edit Queries
   * ordered_payment_cycle.gsql
   * rt_cycle.GSQL - This the modified Rocha-Thatte cycle algorithm from GSQL Graph Algorithms
6. Run the query ordered-payment-cycle
   * The files ops_02_output.txt and ops_02_detailed_output.txt show a sample output to check
   * Also check the output with the graph in Page 4 of TG_Graph_For_All.pdf. TigerGraph finds all rings and orders them nicely !
 
