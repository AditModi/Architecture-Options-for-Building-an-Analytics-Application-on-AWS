* Most analytics applications require frequent batch processing, which allows them to process data in batches at varying interval. For example, processing daily sales aggregations by individual store and then writing that data to the data warehouse on a nightly basis can allow business intelligence (BI) reporting queries to run faster. 
* Batch systems must be built to scale for all sizes of data and scale seamlessly to the size of the dataset being processed at various job runs.

* It is important for the batch processing system to be able to support disparate source and target systems, process various data formats, seamlessly scale out to process peak data volumes, ability to orchestrate jobs using workflow, provide a simple way to monitor the jobs and most importantly offer an ease of use development framework that accelerates job development. 
* Business requirements might dictate that batch data processing jobs be bound by an SLA, or have certain budget thresholds. Use these requirements to determine the characteristics of the batch processing architecture.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2pta6krv4lb42yftbhd4.png)
 

> **Architecture Options for Building an Analytics Application on AWS** is a Series containing different articles that cover the key scenarios that are common in many analytics applications and how they influence the design and architecture of your analytics environment in AWS. These series present the assumptions made for each of these scenarios, the common drivers for the design, and a reference architecture for how these scenarios should be implemented.

* On AWS, analytic services, such as Amazon EMR , Amazon Redshift , Lake Formation Blueprints , and AWS Glue family services namely Glue ETL , Glue Workflows , AWS Glue DataBrew , AWS Glue Elastic Views allow you to run batch data processing jobs at scale for all batch data processing use cases and for various personas, such as data engineer, data analyst, and data scientists. 
* While there are some overlapping capabilities between these services, knowing the core competencies and when to use which service or services allow you to accomplish your objectives in the most effective way.

# Characteristics

* Following are the key characteristics that determine how you should plan when developing a batch processing architecture.

 * **Ease of use development framework:** This is one of the most important characteristics that truly allows personas of ETL developers and data engineers, data analysts, and data scientists to improve their overall efficiencies. An ETL developer benefits from a hybrid development interface that helps them to use the best of both—developing part of their job and switching to writing customized complex code where applicable. Data analysts and data scientists spend a lot of their time preparing data for actual analysis, or capturing feature engineering data for their machine learning models. You can improve their efficiencies in data preparation by adopting a no-code data preparation interface which helps them to normalize and clean data up to 80% faster compared to traditional approached to data preparation.

 * **Support disparate source and target systems:** Your batch processing system should have the ability to support various different types of data sources and targets between relational, semi-structured, non-relational, and SaaS providers. When operating in the cloud, a connector ecosystem can benefit you by seamlessly connecting to various sources and targets, and can simplify your job development.

 * **Support various data file formats:** Some of the commonly seen data formats are CSV, Excel, JSON, Apache Parquet, Apache ORC, XML, and Logstash Grok. Your job development can be accelerated and simplified if the batch processing services can natively profile these various file formats, infer schema automatically (including complex nested structures) so that you can focus more on building transformations.

 * **Seamlessly scale out to process peak data volumes:** Most batch processing jobs experience varying data volumes. Your batch processing job should have the ability to scale out to handle peak data spikes and scale back in when the job completes.

 * **Simplified job orchestration with job bookmarking capability:** The ability to develop job orchestration with dependency management, and the ability to author the workflow using API, CLI, and a graphical user interface allows for a robust CI/CD integration.

 * **Ability to monitor and alert on job failure:** This is an important measure for ease of operational management. Having quick and easy access to job logs, and a graphical monitoring interface to access job metrics can quickly help you identify errors and tuning opportunities for your job. Coupling that with an event-driven approach to alert on job failure will be invaluable for easing operational management.

 * **Provide a low-cost solution:** Costs can quickly get out of control if you do not plan correctly. A pay as you go pricing model for both compute and authoring jobs can help you overcome hefty costs upfront and allows you to only pay for what you use instead of overpaying to accommodate for peak workloads. Use automatic scaling to accommodate spiky workloads when necessary. Using Spot Instances where applicable can bring your costs down for workloads where they are a good fit.


# Reference architecture

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h3jhu0xds4hn59pp15ur.png)

> Batch data processing reference architecture

1. Batch data processing systems typically require a persistent data store for source data. When developing batch data processing applications on AWS, you can use data from various sources, including your on-premises data stores, Amazon RDS, Amazon S3, DynamoDB, and any other databases that are accessible from the cloud.

2. Data processing jobs need access to a variety of data stores to read data. You can use AWS Glue connectors from the AWS Marketplace to connect to a variety of data stores, such as Google BigQuery, and SAP HANA. You can also connect to SaaS application providers, such as Salesforce, ServiceNow, and Google Analytics, using AWS Glue DataBrew and Amazon AppFlow. In addition, you can always rely on the custom JDBC capability in Apache Spark and connect to any JDBC-compliant data store from Amazon EMR or AWS Glue jobs.

3. Choosing the right authoring tool for the job simplifies job development and improves agility.

  a. You can use AWS Glue Studio when authoring jobs for the AWS Glue Spark runtime engine.

  b. Use AWS Glue Blueprints when you need to create a self-service parametrized job for analysts and control what data the analyst is allowed to access.

  c. Use Amazon EMR notebook for interactive job development and scheduling notebook jobs against Amazon EMR.

  d. Use Amazon SageMaker Notebook when working within SageMaker ML development.

  e. Use AWS Glue DataBrew from the AWS Management Console or from a Jupyter Notebook for no-code development experience.

  f. Use Lake Formation Blueprints when you need to quickly create batch data ingestion jobs to rapidly build a data lake in AWS.

4. Choosing the right processing engine for your batch jobs allows you to be flexible with managing costs and lowering operational overhead. Today, only Amazon EMR and Amazon Redshift offer the ability to autoscale seamlessly based on your job runtime metrics using the managed scaling feature and concurrency scaling features for read and write (preview) respectively. Other services depicted under job processing in the reference architecture require you to specify the maximum processing capacity for your job, which will be used to accommodate peak data volumes. 
Amazon EMR and Amazon Redshift offer server-based architectures while rest of the services depicted in the reference architecture are fully serverless. Amazon EMR allows you to use Spot Instances for suitable workloads that can further save your costs. A good strategy is to complement these processing engines to meet the business objectives of the SLA, functionality, and lower TCO by choosing the right engine for the right job.

5. Batch processing jobs usually require writing processed data to a target persistent store. This store can reside anywhere between AWS, on-premises, or other cloud providers. You can use the rich connector interface AWS Glue offers to write data to various target platforms, such as Amazon S3, Snowflake, and Amazon OpenSearch Service. You can also use the native spark JDBC connector feature and write data to any supported JDBC target.

6. All batch jobs require a workflow that can handle dependency checks to ensure no downstream impacts and have a bookmarking capability that allows them to resume where they left off in the event of a failure or at the next run of the job. When using AWS Glue as your batch job processing engine, you can use the native workflow capability to help you create a workflow with a built-in state machine to track the state of your job across the entire workflow. Glue jobs also support a bookmarking capability that keeps track of what it has processed and what needs to be processed during next run. 
Similarly, AWS Lake Formation blueprints support a bookmarking capability when processing incremental data. With EMR Studio, you can schedule notebook jobs. When using any of the analytic processing engines, you can build job workflows using an external scheduler, such as AWS Step Functions or Amazon Managed Workflows for Apache Airflow that allows you to interoperate between any service including external dependencies.

7. Batch processing jobs write data output to target data store, which can be anywhere within the AWS Cloud, on premises, or at another cloud provider. You can use the AWS Glue Data Catalog to crawl the supported target databases to simplify writing to your target database. 

# Configuration notes

**Use AWS Glue Data Catalog as a central metastore for your batch processing jobs, regardless of which AWS analytic service you use as a processing engine.**Batch processing jobs cater to a variety of workloads ranging from running several times an hour or day, to running monthly or quarterly The data volumes vary significantly and so do the consumption patterns on the processed dataset. Always work backwards to understand the business SLAs and develop your job accordingly. The central Data Catalog makes it easy for you to use the right analytic service to meet your business SLAs and other objectives, thereby creating a central analytic ecosystem.

**Avoid lifting and shifting server-based batch processing systems to AWS.** By lifting and shifting traditional batch processing systems into AWS, you risk running over-provisioned resources on Amazon EC2. For example, traditional Hadoop clusters are often over-provisioned and idle in an on-premises setting. Use AWS Managed Services, such as AWS Glue, Amazon EMR, and Amazon Redshift, to simplify your architecture using a lake house pattern and remove the undifferentiated heavy lifting of managing clustered and distributed environments.

**Automate and orchestrate everywhere.** In a traditional batch data processing environment, it’s a best practice to automate and schedule your jobs in the system. In AWS, you should use automation and orchestration for your batch data processing jobs in conjunction with the AWS APIs to spin up and tear down entire compute environments, so that you are only charged when the compute services are in use. For example, when a job is scheduled, a workflow service, such as AWS Step Functions, would use the AWS SDK to provision a new EMR cluster, submit the work, and shut down the cluster after the job is complete. Similarly, you can use Terraform or a CloudFormation template to achieve similar functionality.

**Use Spot Instances and Graviton-based instance types on EMR to save costs and get better price performance ratio.** Use Spot Instances when you have flexible SLAs that are resilient to job reruns upon failure and when there is a need to process very large volumes of data. Use Spot Fleet, EC2 Fleet, and Spot Instance features in Amazon EMR to manage Spot Instances.

**Continually monitor and improve batch processing jobs.** Batch processing systems evolve rapidly as data source volumes increase, new batch processing jobs are authored, and new batch processing frameworks are launched. Instrument your jobs with metrics, timeouts, and alarms to have the metrics and insight to make informed decisions on batch data processing system changes.

---

Hope this guide gives you an Introduction to Batch Data Processing, explains the Characteristics, Reference Architecture and Configuration Notes for Batch Data Processing.

Let me know your thoughts in the comment section 👇
And if you haven't yet, make sure to follow me on below handles:

👋 **connect with me on [LinkedIn](https://www.linkedin.com/in/adit-modi-2a4362191/)**
🤓 **connect with me on [Twitter](https://twitter.com/adi_12_modi)**
🐱‍💻 **follow me on [github](https://github.com/AditModi)**
✍️ **Do Checkout [my blogs](https://aditmodi.hashnode.dev)** 

Like, share and follow me 🚀 for more content.

---

[Reference Guide](https://docs.aws.amazon.com/wellarchitected/latest/analytics-lens/batch-data-processing.html)