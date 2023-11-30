# Datazone-demos
## Background

We built a mini demo environment for AWS Datazone for a customer showcase.

## Setup

This is our demo environment setup involving multiple AWS accounts as well as an Azure account.


## AWS DataZone Key Concepts

[AWS DataZone Documentation](https://docs.aws.amazon.com/datazone/latest/userguide/what-is-datazone.html)

Amazon DataZone is a data management service that makes it faster and easier for you to catalog, discover, share, and govern data stored across AWS, on-premises, and third-party sources. With Amazon DataZone, administrators who oversee organization’s data assets can manage and govern access to data using fine-grained controls. These controls help ensure access with the right level of privileges and context. Amazon DataZone makes it easy for engineers, data scientists, product managers, analysts, and business users to share and access data throughout an organization so they can discover, use, and collaborate to derive data-driven insights.

The following are some concepts and key terms used within AWS DataZone:


### Domain

You can use Amazon DataZone domains to organize your assets, users, and their projects. By associating additional AWS accounts with your Amazon DataZone domains, you can bring together your data sources. You can then publish assets from these data sources to your domain's catalog, with metadata forms and glossaries that improve metadata completeness and quality. You can also search and browse these assets to see what data is published in the domain. Additionally, you can join projects to collaborate with others users, subscribe to assets, and use project environments to access analytics tools, including Amazon Athena and Amazon Redshift. Amazon DataZone domains enable you with the flexibility to reflect the data and analytics needs of your organizational structure, whether it's creating a single Amazon DataZone domain for your enterprise or multiple Amazon DataZone domains for different business units.

### Projects

Projects enable a group of users to collaborate on various business use cases that involve publishing, discovering, subscribing to, and consuming data in the Amazon DataZone catalog. Project members consume assets from the Amazon DataZone catalog and produce new assets using one or more analytical workflows. Projects support the following activities within the data portal:

- Project owners can add members with owner and contributor permissions
- Project members can be SSO users, SSO groups, and IAM users
- Project members can request subscription to the assets in the data catalog
- Subscription approvals are provided to the projects

### Environments

Environments are collections of zero or more configured resources (for example, an Amazon S3, an AWS Glue database, or an Amazon Athena workgroup), with a given set of IAM principals who can operate on those resources. Environments are created by using environment proﬁles which are pre-configured sets of resources and blueprints that provide reusable templates for creating environments. Environment profiles define settings such as the AWS account or region in which environments are deployed.

*Curating of your project inventory assets* - after creating a project inventory, data owners can curate their inventory assets with the required business metadata by adding or updating business names (asset and schema), descriptions (asset and schema), read me, glossary terms (asset and schema), and metadata forms. You can do this via the data portal or by using the Amazon DataZone APIs. Each edit to your asset creates a new inventory version.

## Demo 

### Use Case #1 - Single Sign On using Azure AD Federation

[Full Demo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-1.mp4)

AWS DataZone integrates with a variety of SSO providers such as AWS Identity Center and Azure AD. 

In this demonstration we are integrating with standard Azure AD federation, but integration with Techpass would follow a similar process. Once authentication, AWS DataZone users gets access to the DataZone data portal, which abstracts away the underlying implementation of AWS DataZone and presents a business-friendly interface.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-1.gif) 
<p align="center">
     <i>SSO access via Azure AD Federation to AWS DataZone Data Portal</i>
</p>

### Use Case #2 - Acquiring metadata, preparation and publishing of data as data producer

In this use case, we will demonstrate how a data producer can gather metadata information from its data source, do some preparation work and publish the data to AWS DataZone for sharing. These are the steps:

2.1 Crawling Metadata
    2.1.1 AWS data sources
    2.1.2 Non-AWS data sources
2.2 Data Preparation     
    2.2.1 Inspecting the data schema
    2.2.2 Tagging schema with glossary terms
    2.2.3 Adding business metadata
2.3 Data Publishing

#### Crawling Metadata from AWS Data Sources

[Full Demo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-2-1.mp4)

In this section, we will demonstrate how to ingest metadata of existing data sources within AWS. We are using this data set **HDB Resale Prices Data** available on [Kaggle](https://www.kaggle.com/datasets/teyang/singapore-hdb-flat-resale-prices-19902020). 

Our source data is being stored in S3, and we will be using AWS Glue crawler to extract the metadata and data schema. 

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-2-1.gif) 
<p align="center">
     <i>S3 as data source</i>
</p>

We will directly import the metadata and schema into AWS DataZone. We will select a preconfigured DataZone database entity to hold the data.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-2-2.gif) 
<p align="center">
     <i>Setting crawler output and frequency</i>
</p>

Once done we will hit the crawler to **Run**, and we can observe the progress near the bottom of the screen.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-2-3.gif) 
<p align="center">
     <i>Initiating crawl</i>
</p>

#### Crawling Metadata from Non AWS Data Sourcse

[Full Demo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-1.mp4)

In this section, we will demonstrate how to ingest metadata into AWS Data Zone from non-AWS sources. We are using this data set **HDB Resale Prices Data** available on [Singstat](https://tablebuilder.singstat.gov.sg/table/TS/M810361).We are going to make use of AWS Glue to crawl a database within Azure SQL Server itself. 


![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-1.gif) 
<p align="center">
     <i>Selecting AWS Glue from AWS Console</i>
</p>

Within AWS Glue, we have a number of pre-configured connections. For transactional databases, AWS Glue establishes these connections over JDBC. 

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-2.gif) 
<p align="center">
     <i>AWS Glue connections</i>
</p>

Opening up the connector named "AzureSQL", we can dive deeper into the connection details. Here you can see that we have preconfigured the necessary details to initiate a JDBC connection to our Azure SQL Server such as the JDBC connection URL and other details.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-3.gif) 
<p align="center">
     <i>Connection details including JDBC Connection URL</i>
</p>

These details matches that over at our Azure SQL Server. 

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-4.gif) 
<p align="center">
     <i>Azure SQL server name</i>
</p>

With the preconfigured connections, we can configure a crawler that executes the crawling activity. 

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-5.gif) 
<p align="center">
     <i>AWS Glue Crawler</i>
</p>

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-6.gif) 
<p align="center">
     <i>Configuring crawling source</i>
</p>

Also within the crawler settings, you can choose to output the crawled metadata directly into AWS DataZone.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-7.gif) 
<p align="center">
     <i>Output crawled metadata to AWS DataZone database</i>
</p>

We initiate the crawling activity. This may take some time to complete especially if this is the first time we are crawling this source. Alternatively, we can also schedule the crawler to activate on a recurring basis.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-8.gif) 
<p align="center">
     <i>Initiating Crawler activity</i>
</p>

Now that our crawling activity is complete, let's take a look at the most recent crawl job. You can also see previous runs of the crawler.

#### Data preparation


[Full Demo - Amazon S3](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-2-2.mp4)   
[Full Demo - Azure SQL](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-2.mp4)

Now that our crawl activity is complete, we head back into the data portal. From there we will do some level of preparation work before publishing this into AWS DataZone for wider use.

From within both **HDB Price Information** and **Household Income Information** project, we see there is one present data source which is pointing to glue crawler we configured earlier. The crawled data appears under **Inventory Data**. 

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-2-4.gif) 
<p align="center">
     <i>Crawled information are populated under respective projects</i>
</p>



From here there are several things we will do: 

1. Inspecting the data schema
2. Tagging schema with glossary terms
3. Add business metadata

**Inspecting the data schema**

One of the first few things we like to do as data publisher is to ensure that the data crawled from Glue is correct. From within **Inventory Data**, choose the dataset item we just imported, and check out the **Schema** tab. Here you will see a list of the different columns that has been automatically crawled from the Azure SQL Server data source.

It is usually time consuming to edit and modify any incorrect column names, especially when we are crawling data from transactional systems. Within AWS DataZone, we make use of ML inference to infer the full column names from source itself. Sometimes this may come in the form of short forms or abbreviations. In our example, the raw column name extracted from Azure SQL Server is *gini coeff equiv hh income aft tax (mos)*. This is being automatically inferred to *Gini Coefficient For Equivalent Household Income After Tax*. (See red box highlighted in the gif) All inferred column names have this icon ![inline image](https://dwei4f633mwy3.cloudfront.net/infer.png). You will be asked to accept or reject the inferred column names. 

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-9.gif) 
<p align="center">
     <i>Inspecting the data schema</i>
</p>

**Tagging schema with glossary terms**

To standardise data intepretation and formats across your organisation, it is often advantageous to define a data glossary of your organisational definition of certain data terms. Within AWS DataZone you can tag each column with a predefined glossary term. 

In the example, let's say the term *gini coeff* is well-defined in your organisation and you would like to ensure that the understanding of this term is unified. You can tag this column with the *gini coeff* tag. Once tagged you can double confirm the definition by mouse over. 

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-10.gif) 
<p align="center">
     <i>Tagging with organisational glossary term</i>
</p>


**Adding Business Metadata**

We further improve the contextual information for each dataset by adding business metadata. To add business metadata to an existing inventory data using **Metadata Forms**. In this case let's provide a data SLA level to inform users of the frequency we intend to update this dataset. 

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-11.gif) 
<p align="center">
     <i>Adding business metadata</i>
</p>

[![](datazone-demo-part-4-2.png)]("https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-2-28Nov2023.mp4")


#### Data Publishing 

Once you are done, you can publish the data to the wider AWS Data Zone domain for consumers to access.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-4-13.gif) 
<p align="center">
     <i>Publishing data set</i>
</p>

### Use Case 3 - Searching and Requesting for data access as a data consumer

[Full Demo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-5.mp4)

Now that data has been publish, we are going to obtain this data as a consumer. 
This typically goes through a few steps:

1. Browsing and identifying suitable datasets
2. Requesting access to the data
3. Fulfilment of data access at source

**Browsing and identifying suitable datasets**

From within our Data Portal, we would be able to data published by projects. 

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-5-1.gif) 
<p align="center">
     <i>Viewing datasets as consumer</i>
</p>

The information added during the data preparation phase prior to publishing can be viewed as the consumer, providing added context to the data.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-5-2.gif) 
<p align="center">
     <i>Previewing datasets before subscribing</i>
</p>

If satisfied, the data consumer can move on to subscribe to the data. To do this you must select a project in which to subscribe. Once the subscription is approved, the dataset would be populated in the chosen project.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-5-3.gif) 
<p align="center">
     <i>Subscribing to the dataset</i>
</p>

**Requesting access to the data**

Over at the producer end, we would receive a data request. We can preview the request details, and if satisfied, we can move on to grant access to the data.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-5-4.gif) 
<p align="center">
     <i>Data Producer granting access to data request</i>
</p>

**Fulfilment of data access at source**

After approval of the data access is granted, AWS DataZone helps with fulfiling this secure access to the data at its source, working with the required source system data technology. For AWS data sources like S3 or RDS, AWS DataZone takes care of the access fulfilment automatically behind the scenes using AWS IAM. 

In this example, once data access is fulfilled, the user can immediately start querying with AWS Athena, as the required IAM role assumption has been taken care of. Do note, this example involves cross-account role assumption as both producer and consumer are using different AWS Accounts.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-5-5.gif) 
<p align="center">
     <i>Granting secure data access to AWS data sources</i>
</p>

For non-AWS sources, AWS DataZone is also able to support the provisioning of data access. In this example, once data access is approved, a set of JDBC connection temporary credentials have been generated adn sent to the requesters email securely.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-5-6.gif) 
<p align="center">
     <i>Granting secure data access to non AWS data sources</i>
</p>

The requester can then make use of data exploitation tooling of their choice (in this case Tableau) to start analysing the data.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-5-7.gif) 
<p align="center">
     <i>Using Tableau to access the approved data set</i>
</p>

### Use Case 4 - Revoking access to subscribed data set as data producer

As a data producer within AWS DataZone, you reserve the right to terminate access by anyone to your dataset. This allows you to retain full control and security of your data. 

To do this, you can simply go back to previously approved request, and hit the **Revoke Subscription** button. The access is now removed. 

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-5-8.gif) 
<p align="center">
     <i>Revoking access to subscribed data as data producer</i>
</p>

The data consumer can no longer access this dataset moving forwards.

![datazonedemo](https://dwei4f633mwy3.cloudfront.net/datazone-demo-part-5-9.gif) 
<p align="center">
     <i>Previously granted credentials will not be able to work</i>
</p>


## Credits

This demo is collectively brought to you by these AWS Solution Architects:

- Demo guide and explanation - *this README.md* [Thong Seng Foo](mailto:ftseng@amazon.com)    
- Demo Planning, Environment Setup [Indra Hartanto](mailto:indrahtt@amazon.com), [Bryan Chen](mailto:bryancwh@amazon.com), [Farid Baharuddin](mailto:faridbb@amazon.com)     
- Demo Video recording and edits - [Thong Seng Foo](mailto:ftseng@amazon.com),[Bryan Chen](mailto:bryancwh@amazon.com), [Farid Baharuddin](mailto:faridbb@amazon.com)    