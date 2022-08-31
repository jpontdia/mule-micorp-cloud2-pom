# mule-micorp-pom

>Parent POM file for Micorp Demo Services

## Table of contents
1. [Using the parent POM](#usinge-the-parent-pom)
2. [Deployment in Anypoint](#deployment-in-anypoint)
  * [Prerequisites](#prerequisites)
  * [Deployment](#deployment)
3. [Recommended content](#recommended-content)

<br>

## Using the parent POM
To use the parent POM in any of the child projects, specify the `parent`
section in the child `pom.xml` as follows:
```xml
	<parent>
		<groupId>078efef1-d139-48ed-92f5-f8d4a0592374</groupId>
		<artifactId>micorp-pom</artifactId>
		<version>1.0.25</version>
		<relativePath/>
	</parent>
``` 

Update the element `version` to match the lastest release available.

 that must be overriden in every service

### Overriding properties
Next is the list of properties that can be customized for the new services.

Mandatory properties in POM 
| Property      | Description |
| ----------- | ----------- |
| api.layer     | Anypoint Visualizer. API layer for the service: system, process or experience       |
| api.tags      | Anypoint Visualizer. Tags for the service separated by commas, example: customer, finance |

Implementation POM example: [mule-micorp-customer-sapi](https://github.com/jpontdia/mule-micorp-customer-sapi)

Properties in CICD pipeline: Sevice functionality 
| Property      | Description |
| ----------- | ----------- |
| encrypt.key     | Encryption key for secure properties       |
| env      | Environment variable for the service: dev, tst, prd, etc. Must match the Anypoint environments |

Properties in CICD pipeline: Maven deployment 
| Property      | Description |
| ----------- | ----------- |
| cicd.connectedapp.clientid     | Connected App for deployment in CICD, Client-id       |
| cicd.connectedapp.secret      | Connected App for deployment in CICD, Secret |
| anypoint.environment.clientid     | Anypoint environment client credentials for the runtime, Client-id       |
| anypoint.environment.secret      | Anypoint environment client credentials for the runtime, Secret |

Properties in CICD pipeline: Name for the service in CloudHub and deployment environment
| Property      | Description |
| ----------- | ----------- |
| deployment.prefix    | Prefix for the name of the service       |
| deployment.env      | Environment for the service: dev, tst, prd, etc. Must match the Anypoint environments |
| commit.hash     | Git commit hash tag appended to the name of the jar file      |
| build.id     | Build numer for the CICD pipeline added to the name of the jar file |

Implementation CICD example: [dev.yml](https://github.com/jpontdia/mule-micorp-customer-sapi/blob/main/.github/workflows/dev.yml) 

Properties in CICD pipeline: Worker characteristics
| Property      | Description |
| ----------- | ----------- |
| region    | See [CloudHub deploy reference](https://docs.mulesoft.com/mule-runtime/4.4/deploy-to-cloudhub#cloudhub-deploy-reference)        |
| workers     | See [CloudHub deploy reference](https://docs.mulesoft.com/mule-runtime/4.4/deploy-to-cloudhub#cloudhub-deploy-reference) |
| workerType     | See [CloudHub deploy reference](https://docs.mulesoft.com/mule-runtime/4.4/deploy-to-cloudhub#cloudhub-deploy-reference)      |

## Deployment in Anypoint

### Prerequisites
To compile and build the project:
* Java Development Kit (JDK) 8. Must be version 8!
* Apache Maven, version 3.8 or later.
* Anypoint account credentials

<br>

### Deployment
Configure settings.xml in your machine with the correct credentials for Anypoint Platform.
The configuration file used for this parent POM and all the services that implement this artifact is: [settings.xml](
https://github.com/jpontdia/mule-micorp-pom/blob/main/settings.xml)

```xml
	<servers>
		<server>
			<id>anypoint-exchange-v3</id>
			<username>MY-USER</username>
			<password>MY-PASSWORD</password>
		</server>
	</servers>
```

The "id" element must be the same between settings.xml and the repository defined in pom.xml.
Deploy the pom changes to the maven repository for your Anypoint platform, from the command line type:

```xml
mvn deploy
```

<br>

## Recommended content
* [How to work with a parent pom](https://help.mulesoft.com/s/article/How-to-work-with-a-parent-pom)
* [How to deploy mule extension with pom hierarchy to exchange](https://help.mulesoft.com/s/article/How-to-deploy-mule-extension-with-pom-hierarchy-to-exchange)

---
[Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)