<!-- [![REUSE status](https://api.reuse.software/badge/github.com/SAP-samples/teched2023-IN268)](https://api.reuse.software/info/github.com/SAP-samples/teched2023-IN268) -->

# Modernize and Elevate Your Integration to Cloud

<!--
## Description

This session will guide you on how to migrate your existing SAP Process Integration and SAP Process Orchestration scenarios to SAP Integration Suite with the Migration Assessment and the Migration Tooling.

Migration Assessment is a new capability within SAP Integration Suite which helps you estimating the technical efforts involved in the migration process and evaluates how various integration scenarios might be migrated. 

After having finished the assessment of the current SAP Process Orchestration landscape and having estimated the effort needed to migrate with the Interface Migration Assessment capability, the next step is the actual migration. The goal of the Migration Tool is to provide a semi-automated migration where interfaces in the Cloud Integration capability of SAP Integration Suite will be automatically created based on SAP Process Orchestration information, so that ideally 60-70% of technical migration efforts are automated. The migration of scenarios is based on a pattern approach, which means that integration flow templates following a specific pattern are used as skeleton to migrate the content and create the final integration flows.
-->

## Overview

This session introduces attendees to Migration Assessment and Migration Tooling which are capabilities of SAP Integration Suite. This session will guide you on how to migrate your existing SAP Process Integration and SAP Process Orchestration integration scenarios to SAP Integration Suite with the Migration Assessment and the Migration Tooling.

Migration Assessment is a new capability within SAP Integration Suite which helps you estimating the technical efforts involved in the migration process and evaluates how various integration scenarios might be migrated. 

After having finished the assessment of the current SAP Process Orchestration landscape and having estimated the effort needed to migrate with the Interface Migration Assessment capability, the next step is the actual migration. The goal of the Migration Tool is to provide a semi-automated migration where interfaces in the Cloud Integration capability of SAP Integration Suite will be automatically created based on SAP Process Orchestration information, so that ideally 60-70% of technical migration efforts are automated. The migration of scenarios is based on a pattern approach, which means that integration flow templates following a specific pattern are used as skeleton to migrate the content and create the final integration flows.

## Requirements

The requirements for this exercise are listed below. Please note that when using the provided laptops and tenants the steps have been already done. For more details, see [Assessing the Migration Strategy and Migrating Content](https://help.sap.com/docs/integration-suite/sap-integration-suite/assessing-migration-strategy-and-migrating-content).

1. Download and install Insomnia or any other http client.
2. Connect your SAP Process Orchestration system to the tenant using the Cloud Connector.
3. Provision Migration Assessment and Cloud Integration capabilities on the tenant.
4. Assign appropriate roles to your user.
5. Setup destination to SAP Process Orchestration.

## Access to SAP Integration Suite tenant

For running through the exercises, you need access to an SAP Integration Suite tenant.

- Please use this [**SAP Integration Suite tenant**](https://cpisuite-europe-03.integrationsuite.cfapps.eu20-001.hana.ondemand.com/shell/home) for your exercises.
- Use the user **userXX** with **XX** your ID and password provided by the instructors.

## Exercises

<!-- Provide the exercise content here directly in README.md using [markdown](https://guides.github.com/features/mastering-markdown/) and linking to the specific exercise pages, below is an example. -->

In the following, the complete list of exercise steps are listed. You can use this section as an index or table of contents. Use the breadcrumb navigation on top of the pages to go back to the Table of Contents.

If you are interested in how the **Migration Assessment** works, start with the first exercise.
- [Exercise 1 - Migration Assessment](exercises/ex1/)

You do not need to go through all three **Migration Tool** exercises, you can pick just one of the exercises depending on your interest and skills. If you are not familiar with SAP Integration Suite, start with a simple scenario. Otherwise, if you are already experienced with SAP Integration Suite, you may opt for the last exercise since this also covers new features that we have recently shipped. In any case, if you like to run through any of the migration tool exercises, you first need to create an integration package and setup the API client which is described in the Prerequisites chapter.

- [Prerequisites for the Migration Tool exercises](exercises/ex0/)
- [Exercise 2 - Migrate and test a simple Point-to-Point scenario](exercises/ex2/)
- [Exercise 3 - Migrate and test a Point-to-Point scenario with JSON conversion](exercises/ex3/).
- [Exercise 4 - Migrate and test a Content-Based-Routing scenario](exercises/ex4/)
  
<!-- **OR** Link to the Tutorial Navigator for example... 
Start the exercises [here](https://developers.sap.com/tutorials/abap-environment-trial-onboarding.html).
-->

<!--
**IMPORTANT**
Your repo must contain the .reuse and LICENSES folder and the License section below. DO NOT REMOVE the section or folders/files. Also, remove all unused template assets (images, folders, etc) from the exercises folder. 
-->

<!--
## Contributing
Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) to understand the contribution guidelines.
-->

## Code of Conduct
1. Use the tenant that we provide only for this exercise, and not for anything else. For further exploration of Migration Assessment and Cloud Integration, use a free BTP trial account or a Free Tier tenant.
2. Do not share any private or personal information such as your name, email address or affiliation.
3. Please strictly follow the instructions, regarding the naming conventions you will use to name the artifacts you will create. This ensures that you will be able to successfully complete the tasks, without clashing with other participants.
4. Other artifacts, created by other participants, will appear in your shared account. Do not access or delete these artifacts. Please respect the rules and allow others to have the same learnings as you.

Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## How to obtain support
Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2023 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
