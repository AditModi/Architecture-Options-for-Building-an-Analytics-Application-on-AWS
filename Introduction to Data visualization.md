Every day, the people in your organization make decisions that affect your business. When they have the right information at the right time, they can make the choices that move your company in the right direction. 

Giving the decision-makers the opportunity to explore and interpret information in an interactive visual environment helps democratize data and accelerates data-driven insights that are easy to understand and navigate.

Building a BI and data visualization service in the cloud allows you to take advantage of capabilities such as scalability, availability, redundancy, and enterprise grade security. 

It also lowers the barrier to data connectivity and allows access to far wider range of data sources —both traditional, such as databases, as well as non-traditional, such as SaaS sources. 

An added advantage of a cloud-based data visualization service is the elimination of undifferentiated heavy lifting related to managing server infrastructure.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2j6nqt147721nnhonnwf.png)

> **Architecture Options for Building an Analytics Application on AWS** is a Series containing different articles that cover the key scenarios that are common in many analytics applications and how they influence the design and architecture of your analytics environment in AWS. These series present the assumptions made for each of these scenarios, the common drivers for the design, and a reference architecture for how these scenarios should be implemented.  

Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

In the world of Big Data, data visualization tools and technologies are essential to analyze massive amounts of information and make data-driven decisions.

# Characteristics

 * **Scalability**: Ensure that the underlying BI infrastructure is able to scale up vertically and horizontally both in terms of concurrent users as well as data volume. For example on AES, Amazon QuickSight SPICE and web application automatically scales up server capacity to accommodate a large number of concurrent users without any manual intervention in terms of provisioning additional capacity for data, for load balance, and others.

 * **Connectivity**: BI applications must be able to not just connect with data platforms like traditional Data Warehouse and databases but also support connectivity to data lake and lake house architectures. The application must also have the capacity to connect to non-traditional sources such as SaaS applications. Typically, data stores are secured behind a private subnet and BI tools and applications must be able to connect in a secure mechanism using strategies, such as VPC endpoints and secure firewalls.

 * **Centralized security and compliance**: BI applications must allow for a layered approach for security. This includes: Securing at the perimeter using techniques such as IP allow lists, security groups, ENIs and IAM policies for cloud resource access, securing the data in transit and data at rest using SSL and encryption, and restricting varying levels of access through fine-grained permissions for users to the underlying data and BI assets. The application must also comply with the governmental and industry regulations for the country or region the company is bound by.

 * **Sharing and collaboration**: BI applications must support data democratization. They must have features that allow sharing of the dashboards with other users in the company as well as for multiple report authors to collaborate with one another by sharing access to the underlying dataset. Not all BI tools have this capability. Amazon QuickSight allows the sharing of assets, such as DataSources, DataSets, Analyses, Dashboards, Themes, and Templates.

 * **Logging, monitoring, and auditing**: BI applications must provide adequate mechanisms to monitor and audit the usage of the application for security (to prevent unwanted access to data assets and other resources) and troubleshooting. 
Amazon QuickSight can be used with Amazon CloudWatch, AWS CloudTrail, and IAM to track record of actions taken by a user, user role, or an AWS service. This provides the who, what, when, and where of every user action in QuickSight.

# Reference architecture

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tpe8q7z81y14lvaub14t.png)
*QuickSight dashboard end-to-end design*

* **Data sources**: Supports connection with traditional Data Warehouse or databases and also have the capacity to connect to non-traditional sources such as SaaS applications. 
Supported datasources in QuickSight include Amazon S3, Amazon Redshift, Amazon Aurora, Oracle, MySQL, Microsoft SQL Server, Snowflake, Teradata, Jira, ServiceNow and many more. 
Check here for the complete list of data sources supported in QuickSight. These data sources could be secured behind a private subnet and QuickSight can connect in a secure mechanism using strategies such as VPC Endpoints, Secure Firewalls and others.

* **Visualization Tool**: Amazon QuickSight.

* **Consumers**: Visual dashboard consumers accessing QuickSight console or embedded QuickSight analytics dashboard. 

# Configuration notes

* **Security**: Implement the principle of least privilege throughout the visualization application stack. Ensure data sources are connected using VPC and restricting security groups to only required protocols, sources and destinations. 
Enforce that the users as well as applications in every layer of the stack are given just the right level of access permissions to data and the underlying resources. Ensure seamless integration with identity providers either industry supported or customized. In the case of multi-tenancy, use namespaces for better isolation of principals and other assets across tenants. 
For example, QuickSight follows the least privilege principle and access to AWS resources such as Amazon Redshift, Amazon S3 or Athena (common services used in data warehouse, data lake or lake House Architectures) can be managed through the QuickSight user interface. 
Additional security at the user or group level is supported using fine-grained access control through a combination of IAM permissions. 
Additionally, QuickSight features, such as row level security, column level security, and a range of asset governance capabilities that can be configured directly through QuickSight user interface.

* **Cost optimization**: Accurately identify the volume of dashboard consumers and embedding requirements to determine the optimal pricing model for the given visualization use case. QuickSight offers two different pricing options (capacity and user based), which allows clients to implement cost-effective BI solutions. 
Capacity pricing allows large-scale implementations and user-based pricing allows clients to get started with minimal investment (Note: SPICE has a 250M records or 500 GB volume per dataset limitation).

* **Low latency considerations**: Use in-memory caching option, such as Memcached, Redis. or the in-memory caching engine in QuickSight called SPICE (Super-fast, Parallel, In-memory Calculation Engine) to prevent latency in dashboard rendering while accommodating any built-in restrictions that the Caching technology might have.

* **Pre-process data views**: Ensure that the data is cleansed, standardized, enhanced, and pre-processed to allow analysis within the BI layer. If possible, create pre-processed, pre-combined, pre-aggregated data views for analysis purposes. ETL tools, such as Glue DataBrew, or techniques, such as materialized views, can be employed to achieve this.

---

Hope this guide gives you an Introduction to Data visualization, explains the Characteristics, Reference Architecture and Configuration Notes for Data visualization.

Let me know your thoughts in the comment section 👇
And if you haven't yet, make sure to follow me on below handles:

👋 **connect with me on [LinkedIn](https://www.linkedin.com/in/adit-modi-2a4362191/)**
🤓 **connect with me on [Twitter](https://twitter.com/adi_12_modi)**
🐱‍💻 **follow me on [github](https://github.com/AditModi)**
✍️ **Do Checkout [my blogs](https://aditmodi.hashnode.dev)** 

Like, share and follow me 🚀 for more content.

---

[Reference Guide](https://docs.aws.amazon.com/wellarchitected/latest/analytics-lens/data-visualization.html)