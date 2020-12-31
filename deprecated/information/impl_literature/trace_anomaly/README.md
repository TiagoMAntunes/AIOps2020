# Paper Notes
Thoughts / Summaries of Relevant Papers

#### Root Cause Detection in a Service-Oriented Architecture
##### Approach
- Ranking of possible root causes
- Uses unsupervised model on
    - Historical time-series metrics
    - Current time-series metrics
    - Call graph 
- Features
    - Random walk over call graph
    - Clustering to detect candidate anomalies
    - Metric similarity to counteract external factors

##### Call Graph Issues 
- Might not represent true dependencies
- Does not account for external factors
- How do we handle serial and parallel calls?
>For example, call latency for a service would be greater than the sum of its downstream calling service’s latency for serial calls, but be maximum in case of parallel calls.
- Dependencies change over time

##### System Subcomponents
MonitorRank consists of three different components
###### Metrics Collection 
- Consumes Kafka data
- Buffers and aggregates to coarser time granularity (every 1 min)
- Stores into time-partitioned database

###### Batch-Mode Engine 
- Generates call graph with a HADOOP job
- Clusters sensors together based on historical correlation
>Then for every pseudo-anomaly we need to compute the similarity of the corresponding metric data against those of all the other sensors. 
- Does some shit with similarity

###### Real-time Engine 


#### Latent Error Prediction and Fault Localization for Microservice Applications by Learning from System Trace Logs
###### Approach (RIP)
>To train the models, we need not only trace logs under successful executions but also trace logs under erroneous executions. 

#### Anomaly Detection from System Tracing Data using Multimodal Deep Learning

###### Feasibility
- Definitely applicable to our project
- Would surrender parent / child information of calls

###### Approach
One model for structure, one for response time
- LSTM with softmax to predict probabilities for next label in trace (meant to learn underlying execution paths)
- LSTM regression on response time for next event (msle)

Merges both modalities on the first LSTM layer

#### Anomaly Detection and Classification using Distributed Tracing and Deep Learning

###### Approach
- RRN (VAE) with GRU cells for response time prediction
- Hamming smoothing filter for noise removal / reduction