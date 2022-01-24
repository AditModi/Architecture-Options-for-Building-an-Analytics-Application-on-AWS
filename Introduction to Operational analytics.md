* Operational analytics refers to inter-disciplinary techniques and methodologies that aim to improve day-to-day business performance in terms of increasing efficiency of internal business processes and improving customer experience and value. 

* Business analysts used the traditional analytics systems to recognize the business trends and identify the decisions. But by using the operational analytics systems, they can initiate such business actions based on the recommendations that the systems provide. They can also automate the execution processes to reduce the human errors. This makes the system go beyond being descriptive to being more prescriptive and even being predictive in nature.

* Enterprises often have diverse and complex IT infrastructure. Challenges arise when trying to identify sources to extract from or identify what operational data captures the state of an analytics application. 

* Traditionally this data came from logging information emanating from different parts of the system. Modern environments include trace and metric data along with log data. Trace data captures the user request for resources as it passes through different systems all the way to the destination and the response back to the user. 

* Metric data contain various measurements that provide insight into the health or operational state of these systems. The combination of these form a rich set of diverse operational data that analytics application can be built on.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vy7x097z2ipn01axpy0g.png) 

> **Architecture Options for Building an Analytics Application on AWS** is a Series containing different articles that cover the key scenarios that are common in many analytics applications and how they influence the design and architecture of your analytics environment in AWS. These series present the assumptions made for each of these scenarios, the common drivers for the design, and a reference architecture for how these scenarios should be implemented.

* Operational analytics is the process of using data analysis and business intelligence to improve efficiency and streamline everyday operations in real time.

* A subset of business analytics, operational analytics is supported by data mining, artificial intelligence, and machine learning. It requires a robust team of business and data analysts. 

# Characteristics

* **Discoverability**: The ability of the system to make operational data available for consumption. This involves discovering multiple disparate types of data available within an application that can be used for various ad hoc explorations.

* **Observability**: The ability to understand internal state from the various signal outputs in the system. By providing a holistic view of these various signals along with a meaningful inference it becomes easy understand how healthy and well performant the overall system is.

* **User centricity**: Each analytics application should address a well-defined operational scope and solve a particular problem at hand. Users of the system often won’t understand or care about the analytics process but only see the value the result.

* **Agility**: The system must be flexible enough to accommodate changing needs of an analytics application and offer necessary control to bring in additional data with low overhead.

# Reference architecture

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/f3cfyqfmz2nkq83a5hxf.png)
*Operational analytics reference architecture*

* **Operational data**: Operational data originates from various points in the environment and systems. It consists of log data including systems logs, machine logs, applications logs, events logs, audit and other logs; metric data systems metrics, resource utilization metrics, application performance metrics; trace data including request-response profile and other telemetric data.

* **Transformation and ingestion**: This represents a layer that collects the operational data and performs additional dissection or enrichment or other transformation before being ingested into Amazon OpenSearch Service. These include decoration data from additional sources or transforming the data into form required for indexing.

* **Indexing**: OpenSearch Service performs indexing of incoming transformed data and makes it available for near-real time searching.

* **Visualization**: This layer brings in all the operational data present in the system into a single pane of glass in the forms of graphs, visualization, and other dashboards for the particular analytics application.

* **Downstream application**: OpenSearch Service also allows operational data indexed to be available for machine learning, alerting, and reporting application. 

# Configuration notes

* **Choose data model before ingestion**: When bringing data in from disparate sources, especially from structured systems into structureless systems such as OpenSearch, special care must be taken to ensure that the chosen data model provides a frictionless search experience for users.

* **Decide what data fields will be searchable**: By default, Amazon OpenSearch Service indexes all data fields. This might not be desirable in situations like fully or partially matching on numeric data types.

* **Use tiered storage**: The value of operational data or any timestamped data generally decreases with the age of the data. Moving aged data into tiered storage can save significant operational cost. Summarized rollups that can condense the data also can help address storage cost.

* **Monitor all involved components**: Monitor all involved components with metrics in Amazon CloudWatch.

---

Hope this guide gives you an Introduction to Operational Analytics, explains the Characteristics and Reference Architecture for Operational Analytics.

Let me know your thoughts in the comment section 👇
And if you haven't yet, make sure to follow me on below handles:

👋 **connect with me on [LinkedIn](https://www.linkedin.com/in/adit-modi-2a4362191/)**
🤓 **connect with me on [Twitter](https://twitter.com/adi_12_modi)**
🐱‍💻 **follow me on [github](https://github.com/AditModi)**
✍️ **Do Checkout [my blogs](https://aditmodi.hashnode.dev)** 

Like, share and follow me 🚀 for more content.

---

[Reference Guide](https://docs.aws.amazon.com/wellarchitected/latest/analytics-lens/operational-analytics.html)