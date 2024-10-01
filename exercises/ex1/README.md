# Exercise 1 - Migration Assessment

In this exercise, you will learn how to migrate your existing integration scenarios to SAP Integration Suite with the Migration Assessment capability of SAP Integration Suite. This offering helps you estimate the technical efforts involved in the migration process and evaluates how various integration scenarios might be migrated.

## Launch the Migration Assessment page

1. If you haven't done so, login to the tenant provided to you with your user **userXX** and the credentials provided to you.
      
2. In the SAP Integration Suite landing page, scroll down to Capabilities, and select **Create Requests** from the **Assess Migration Scenarios** tile.

<br>![](/exercises/ex1/images/Access_Migration_Scenarios.png)
   
## Checkout the Configuration

After completing these steps you will be able to test the connection to your SAP Process Orchestration system, and understand what rules the assessment is based on.

<b>Note:</b> For this exercise, the connection to a cloud connector has been already established.

1. Navigate to **Settings** and Select **J2E** System to view the details. For this exercise, the system setup is already done and you can click on <b>Test Connection</b> to check the connection to the SAP Process Orchestration system.

<br>![](/exercises/ex1/images/View_PO_System.png)

2. In the Migration Assessment Application, navigate to **Configure > Rules**. Here you can find a list of rules predefined by SAP. Rules are a set of characteristics according to which the application evaluates whether an integration scenario can be migrated and what effort you can expect. As an example, select the rule **SenderAdapterType**.

**Note:** Currently, you can’t add custom rules or edit the standard rules. You can only view the standard rules.

<br>![](/exercises/ex1/images/Configure_Rule.png)  

3. Open the variant **MAIN_SenderAdapterType**

<br>![](/exercises/ex1/images/MainSenderAdapterType.png)

Here, you can see all the parameters of the rules, such as Rule Match Value, Assessment Category, and the Weight assigned to each rule match value. Based on these weights, the application calculates the estimated effort, which means that some parameters, and therefore rules, have a bigger influence on the final estimation than others.

 
## Reuse an existing Data Extraction Request

Usually, the data extraction takes some time depending on the number of integration scenarios configured on SAP Process Orchestration. For our exercise, we have configured just a handful of scenarios in the SAP Process Orchestration system, so that the extraction runs faster compared to a real customer system.
Nevertheless, you do not need to run an extraction, instead you can reuse the already created and completed Data Extraction Request. If by accident the data extraction has been deleted, you can create a new one.

1.	In the Migration Assessment Application, navigate to **Request** and select the **Data Extractions** tile.

<br>![](/exercises/ex1/images/Request_Data_Ext.png)
  	
2. As you can see, we have already run the data extraction. The status is **Completed** with warnings since some of the integration scnearios have not been fully extracted. From the **Actions** menu, you can enter the extraction dashboard and the logs to get more details about the extraction status.

<br>![](/exercises/ex1/images/Reuse_Data_Ext.png)
   
## Create a Scenario Evaluation Request

Assess your integration scenarios using the information from the data extraction requests. The prerequisite is that you have at least one data extraction request in status <b>Completed</b>.

1. Navigate to **Request**.

<br>![](/exercises/ex1/images/Navigate_To_Request.png)

2. Select the **Scenario Evaluation** tile.

<br>![](/exercises/ex1/images/Request_Scenario_Eval.png)
   
3. Select <b>Create</b>.

<br>![](/exercises/ex1/images/Select_Create.png)
   
4. Enter a Request Name such as **UserXX-Evaluation** where **XX** is the user id assigned to you and choose the existing Data Extraction Request from the drop-down. For this specific run of your scenario evaluation, enter an Evaluation Run Name such as **UserXX-Evaluation-Run** (where **XX** is your user from 00 to 99) and a Description.

<br>![](/exercises/ex1/images/Create_Sce_Eval.png)

<b>Note:</b> You usually run a new evaluation request for a new data extraction whereas you run a new evaluation run whenever the assessment rules have been changed.

5. The new request appears in the list of scenario evaluation requests in Status <b>In Progress</b>.

<br>![](/exercises/ex1/images/Evaluation_In_Progress.png)
   
6. Refresh and wait until the request changes to status <b>Completed</b>. Different Actions can be performed for a scenario evaluation request.

<br>![](/exercises/ex1/images/Complete_Sce_Eval.png)
   
## View Generated Reports

Access and download analysis of your scenario evaluation runs with details specific to your integration scenarios, for example, adapters and an overview of the rules used in the evaluation. Further, you can download details about the latest evaluation run in one of two formats <b>.xlsx</b> file and <b>.pdf</b> file.

1. Let’s start with opening the dashboard. Select the <b>Open Dashboard</b> icon.

<br>![](/exercises/ex1/images/Open_Dash.png)
   
2. The dashboard shows you an analysis of your scenario evaluation runs with details specific to your integration scenarios, i.e., scenarios grouped by assessment categories, scenarios grouped by rough t-shirt effort estimation, statistics about adapters used in your integration scenarios, etc. You can switch between the data of all runs performed for the scenario evaluation request so far (note, if you haven’t triggered another analysis, there is only one entry in the drop-down menu).

<br>![](/exercises/ex1/images/Overview_Dash.png)

3. Scoll down a bit. This shows you the statistics of the modernization recommendations. Instead of pure lift and shift, alternative implementation options are recommended in terms of integration styles, protocols, and security.

<br>![](/exercises/ex1/images/Overview_Recommendations.png)
   
4. Switch to the <b>Integration Scenarios</b> tab, and you see the list of all integration scenarios including effort size and assessment category.

<br>![](/exercises/ex1/images/Dashboard.png)
   
5. Switch back to the list of <b>Scenario Evaluation</b> requests. From the Additional Options menu, you can select <b>Trigger Analysis</b> to schedule a new evaluation run based on the most recent data extraction. Let's skip this for now as data did not change. Furthermore, you have the option to download details about the latest evaluation run either in an Excel format or as a PDF file.

<br>![](/exercises/ex1/images/Eval_Actions.png)
     
6. The option as .xlsx file lists all integration scenarios that were part of the request with migration effort and status as well as the rules applied to them. In addtion, you find a tab providing more details about the modernization recommendations.

<br>![](/exercises/ex1/images/Excel.png)

7. The option as .pdf file features the previously mentioned details about the integration scenarios while also providing a written summary of adapters and the assessment in general, with charts and tables as visual aids. It also maps the t-shirt effort estimation to effort estimation in person days based on project experience. This file is suited as a summarizing report, that can be used for example for management.

<br>![](/exercises/ex1/images/pdf.png)

## Summary

Once you have evaluated the migration possibility using the Migration Assessment capability of SAP Integration Suite, you are all set to migrate an integration artifact with the Migration tool.

Continue to - [Exercise 2 - Migrate and test a simple P2P scenario](../ex2/README.md)
