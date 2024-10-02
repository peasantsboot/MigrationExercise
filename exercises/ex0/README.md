
# Prerequisites for the Migration Exercises

After having finished the assessment of the current SAP Process Orchestration landscape and having estimated the effort needed to migrate with the Migration Assessment capability, the next step is the actual migration. The goal of the Migration Tool is to provide a semi-automated migration where interfaces in Cloud Integration will be automatically created so ideally 60-70% of technical migration efforts are automated. The migration of scenarios is based on a pattern approach, the suitable pattern is applied and the required flow steps are added to create the final integration flows.

Before running through the migration tool exercises, you first need to run trough the folloing preparations steps:
- [Create an integration package](#create-integration-package)
- [Setup Bruno API client](#setup-bruno-client)

## Create an Integration package

As a prerequisite, you first need to create an integration package where the automatically generated integration flows are created. If you have already run through other exercises before, you may have already created an own package. In this case, you can simply reuse the other package and skip the steps below.

1. If you are not already in the SAP Integration Suite landing page, switch back to the landing page by clicking on the SAP sign.

<br>![](/exercises/ex2/images/Navigate_Back.png)

2. Navigate to <b>Design > Integrations and APIs</b>, and select  <b>Create</b>.

<br>![](/exercises/ex2/images/Create_Pack.png)
   
3. Fill in the <b>Name</b> of the integration package, e.g. **User XX** where <b>XX</b> is your user number from 00 to 99, and a short <b>Description</b>. The technical name is automatically set. Then click <b>Save</b>.

<br>![](/exercises/ex2/images/00-02-SavePackage.png)

## Setup Bruno API client

To run the integration scenarios, you can use any API test client of your choice. In our exercise scripts,
we use the open source API client Bruno for which we have prepared a collection.
The collection contains sample requests and environment parameters to authenticate at the provided tenant.

### Download and install Bruno's desktop application

Skip this chapter if you run the exercises on the laptop provided by us. Here, the tool has been already installed.
Otherwise, if you run the exercises on your own laptop, you first need to download and install the Bruno API client.

See [Download Bruno's Desktop Application](https://docs.usebruno.com/get-started/bruno-basics/download).

### Import collection

Import the provided collection if not already done.

1. Download the collection **Migration-Exercises.json** from [here](/exercises/ex0/download/Migration-Exercises.json).
2. Open Bruno and select **Import Collection** either from the menu or from the home screen.

<br>![](/exercises/ex0/images/bruno-import-collection.png)

3. On the upcoming dialog, select the type **Bruno Collection**.

<br>![](/exercises/ex0/images/bruno-import-collection-bruno.png)

4. Navigate to the location where you saved the beforehand downloaded collection and select the same.

<br>![](/exercises/ex0/images/bruno-import-collection-file.png)

5. Browse to define a location, eventually create a new folder. Then select **Import**.

<br>![](/exercises/ex0/images/bruno-import-collection-location.png)

### Select environment

As part of the collection, environment parameters have been maintained, that is **client id** and **client secret** to be able to authenticate at the Cloud Integration tenant.

1. If you expand the **Migration Exercises** collection, you should see three requests. In order to be able to select an environment, you need to select any request.

<br>![](/exercises/ex0/images/bruno-import-collection-requests.png)

2. If you select a request for the first time, you need to select the security level. Select **Safe Mode**.

<br>![](/exercises/ex0/images/bruno-open-save-mode.png)

3. By default, no environment has been selected. From the drop down on the upper right corner, select the environment **eu03**.

<br>![](/exercises/ex0/images/bruno-environment-configure.png)


Go back to - [Main page](../../README.md)
