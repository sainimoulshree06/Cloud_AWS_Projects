# Project 1 Objective
 - The project aims to migrate data from the City of Vancouver to an AWS cloud platform and create a comprehensive data analytics pipeline. The goal is to streamline data processing, analysis, and visualization for various city departments, ensuring scalability, security, and efficiency in data management.

## Table of Contents
 - [Methodology](#methodology)
 - [AWS Services](#aws-services)
 - [Data Pipeline Implementation](#data-pipeline-implementation)
 - [Data Analysis](#data-analysis)
 - [Outcome](#outcome)
 - [Insights and Findings](#insights-and-findings)
 - [Cost Estimation](#cost-estimation)
 - [Conclusion](#conclusion)

## Methodology

### Data Analytical Question Formulation
 - Delved into the data for 2023 and 2024 to produce a metric called “Percentage of Calls handled.” The metric will provide the percentage of calls handled in the years 2023 and 2024, respectively
 - Percentage of calls handled = (Number of calls handled/ Number of calls offered) * 100
   
   <kbd> <img src="https://github.com/user-attachments/assets/b4ba5957-631f-40cb-843f-3cbc6c1e20c9" /> </kbd>

### Data Discovery
- Focussed on the procedure ‘Contact Centre Metrics’ in the Government and Finance department for the city of Vancouver. [Data Source Link](https://opendata.vancouver.ca/explore/dataset/3-1-1-contact-centre-metrics/information/)
- Utilized datasets in Excel Format is as shown below.
   
  <kbd> <img src="https://github.com/user-attachments/assets/83f35f73-b08c-4036-9ee7-a5299c6434ee" /> </kbd>
  
  
### Dataset Preparation
 - Involved:
    - Data collection
    - ETL processes
    - Data cleaning using AWS Glue DataBrew.

### Data Pipeline Design
 - Designed using draw.io to automate data processing stages.

<kbd> <img src="https://github.com/user-attachments/assets/1db2d1a2-0146-4cdc-8ca0-635b5c38f8c3" /> </kbd>

### Data Analysis
 - Performed using AWS Athena for querying and deriving insights.
   
## AWS Services
 - AWS Services:
    - Amazon S3 for storage
    - EC2 for computation
    - AWS Glue for ETL processes
    - Athena for data analysis.
 
## Data Pipeline Implementation:
 - Implemented using AWS Glue for ETL processes.
 - Transformation operations included schema changes, aggregation, and union operations.
    - Change Schema Operation: The schema of the 2023 and 2024 dataset has been changed by deleting all other columns that are not required and keeping and renaming the columns BI_ID, Year, calls_offered, and calls_handled.
    - Aggregate Operation: The aggregate function has been used to aggregate the records of the ‘Year’ column within the 2023 and 2024 dataset.
    - Union Operation: In order to prepare a collective dataset out of 2023 and 2024 records, the Union function has been utilized to create a new output from all the records of the two similar input datasets.
    - Change Schema: At this stage, unwanted columns have been deleted by using the change schema operation
    - Derived Column: At this stage, the matric is calculated by performing the SQL operation
Calls handled Percentage = (calls_handled/calls_offered) *100.
   
   <kbd> <img src="https://github.com/user-attachments/assets/3e9b389a-6083-4f76-97de-90bf7b0b63e2" /> </kbd>

## Data Analysis
 - Data analysis was performed using AWS Athena.
 - SQL database was utilized to analyze the content of the dataset.
 - Table DDL

```sql
  --Contact Centre Table --
CREATE EXTERNAL TABLE `gov_fin_contactcentre_table_vivek`(
  `year` string, 
  `percent_of_calls_handled` string)
ROW FORMAT DELIMITED 
  FIELDS TERMINATED BY ',' 
STORED AS INPUTFORMAT 
  'org.apache.hadoop.mapred.TextInputFormat' 
OUTPUTFORMAT 
  'org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat'
LOCATION
  's3://project1-gov-fin-vivek-dataset/Government and Finance Domain/Curated/Yearly Analysis'
TBLPROPERTIES (
  'classification'='csv', 
  'skip.header.line.count'='1', 
  'transient_lastDdlTime'='1724308959')
```
 - Data as pulled from AWS Athena Database is as shown below:
   
<kbd> <img src="https://github.com/user-attachments/assets/c214f109-7a25-4891-930e-68468c60c921" /> </kbd>

## Outcome
 - General Server and Web Server were set up using Amazon EC2 for internal and external data access.
 - Published the annual analysis report on the percentage of calls handled for public access.
   
<kbd> <img src="https://github.com/user-attachments/assets/77a924dd-3efb-46c8-aef0-2a18660fa08f" /> </kbd>

## Insights and Findings
 - 2023: The percentage of calls handled was 94.19%, indicating a high efficiency in managing calls at the '3-1-1 contact center' for the City of Vancouver during this year.
 - 2024: The percentage of calls handled dropped slightly to 92.93%. This reduction, although minor, indicates a slight decline in the call-handling efficiency compared to the previous year.
 - Comparison: There is a noticeable decrease of approximately 1.26% in the percentage of calls handled from 2023 to 2024. This could be due to various factors such as an increase in call volume, changes in operational procedures, or resource allocation challenges.

## Cost Estimation
 - Amazon S3: Estimated annual expense of $285.846 for storage across four buckets.
 - AWS Glue DataBrew: Estimated yearly cost of $32.04 for cleaning and restructuring datasets.
 - AWS Glue: Estimated total cost of $13.20 for ETL job runs.
 - Amazon Athena: Estimated annual expense of $35.76 for querying and analysis.
 - EC2: Total yearly cost of $225.96 for hosting general and web servers.

## Conclusion
 - The project showcases the effectiveness of using AWS cloud services for large-scale data analytics and highlights the capabilities in automating data workflows and gaining insights for city management.

# Project 2 Objective
 - The objective of this project is to accurately calculate the student graduation rates for the years 2022, 2023 and 2024 at the University Canada West (UCW).
 - By leveraging sample data, such as student records and course completion information, this project seeks to uncover key insights into student performance, identify trends, and offer data-driven recommendations to improve future graduation rates.

## Table of Contents
 - [Data Analytical Question Formulation](#data-analytical-question-formulation)
 - [Dataset Preparation](#dataset-preparation)
 - [Data Pipeline Design](#data-pipeline-design)
 - [AWS Services](#aws-services)
 - [Data Cleaning and Structuring](#data-cleaning-and-structuring)
 - [Data Pipeline Implementation](#data-pipeline-Implementation)
 - [Outcome](#outcome)
 - [Insights and Findings](#insights-and-findings)
 - [Conclusion](#conclusion)

## Data Analytical Question Formulation
 - Delved into the sample data for 2022, 2023 and 2024 to produce a metric called “Student Graduation Rate.” The metric will provide the percentage of student graduated in the years 2022, 2023 and 2024, respectively.
 - Percentage of Students Graduated (SGR) = (Number of Student Enrolled/ Number of Student Graduated) * 100
  
## Dataset Preparation
 - Sample dataset includes two Excel files
    - Sample Student Records Information.
<kbd> <img src="https://github.com/user-attachments/assets/914c6d2a-d87e-43b9-b06e-cde92d67f59c" /> </kbd>
    - Sample Graduation Records Information.<kbd> <img src="https://github.com/user-attachments/assets/73c8cfc3-deb2-4657-a2f5-ee75d2868d7e" /> </kbd>
      
## Data Pipeline Design
 - Designed using draw.io to anlayse data processing stages.

<kbd> <img src="https://github.com/user-attachments/assets/d95b91b5-3d91-4169-8fba-9cd15b5aea17" /> </kbd>
   
## AWS Services
 - AWS Services:
    - Amazon S3 for storage
    - AWS GlueData Brew for Cleaning and Structuring.
    - AWS Glue for Data Pipleline.

## Data Cleaning and Structuring
 - It includes operations such as
    - Checking invalid values in data set such as null rows.
    - Renaming of coloum names.
    - Change of Data Type for columns.
    - Change of Schema (Addition of Coloumn).
    - Creation and publishing of recipe.

<kbd> <img src="https://github.com/user-attachments/assets/db441eb5-0266-48f6-911c-3c06a8b1f9c6" /> </kbd>

## Data Pipeline Implementation:
 - Implemented using AWS Glue for ETL processes.
 - Transformation operations included schema changes, aggregation, and union operations.
   
<kbd> <img src="https://github.com/user-attachments/assets/c5c54041-9b76-4cb8-aac0-682901128319" /> </kbd>

## Outcome
 - Figure shows the determination of metrics as deduced from ETL Glue.
   
<kbd> <img src="https://github.com/user-attachments/assets/ef50dbd0-f11f-42d4-9a3e-7052bb8347e6" /> </kbd>

## Insights and Findings
 - Student Graduation Rate (SGR) for 2023:
    - The graduation rate for the year 2023 is 66.67%.
    - This indicates that approximately two-thirds of the students enrolled in the relevant programs at UCW successfully graduated in 2023.
    - This rate reflects a decrease when compared to the previous year (2022).
      
 - Student Graduation Rate (SGR) for 2024:
    - The graduation rate for the year 2024 is 69.70%.
    - This shows a slight improvement over the 2023 graduation rate, suggesting positive changes in student performance or institutional effectiveness.
    - However, it still falls short of the graduation rate observed in 2022.

 - Trend Analysis:
    - There is a notable fluctuation in the graduation rates over the three years:
    - 2022: 73.53%
    - 2023: 66.67% (a decrease from 2022)
    - 2024: 69.70% (an increase from 2023 but still lower than 2022)
    - This trend highlights potential areas of concern in student retention or program effectiveness that UCW may need to address.

## Conclusion
 - The project effectively uses AWS Glue DataBrew for data cleaning and transformation, and the ETL pipeline is successfully executed to calculate the student graduation rate.
 - The entire workflow, from data preparation to final output generation, is well-organized with clear steps for extracting, transforming, and loading data into an S3 bucket.
 - The project aims to provide insights into university graduation rates by using a systematic data processing approach, and the documented pipeline reflects a comprehensive methodology to achieve the objective.

# Project 3 Objective
 - To design and implement a secure, efficient, and scalable Data Analytics Platform (DAP) for the City of Vancouver using AWS cloud services. This platform aims to facilitate the migration, storage, processing, and analysis of city datasets to enhance data-driven decision-making while ensuring data protection, governance, and compliance with privacy standards.

## Table of Contents
 - [Data Discovery](#data-discovery)
 - [ETL Workflow](#etl-workflow)
 - [Data protection](#data-protection)
 - [Data Governance](#data-governance)
 - [Data Monitoring](#data-monitoring)
 - [AWS Services Used](aws-services-used)
 - [DAP Architectural Analysis](#dap-architectural-analysis)
 - [Insights and Findings](#insights-and-findings)
 - [Conclusion](#conclusion)

### Data Discovery
- Focussed on the procedure ‘Awarded Contracts’ in the Government and Finance department for the city of Vancouver. [Link](https://opendata.vancouver.ca/explore/dataset/awarded-contracts/information/?disjunctive.bid_type)

### ETL Workflow
 - Implemented using AWS Glue for ETL processes.
<kbd> <img src="https://github.com/user-attachments/assets/dcd7ca1e-b819-48dc-823e-36b33ea2c221" /> </kbd>
  
### Data Protection
 - Identity and Access Management (IAM)
    - User Access Control: IAM is used to create users, user groups, and roles to manage access to AWS resources. The project assigns specific roles, such as 'LabRole,' to ensure that only authorized users have the necessary permissions.
<kbd> <img src="https://github.com/user-attachments/assets/0149e8a3-2985-4c67-8a2d-f4e2f6fd329b" /> </kbd>
    - Policy Creation: Policies are defined to grant the minimum required permissions for users, ensuring that each user or group can access only the resources they need.
 - Encryption and Decryption
    - AWS Key Management Service (KMS):
    - Symmetric Key: Used to encrypt and decrypt data using the same key. This key is used for encrypting data stored in Amazon S3 buckets, ensuring that only authorized users can access the data.
    - Asymmetric Key: A pair of public and private keys is used for encryption and decryption. This method is used for data that requires higher security, allowing encryption with one key and decryption with another.
<kbd> <img src="https://github.com/user-attachments/assets/78a59c3b-9faa-485b-861e-898709f1e2c2" /> </kbd>
 - Data Storage Security in Amazon S3
    - Bucket Policies and Access Controls: Access to the S3 buckets is restricted using IAM roles and bucket policies to ensure that only authorized users and services can access the data.
    - ETL Pipeline Security: The ETL pipeline processes data through AWS Glue with encryption mechanisms to protect data during transformation.
 - Techniques for Integrity Protection
    - Data Integrity Checks: Encryption and decryption mechanisms ensure that data is secure and unaltered during storage and transmission. For example:
    - Versioning in S3: Amazon S3 versioning is configured to keep previous versions of objects, preventing data loss from accidental deletions or alterations.
<kbd> <img src="https://github.com/user-attachments/assets/f4b3f5d4-3739-476a-87df-eba91abe7fd7" /> </kbd>
 - Monitoring and Auditing
    - Replication:Replication provides data protection by automatically making several copies of the data in different buckets, whether in the same region or different regions.
<kbd> <img src="https://github.com/user-attachments/assets/c31bf07a-5cfb-4b60-8556-fb0a8a40e6dc" /> </kbd>

### Data Governance
 - Data Quality Management
    - AWS Glue: ETL Pipeline - The ETL (Extract, Transform, Load) pipeline using AWS Glue is designed to clean, process, and structure the data before it is stored in the "Trusted" zone. This ensures that the data used for analytics is of high quality, complete, and ready for analysis.
<kbd> <img src="https://github.com/user-attachments/assets/3f36ebff-925c-4c8e-873b-03a76b642771" /> </kbd>
    - Data Quality Checks: During the data processing phase, AWS Glue performs data quality checks to remove duplicates, fill in missing values, and format the data according to predefined standards.
<kbd> <img src="https://github.com/user-attachments/assets/b1e2a736-8e0e-420a-a01f-f97101d9bee0" /> </kbd>
    - Conditional Routing: Only records that pass data quality checks are moved into the trusted zone, ensuring that the dataset used for analytics is accurate and reliable.
<kbd> <img src="https://github.com/user-attachments/assets/43ab5eeb-80ff-4a7e-9297-b3e02b833755" /> </kbd>
 - Data Privacy Management
    - Encryption and Access Control: Data privacy is enforced by encrypting sensitive data using AWS KMS and restricting access through IAM policies. Only authorized users with the appropriate roles can access and manipulate sensitive data, ensuring that privacy is maintained.
 - Data Versioning: S3 versioning is enabled to maintain a history of changes to the data. This allows for the recovery of previous versions in case of accidental deletions or modifications, supporting data governance by providing data lineage and audit trails.
    - LabRole Implementation: A predefined role ('LabRole') is assigned to manage permissions for encryption keys, data access, and usage within the platform, ensuring consistent governance policies across the platform.
   
### Data Monitoring
 - AWS CloudWatch for Real-Time Monitoring
    - Resource Monitoring: AWS CloudWatch is used to monitor key metrics of AWS resources, such as CPU utilization, memory usage, and network activity. It provides real-time insights into the performance of the data analytics platform.
    - Custom Metrics and Dashboards: CloudWatch allows the creation of custom metrics and dashboards for specific aspects of the data analytics platform. For example, monitoring the status of S3 buckets, ETL pipelines in AWS Glue, and data processing jobs helps track data flow and detect anomalies.
<kbd> <img src="https://github.com/user-attachments/assets/a05efbac-af60-44cd-81da-ab08890589fb" /> </kbd>
    - Alarms and Notifications: CloudWatch Alarms are set up to trigger notifications when certain thresholds are breached (e.g., unusually high data access attempts, resource usage spikes). This proactive monitoring helps in identifying and mitigating potential security incidents or performance issues.
<kbd> <img src="https://github.com/user-attachments/assets/40569bee-8274-4b29-87da-14e4a46eb538" /> </kbd>
 - AWS CloudTrail for Audit Logging
    - Activity Logging: AWS CloudTrail captures and logs all API calls made within the AWS environment. This includes actions performed on data stored in S3, modifications to IAM roles, and operations within AWS Glue.
    - Audit Trails: CloudTrail logs serve as an audit trail, documenting who accessed or modified the data and when these actions occurred. This is crucial for tracking unauthorized access attempts and ensuring compliance with data governance policies.
    - Event History: CloudTrail maintains a history of events for a specified period, allowing for a retrospective analysis of data access and usage patterns. This can be used to detect unusual activity or verify compliance with data privacy regulations.
<kbd> <img src="https://github.com/user-attachments/assets/ebed967a-7e96-4352-8cc4-b166400a284a" /> </kbd>

## AWS Services Utilised
 - AWS Services:
    - IAM: Access control and user management.
    - KMS: Encryption and key management.
    - S3: Data storage and management with encryption and versioning.
    - AWS Glue: Data integration, ETL, and data quality management.
    - CloudWatch: Real-time monitoring and alerting.
    - CloudTrail: Audit logging and activity tracking.
    - S3 Access Logs: Data access monitoring and auditing.
    - Cost Explorer: Cost tracking and optimization.
      
## DAP Architectural Anlaysis
 - Operational Excellence
    - Best Practices: The platform implements AWS best practices to enhance operational efficiency, reliability, and scalability. This includes using IAM for fine-grained access control and AWS Glue for structured data processing.
    - Disaster Recovery: S3 bucket replication and versioning are used to implement disaster recovery strategies. Replicated buckets and versioning ensure that data is recoverable in the event of accidental deletion or corruption.
    - Real-Time Monitoring: AWS CloudWatch monitors the performance and health of the platform in real-time, enabling proactive identification of issues through automated alerts for key metrics like CPU usage and memory consumption.
 - Security
    - Comprehensive Security Practices: Security is a core focus of the DAP architecture. IAM roles and policies are used to enforce the principle of least privilege, ensuring that users and applications have only the necessary access rights.
    - Data Encryption: AWS KMS is used to encrypt sensitive data at rest in S3 buckets. Both symmetric and asymmetric encryption techniques are employed to ensure that data remains confidential and protected from unauthorized access.
    - Auditing and Monitoring: AWS CloudTrail is enabled to log and monitor all user activities, providing a comprehensive audit trail. This logging ensures transparency, accountability, and the ability to detect potential security incidents promptly.
 - Reliability
    - Data Redundancy and Versioning: Amazon S3 versioning is enabled to maintain multiple versions of objects, ensuring that previous versions are available in case of accidental deletions or modifications. This supports data integrity and reliability.
    - Regular Backups: The platform employs regular backups of data and applications, facilitated through S3 bucket replication and automated processes in AWS Glue. This allows for quick restoration in the event of a failure.
    - Data Quality and Integrity: AWS Glue is used to automate the data governance process, ensuring completeness, uniqueness, and freshness of data. This automation helps maintain the reliability of the datasets used for analysis.
 - Performance Efficiency
    - Optimized Resource Usage: The platform is designed to use Amazon S3 for storing raw, processed, and curated datasets. This service is chosen for its ability to handle large volumes of data efficiently.
    - Resource Monitoring and Tuning: AWS CloudWatch continuously monitors resource performance, including CPU utilization and memory usage. Performance metrics are tracked in real-time to identify bottlenecks and optimize resources.
    - Right Sizing of Resources: The platform ensures that the instances and storage solutions are right-sized based on performance requirements, ensuring efficient resource allocation and avoiding over-provisioning.
 - Cost Optimization
   - Cost Management: AWS Cost Explorer is used to monitor and analyze cost and usage patterns. This helps identify opportunities for cost savings, such as optimizing storage costs and minimizing redundant data processing.
    - Data Quality Routing: Data quality is enhanced through conditional routing in the ETL pipeline, where only records passing quality checks are processed further. This reduces costs by avoiding storage of outdated, null, or redundant data.
    - Elastic Resource Allocation: The platform adjusts the number of running instances based on the current needs. For example, it uses a general server during standard operations and scales to a web server when publishing data to the internet, optimizing resource costs.
 - Sustainability
    - Long-Term Efficiency and Scalability: The architecture is designed to ensure long-term sustainability by focusing on efficient resource utilization. Services like Amazon S3 and Glue are used in a manner that allows for scalability while minimizing resource wastage.
    - Resource Efficiency: By rightsizing instances and optimizing storage, the platform minimizes its carbon footprint and operational costs, supporting sustainable data management practices.

## Insights and Findings
 - Secure Data Analytics Platform: The project successfully implements a secure data analytics platform for the City of Vancouver using AWS services. Data protection is ensured through encryption (using AWS KMS) and access control (via IAM), safeguarding data confidentiality and integrity.
 - Effective Data Governance: The platform enforces data governance using AWS Glue for ETL processes and data quality checks, ensuring that only high-quality, clean data is used for analysis. IAM policies and S3 bucket structuring further support privacy and compliance.
 - Comprehensive Data Monitoring: Real-time monitoring using AWS CloudWatch and CloudTrail tracks resource usage, API activities, and data access. This continuous monitoring helps maintain operational transparency and swiftly detect anomalies or security issues.
 - Scalability and Cost Optimization: The architecture leverages AWS services like S3 and Glue to create a scalable platform capable of handling large datasets. Cost optimization is managed through AWS Cost Explorer, ensuring efficient resource usage.
 - Enhanced Data Security and Privacy: Encryption techniques and role-based access control ensure data privacy and compliance, critical for handling sensitive city data. Versioning in S3 maintains data integrity, allowing for recovery of previous data versions.

## Conclusion
 - The AWS Data Analytics Platform for the City of Vancouver successfully establishes a secure, scalable, and efficient environment for managing and analyzing city datasets. By leveraging a combination of AWS services, including IAM, KMS, S3, Glue, CloudWatch, and CloudTrail, the platform ensures robust data protection, governance, and real-time monitoring. This approach not only safeguards sensitive data through encryption and access controls but also enhances data quality and integrity through meticulous ETL processes and data governance practices.
 - The platform is designed to adapt to varying data volumes and analytical needs, demonstrating both scalability and cost efficiency. It sets a strong foundation for data-driven decision-making while adhering to privacy and compliance standards. This project showcases how cloud-based solutions can be effectively utilized to meet the complex data management needs of public sector entities. Moving forward, the platform can be further enhanced with advanced analytics and automated governance to provide deeper insights and continuous optimization.
