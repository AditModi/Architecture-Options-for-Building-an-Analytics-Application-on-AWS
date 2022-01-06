* Organizations of all sizes have recognized that data is one of the key factors for increasing and sustaining innovation, and driving value for their customers and business units. 
* They are modernizing traditional data platforms with cloud-native technologies that are highly scalable, feature-rich, and cost-effective. 
* As you look to make business decisions driven by data, you can be agile and productive by adopting a mindset that delivers data products from specialized teams, rather than through a centralized data management platform that provides generalized analytics.

* A centralized model simplifies staffing and training by centralizing data and technical expertise in a single place. This reduces technical debt since you are managing a single data platform, which reduces operational costs. Data platform groups, often part of central IT, are divided into teams based on the technical functions they support. 
* For instance, one team might own the ingestion technologies used to collect data from numerous data sources managed by other teams and lines of business (LOBs). A different team might own the data pipelines, the writing and debugging extract, transform, and load (ETL) code, and orchestrating job runs, while validating and fixing data quality issues and ensuring that data processing meets business SLAs. 
* However, managing data through a central data platform can create scaling, ownership, and accountability challenges. Central teams might not understand the specific needs of a data domain, due to data types and storage, security, data catalog requirements, or the specific technologies needed for data processing.

* You can often reduce these challenges by giving ownership and autonomy to the team who owns the data. This allows them to focus on building data products, rather than being limited to a common central data platform. 
* For example, make product teams responsible for ensuring that the product inventory is updated regularly with new products and changes to existing ones. They’re the domain experts of the product inventory datasets, and if a discrepancy occurs, they’re the ones who know how to fix it. 
* Therefore, they’re best able to implement and operate a technical solution to ingest, process, and produce the product inventory dataset. They own everything leading up to the data being consumed: they choose the technology stack, operate in the mindset of data as a product, enforce security and auditing, and provide a mechanism to expose the data to the organization in an easy-to-consume way. 
* This reduces overall friction for information flow in the organization, where the producer is responsible for the datasets they produce and is accountable to the consumer based on the advertised SLAs.

* This data-as-a-product paradigm is similar to the operating model that Amazon uses for building services. Service teams build their services, expose APIs with advertised SLAs, operate their services, and own the end-to-end customer experience. 
* This is distinct from the model where one team builds the software, and a different team operates it. The end-to-end ownership model has allowed us to implement faster, with higher efficiency, and to quickly scale to meet customers’ use cases. 
* We aren’t limited by centralized teams and their ability to scale to meet the demands of the business. Each service we build relies on other services that provide the building blocks. 
* The analogy to this approach in the data world would be the data producers owning the end-to-end implementation and serving of data products, using the technologies they selected based on their unique needs. 

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lao5jezks12kf7hla1gg.png)
 
people have been talking about the data-driven organization model for years, which consists of data producers and consumers. This model is similar to those used by some of early adopting consumers and has been described by "Zhamak Dehghani of Thoughtworks", who coined the term data mesh.

# Characteristics

* Data mesh is a pattern for defining how organizations can organize around data domains with a focus on delivering data as a product. However, it might not be the right pattern for every customer.

* A lake house approach and the data lake architecture provide technical guidance and solutions for building a modern data platform on AWS.

* The lake house approach with a foundational data lake serves as a repeatable blueprint for implementing data domains and products in a scalable way.

* The manner in which you use AWS analytics services in a data mesh pattern might change over time, but remains consistent with the technological recommendations and best practices for each service.

* The following are data mesh design goals:

 * **Data as a product** – Each organizational domain owns their data end to end. They’re responsible for building, operating, serving, and resolving any issues arising from the use of their data. Data accuracy and accountability lies with the data owner within the domain.

 * **Federated data governance** – Data governance helps ensure that data is secure, accurate, and not misused. The technical implementation of data governance, such as collecting lineage, validating data quality, encrypting data at rest and in transit, and enforcing appropriate access controls, can be managed by each of the data domains. However, central data discovery, reporting, and auditing is needed to make it easy for users to find data, and for auditors to verify compliance.

 * **Common access** – Data must be easily consumable by subject matter experts, such as data analysts and data scientists, and by purpose-built analytics and machine learning (ML) services, such as Amazon Athena, Amazon Redshift, and Amazon SageMaker. This requires data domains to expose a set of interfaces that make data consumable while enforcing appropriate access controls and audit tracking.

* The following are user experience considerations:

 * Data teams own their information lifecycle, from the application that creates the original data, to the analytics systems that extract and create business reports and predictions. Through this lifecycle, they own the data model, and determine which datasets are suitable for publication to consumers.

 * Data domain producers expose datasets to the rest of the organization by registering them with a central catalog. They can choose what to share, for how long, and how consumers can interact with them. They’re also responsible for maintaining the data and making sure it’s accurate and current.

 * Data domain consumers and individual users should be given access to data through a supported interface, such as a data API, that helps ensure consistent performance, tracking, and access controls.

 * All data assets are easily discoverable from a single central data catalog. The data catalog contains the datasets registered by data domain producers, including supporting metadata, such as lineage, data quality metrics, ownership information, and business context.

 * All actions taken with data, usage patterns, data transformations, and data classifications should be accessible through a single, central place. Data owners, administrators, and auditors should be able to inspect an organization’s data compliance posture in a single place.

* Let’s start with a high-level reference design that builds on top of the data mesh pattern. It further separates consumers, producers, and central governance to highlight the key aspects discussed previously. However, note that a data domain, in a data mesh pattern, might represent a data consumer, a data producer, or both.

* The AWS Lake House architecture relies on an AWS Glue and AWS Lake Formation Data Catalog for users to access the objects as tables. The users are entitled to these tables using Lake Formation, which is one per AWS account. 
* Each Lake Formation account has its own Data Catalog, but storing the metadata on the data objects on multiple accounts across various catalogs makes it hard for the consumers to select the table. 
* A consumer has to log into individual accounts to see the objects, assuming that the consumer knows exactly where to look. A central catalog also makes it easy to feed into a central business catalog and allows easier auditing of grants or revokes (it just makes it easier; it does not provide a single store of audits). Therefore, a central Data Catalog is recommended.

* The metadata being on the central catalog does not make the tables in individual lakes accessible to all the consumers automatically. The actual entitlement on tables is individually granted and revoked by the application owner.

* This allowss the data mesh objective of the data strategy where the data is stored in multiple individually managed lakes, as opposed to a single central lake, while being accessible, provided properly entitled, to all the consumers. 
* The role of the Data Catalog is of paramount importance here as the consumers can locate the proper storage of the data, they are interested in.

|Term	         |Definition     |
| -------------- |---------------|
|Data mesh	|Data is stored in multiple data stores, not in one single store. Consumers can access them as needed, assuming they are properly entitled.|
|AWS Lake Formation	|A service that makes the data available as tables. Allows the owner of that table to give permissions to consumers.|
|AWS Glue Data Catalog (Data Catalog)	|A data store containing metadata about the data, for example, table name, the columns in them, and user-defined tags. It does not contain actual data. This allows a consumer to know what to select.|
|Amazon Athena	|A managed service that allows a user to enter a SQL query to select data. It in turn fetches the data and presents it in a tabular format. Athena needs a Data Catalog to let the consumer know the columns to select.|
|Resource link	|A link that extends from one catalog to another and allows the consumers in the remote catalog to view and query the tables in the remote database as if the tables were in their local database. There are two types of resource links: for a specific table, and for an entire database.|

# Reference architecture

* Here is a pattern for a single producer account, a single consumer account, and a central Lake Formation account. Each account has an AWS Glue Data Catalog. 
* The central account's Data Catalog is considered the main catalog. Resource links are established to the producer and consumer accounts. 
* This way, when the central account changes something, both accounts get the schema updates. The consumers selecting data will always see the most recent metadata.

* The producer account always has the authority to grant or revoke the permissions on the tables in its Data Catalog. The central Lake Formation account is merely a holder of metadata, which sends it to all the consumer accounts which has a subscription via a resource link. Under no circumstances the central Lake Formation account can grant on its own.

* With the concept in place, let’s look at three design patterns for deploying a data mesh architecture.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h336eb7blyqv25ixxjqx.png)

> Data mesh reference architecture

* Workflow from producer to consumer:

1. Data source locations hosted by the producer are created within the producer’s AWS Glue Data Catalog and registered with Lake Formation.

2. When a dataset is presented as a product, producers create Lake Formation Data Catalog entities (database, table, columns, attributes) within the central governance account. This makes it easy to find and discover catalogs across consumers. However, this doesn’t grant any permission rights to catalogs or data to all accounts or consumers, and all grants are be authorized by the producer.

3. The central Lake Formation Data Catalog shares the Data Catalog resources back to the producer account with required permissions via Lake Formation resource links to metadata databases and tables.

4. Lake Formation permissions are granted in the central account to producer role personas (such as the data engineer role) to manage schema changes and perform data transformations (alter, delete, update) on the central Data Catalog.

5. Producers accept the resource share from the central governance account so they can make changes to the schema at a later time.

6. Data changes made within the producer account are automatically propagated into the central governance copy of the catalog.

7. Based on a consumer access request, and the need to make data visible in the consumer’s AWS Glue Data Catalog, the central account owner grants Lake Formation permissions to a consumer account based on direct entity sharing, or based on tag-based access controls, which can be used to administer access via controls like data classification, cost center, or environment.

8. Lake Formation in the consumer account can define access permissions on these datasets for local users to consume. Users in the consumer account, like data analysts and data scientists, can query data using their chosen tool such as Athena and Amazon Redshift.

In some cases, multiple catalogs are necessary and there is no other alternative. For example, if data is sent to both Regions, there will be two Data Catalogs that need to be maintained.

**Option 1: Central data governance model**

Here is a more practical model with multiple producers and consumers accounts. There is still a single central data governance account, which has resource links to all the other accounts. Note that we didn't deliberately name them with specific lines of business (LOBs), since this model applies to any LOB and any number of lakes. 

*Roles of various accounts*

Here are the roles of the various types of accounts.

|Account	  |Description    |
| --------------  |---------------|	
|Producer account |* Allows data producers to write data into their respective S3 buckets.* Does not allow interactive access to S3 buckets or objects in them.* Allows only production ETL jobs to perform transformation, movement, etc.|
|Consumer account	|* Allows data consumption through Athena, Redshift Spectrum, and web apps.* Only cataloged items can be queried, not all objects in the bucket.* Isolates the data changes (done by producer account) from data access (consumer accounts).|
|Central account	|* This is a central catalog of all metadata. If additional consumer accounts are created, the metadata is replicated from this central account.* Since all metadata is in one place, it allows easier auditing of actions like grants and revokes on tables. The actual auditing is still decentralized but a central account makes the reporting easier.* Consumer accounts need to access the metadata using resource links to this central catalog only.* Does not contain any actual data. Only logs are stored here.|

*Notes*

 * These are just roles and they are not mutually exclusive. It's possible to have one AWS account with both roles of producer and consumer. A batch serving account is such an example.

 * These accounts are Region-specific and are all in the same Region. They are not across Regions.

* These accounts interact as shown in the following diagrams.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/e7uva0hl8xtb680wijm0.png)

*Central data governance model*

* The producers can onboard their dataset table names, but the tables are completely independent and federated in central data governance account.

*Advantages*

 * All datasets are available in one place for querying.

 * Entitlements become easier.

 * A single database to database resource link is enough (assuming database-to-database resource links are allowed).

 * Single source of data truth – one-way sharing of catalog across various organizations.

 * The LOBs still have the choice to define metadata, schema evolution and manage permissions. The central Lake Formation account does not enforce anything on them.

 * Allows centralized auditing.

 * Allows local sandbox accounts for consumers, which is useful in cases such as model training and serving.

*Disadvantages*

 * More complex for consumer analysts than using one data warehouse.

 * Required skills are more aligned to security and governance than analytics.

 * Technology solution – may not solve issues created by misaligned LOBs incentives.

**Option 2: Federated Line of Business (LOB) central governance model**

* In this model, each LOB maintains an independent central Lake Formation account, which eases the use of centralized auditing in that LOB. Consumer accounts can see the data from producer accounts in the same LOB only. For accessing the data across LOBs, they need to establish the resource links to the appropriate catalog.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/laiocn1pyjjh0zcf15t3.png)

*Federated LOB central governance model*

*Advantages*

 * Each LOB still maintains their own Lake Formation central account and access control.

 * The blast radius in case of non–availability of a single Lake Formation account is reduced.

*Disadvantages*

 * Centralized metadata is impossible since there is no central account. Audits from each central account need to be pulled and consolidated.

 * Resource links need to be created across multiple catalogs. This makes it difficult to maintain the links, especially as the number of lakes grows.

**Option 3: Completely federated data governance model**

* In this model, there is no central Lake Formation. Each producer account maintains their own Data Catalog and each consumer accesses the Data Catalog via a resource link.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/v8e0gtq78108g3sud3ak.png)

*Completely federated data governance model*

*Advantages*

 * There is complete separation among the Lake Formation accounts.

 * Local queries go to the local Lake Formation Data Catalog. They don't need the trip to the central Lake Formation.

 * Any operator error that deletes a single Lake Formation account will not affect anything else, even inside the same LOB.

*Disadvantages*

 * Entitlements will need to be distributed.

 * Multiple resource links need to be created and maintained, which quickly becomes a burden in the data organization scale.

 * When data from a central business catalog is replicated over to the other Lake Formation catalogs, all those Lake Formation catalogs need to be updated individually.

   
---

Hope this guide gives you an Introduction to Data Mesh, explains the Characteristics and Reference Architecture for Data Mesh.

Let me know your thoughts in the comment section 👇
And if you haven't yet, make sure to follow me on below handles:

👋 **connect with me on [LinkedIn](https://www.linkedin.com/in/adit-modi-2a4362191/)**
🤓 **connect with me on [Twitter](https://twitter.com/adi_12_modi)**
🐱‍💻 **follow me on [github](https://github.com/AditModi)**
✍️ **Do Checkout [my blogs](https://aditmodi.hashnode.dev)** 

Like, share and follow me 🚀 for more content.

---

[Reference Guide](https://docs.aws.amazon.com/wellarchitected/latest/analytics-lens/data-mesh.html)