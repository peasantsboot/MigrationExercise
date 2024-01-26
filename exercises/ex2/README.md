# Exercise 2 - Migrate and test a simple SOAP to SOAP scenario

In this exercise, we will create and migrate a simple SOAP to SOAP scenario to call a web service which converts a number into text.
  
## Run the Migration Wizard

Every Integrated Configuration Object (ICO) that can be migrated has an associated template in the migration tooling. Based on these templates, the migration tooling creates equivalent integration flows in the SAP Integration Suite. Let's start with the actual migration.

1. Open your previously created package, and switch to the <b>Artifacts</b> tab, then switch to <b>Edit</b> mode. If you haven't created an integration package yet, navigate to [Create an Integration package](/exercises/ex0/#create-an-integration-package), create a new package and then return. Otherwise, proceed with the next steps.

<br>![image](/exercises/ex2/images/EditPackage.png)
   
2. Switch to tab <b>Artifacts</b> and click on  <b>Migrate</b> to start the migration wizard.

<br>![](/exercises/ex2/images/Migrate.png)
   
3. Select the SAP Process Orchestration system for which the assessment was previously done. For this, expand the Name section and select your system from the drop-down menu. Click <b>Next Step</b> to proceed with configuring the scenario.

<br>![](/exercises/ex2/images/PO_Sys.png)
   
4. Currently, only Integrated Configuration Objects (ICO) are supported. You can use the filter to filter out the list of ICOs and choose the appropriate scenario. Click on <b>Show Filters</b>. 

<br>![image](/exercises/ex2/images/ShowFilters.png)

5. In the filter, fill in **bootcamp** as <b>Namespace</b>. The filter reduces the number of entries in the **Name** drop down list. Choose the interface **SI_NumberConversion_Out** with sender **PIMAS_Sender** from the drop-down list. Click <b>Next Step</b>.

<br>![image](/exercises/ex2/images/ChooseScenario.png)

6. The best-fit template is identified by the migration framework and will be automatically filled in for you. In this case, it will be **P2P_SYNC_0001**. Click <b>Next Step</b>.

<br>![](/exercises/ex2/images/Template.png)

7. In the next step, you can choose whether you create reusable message mapping artifacts or not. In this exercise, let's opt for using local resources. So, **unselect** the **Enable Reusable Message Mapping Artifacts** flag. Then, click <b>Next Step</b>

<br>![](/exercises/ex2/images/NoReusableArtifacts.png)

8. Maintain any **Name** for your integration flow, e.g. following the pattern: **soap_to_soap_sync_userXX where <b>XX</b> is your user id from 00 to 99. Note, that the ID of your integration flow needs to be unique across all integration flows on the tenant. Click on <b>Review</b>.

<br>![](/exercises/ex2/images/Int_Name_Review.png)
    
9. Verify the information and then click on <b>Migrate</b>.

<br>![](/exercises/ex2/images/Final_Migrate.png)
    
10. A new integration flow has been generated within your package. Click on the artifact to take a closer look at each individual step. The required information is automatically populated such as the connection information. Click on <b>View Artifact</b>.

<br> ![image](/exercises/ex2/images/ViewArtifact.png)


## Deploy migrated artifacts

After completing these steps you will be able to deploy the Integration flow and monitor your scenario.
    
1.  Click on the <b>SOAP Adapter</b> and view the <b>Connection</b> details. You can see that the endpoint address has been automatically set based on the integration flow name that you have entered. For this particular scenario, no manual steps need to be carried out. It should run as is. Select <b>Deploy</b> to get the integration flow deployed on the tenant runtime.

<br>![](/exercises/ex2/images/Open_Iflow.png)
    
2. In the upcoming dialog, keep the Runtime Profile as is, i.e., **Cloud Integration**. Then, click **Yes**.

<br>![](/exercises/ex2/images/Deploy_Con.png)

3. Confirm that the deployment has been triggered.

<br>![](/exercises/ex2/images/Deploy_Con2.png)
  
4. You can check the deployment status via the monitor dashboard. Navigate to <b>Monitor > Integrations and APIs</b>.

<br>![](/exercises/ex2/images/Monitor_Int.png)

5. On the monitoring page, select the <b>Manage Integration Content</b> tile.

<br>![](/exercises/ex2/images/ManageIntContentTile.png)
   
6. Your integration flow should be in status <b>Started</b>. From here, you get the endpoint that you need to call to test the scenario. <b>Copy the endpoint</b> as we will use it in the next step.

<br>![](/exercises/ex2/images/Copy_endpoint.png)
   
Now you are all set to test your scenario!

## Verify the Interface via Insomnia

After completing these steps you will be able to test the interface and get the desired result of converting a number into a text.

1. Open Insomnia and click on <b>Use the local Scratch Pad</b>.

<br>![image](/exercises/ex2/images/Insomnia-1.png)  

2. Create a <b>New HTTP-Request</b>.

<br>![image](/exercises/ex2/images/Insomnia-2.png)  

3. <b>Change the Request Method from GET to POST</b>, by clicking the dropdown icon next to GET.  

<br>![image](/exercises/ex2/images/Insomnia-3.png)  

4. <b>Paste the endpoint</b> from you integration flow as URL.  

<br>![image](/exercises/ex2/images/Insomnia-4.png)  

5. Add a <b>Body</b> of type XML.

<br>![image](/exercises/ex2/images/Insomnia-5.png)  

6. Provide following payload:

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

<br>![image](/exercises/ex2/images/Insomnia-6.png)  

7. Switch to tab <b>Auth</b> and choose <b>Basic Auth</b>.

<br>![image](/exercises/ex2/images/Insomnia-7.png)  

8. Provide following credentials:<br>

<br>USERNAME =
```yaml
sb-3009327f-3dc1-4e3e-9853-5bd7c23e221d!b44358|it-rt-cpisuite-europe-03!b18631
```
<br>PASSWORD = 
```yaml 
e507568e-892c-443f-a6ba-4d53f76fecac$wS5Kq2nV25PlNT-U8bh8Yd-HGoBZpO-XW7Za9X3URE0=
```

<br>![image](/exercises/ex2/images/Insomnia-8.png)  

9. Click <b>Send</b>. The request should return HTTP code 200 and a response with the converted text.

<br>![image](/exercises/ex2/images/Insomnia-9.png)  

10. Navigate back to the monitoring page, and click the **Monitor Message Processing** link below the **Artifact Details** of your deployed SOAP to SOAP integration flow.

<br>![image](/exercises/ex2/images/Monitoring_Navigate_To_MPL.png)

11. In the message monitor, you should see one new log in status **Completed**.

<br>![image](/exercises/ex2/images/Monitoring_MPL_Completed.png)

## Summary

Congratulations. You have successfully migrated and tested your scenario now.

Continue to - [Exercise 3 - Migrate and test a SOAP to REST scenario](../ex3/README.md)

