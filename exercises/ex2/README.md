# Exercise 2 - Migrate and test a simple SOAP to SOAP scenario

In this exercise, we will create and migrate a simple SOAP to SOAP scenario to call a web service which converts a number into text.
  
## Run the Migration Wizard

Every Integrated Configuration Object (ICO) that can be migrated has an associated pattern in the migration tooling. Based on these patterns, the migration tooling creates equivalent integration flows in the SAP Integration Suite. Let's start with the actual migration.

1. Open your previously created package, and switch to the <b>Artifacts</b> tab, then switch to <b>Edit</b> mode. If you haven't created an integration package yet, navigate to [Create an Integration package](/exercises/ex0/#create-an-integration-package), create a new package and then return. Otherwise, proceed with the next steps.

<br>![image](/exercises/ex2/images/EditPackage.png)
   
2. Click on  <b>Migrate</b> to start the migration wizard.

<br>![](/exercises/ex2/images/Migrate.png)
   
3. Select the SAP Process Orchestration system for which the assessment was previously done. For this, expand the Name section and select your system from the drop-down menu. Click <b>Next Step</b> to proceed with configuring the scenario.

<br>![](/exercises/ex2/images/PO_Sys.png)
   
4. In SAP Process Orchestration, only Integrated Configuration Objects (ICO) are supported. So keep the Object Type as **Integrated Configuration**. You can use the filter to filter out the list of ICOs and choose the appropriate scenario. Click on the <b>Selection</b> icon. 

<br>![image](/exercises/ex2/images/ShowFilters.png)

5. In the filter of the upcoming dialog, fill in **bootcamp** as <b>Namespace</b>, then select button **Go** to restrict the list of Items. Choose the interface **SI_NumberConversion_Out** with sender **PIMAS_Sender** from the Items list.

<br>![image](/exercises/ex2/images/ChooseScenario.png)

6. Once you have selected the scenario, click <b>Next Step</b>.

<br>![image](/exercises/ex2/images/ChooseScenarioNext.png)

7. The best-fit pattern is identified by the migration framework and will be automatically filled in for you. In this case, it will be **Point-to-Point Synchronous**. Click <b>Next Step</b>.

<br>![](/exercises/ex2/images/P2PSyncPattern.png)

8. In the next step, you can choose whether you create reusable message mapping artifacts or not. In this exercise, let's opt for using local resources. So, **unselect** the **Enable Reusable Message Mapping Artifacts** flag. Then, click <b>Next Step</b>

<br>![](/exercises/ex2/images/NoReusableArtifacts.png)

9. Maintain any **Name** for your integration flow, e.g. following the pattern: **soap_to_soap_sync_userXX** where <b>XX</b> is your user id from 00 to 99. Note, that the ID of your integration flow needs to be unique across all integration flows on the tenant. Click on <b>Review</b>.

<br>![](/exercises/ex2/images/Int_Name_Review.png)
    
10. Verify the information and then click on <b>Migrate</b>.

<br>![](/exercises/ex2/images/Final_Migrate.png)
    
11. A new integration flow has been generated within your package. Click on the artifact to take a closer look at each individual step. The required information is automatically populated such as the connection information. Click on <b>View Artifact</b>.

<br> ![image](/exercises/ex2/images/ViewArtifact.png)


## Deploy migrated artifacts

After completing these steps you will be able to deploy the Integration flow and monitor your scenario.
    
1.  Click on the <b>SOAP Adapter</b> and view the <b>Connection</b> details. You can see that the endpoint address has been automatically set based on the integration flow name that you have entered. For this particular scenario, no manual steps need to be carried out. It should run as is. Select <b>Deploy</b> to get the integration flow deployed on the tenant runtime.

<br>![](/exercises/ex2/images/Open_Iflow.png)
    
2. In the upcoming dialog, keep the Runtime Profile as is, i.e., **Cloud Integration**. Then, click **Yes**.

<br>![](/exercises/ex2/images/Deploy_Con.png)

3. Confirm that the deployment has been triggered.

<br>![](/exercises/ex2/images/Deploy_Con2.png)
  
4. You can check the deployment status via the monitor dashboard. Navigate to <b>Monitor > Integrations and APIs</b>. On the monitoring page, select the <b>Manage Integration Content</b> tile.

<br>![](/exercises/ex2/images/ManageIntContentTile.png)
   
5. Your integration flow should be in status <b>Started</b>. From here, you get the endpoint that you need to call to test the scenario. <b>Copy the endpoint</b> as we will use it in the next step.

<br>![](/exercises/ex2/images/Copy_endpoint.png)
   
Now you are all set to test your scenario!

## Verify the Interface

After completing these steps you will be able to test the interface and get the desired result of converting a number into a text.

**Note**: You have two options to execute and test your integration scenario:
- The quickest option is to use the Bruno API client application for which we have provided a collection with pre-configured sample request. As a prerequisite to test your integration scenario using the Bruno API client, you should have gone through [Setup Bruno API client](../ex0#setup-bruno-api-client/). If not, do the setup, then come back and proceed with [option 1](#option-1-using-bruno-api-client).
- If you like to use your own tool, we have described in detail how to setup a sample request incl. body and authentication. This is described in [option 2](#option-2-using-your-own-api-client).

### Option 1: Using Bruno API client

1. Open the Bruno application on your laptop, expand the **Migration Exercises** collection and select the POST request **Exercise 2 - P2P SOAP to SOAP**. Paste the copied end point from the clipboard into the URL field or simply replace the **XX** in the URL with the id provided to you. Ensure that the **eu03** environment has been selected. Then trigger a message by selecting the **Send Request** button on the upper right.

<br>![image](/exercises/ex2/images/Bruno_SendRequest.png)  

2. Upon success, you will receive **200 OK** status and the converted number as a response.

<br>![image](/exercises/ex2/images/Bruno_SendRequest_Successful.png) 

3. Navigate back to the monitoring page, and click the **Monitor Message Processing** link below the **Artifact Details** of your deployed SOAP to SOAP integration flow.

<br>![image](/exercises/ex2/images/Monitoring_Navigate_To_MPL.png)

4. In the message monitor, you should see one new log in status **Completed**.

<br>![image](/exercises/ex2/images/Monitoring_MPL_Completed.png)

Scroll down to proceed to the next exercise.

### Option 2: Using your own API client

Skip this option if you have used the Bruno API client to test the integration scenario.

1. Open your own API client and create a new **POST** request.

2. Paste the copied end point from the clipboard into the URL field.

3. Define the payload of type XML as follows.

```xml
<soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:pi="http://pi-elevation.bootcamp.com">
    <soapenv:Header />
    <soapenv:Body>
        <pi:MT_NumberConversion_REQ>
            <number>1389</number>
        </pi:MT_NumberConversion_REQ>
    </soapenv:Body>
</soapenv:Envelope>
```

4. To authenticate to the Cloud Integration runtime, select **Basic Authentication** and maintain the credentials as follows.

<br>User name =
```yaml
sb-3009327f-3dc1-4e3e-9853-5bd7c23e221d!b44358|it-rt-cpisuite-europe-03!b18631
```
<br>Password = 
```yaml 
e507568e-892c-443f-a6ba-4d53f76fecac$wS5Kq2nV25PlNT-U8bh8Yd-HGoBZpO-XW7Za9X3URE0=
```

5.	Trigger a message. Upon success, you will receive **200 OK** status as a response.
6.	For monitoring the message in the message monitor of SAP Integration Suite, see steps 3 to 4 in [option 1](#option-1-using-bruno-api-client).

## Summary

Congratulations. You have successfully migrated and tested your scenario now.

Continue to - [Exercise 3 - Migrate and test a SOAP to REST scenario](../ex3/README.md)

