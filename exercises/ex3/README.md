# Exercise 3 - Migrate and Test SOAP to REST Scenario

In this exercise, we will create and migrate a SOAP to REST scenario.	For this particular scenario, not all attributes of the Integrated Configuration Object (ICO) on SAP Process Orchestration could be mapped to the parameters in the integration flow on Cloud Integration, so a couple of manual adjustments will need to be carried out which we will do as a part of the exercise.

## Run the Migration Wizard

1. Open your previously created package, and switch to the <b>Artifacts</b> tab, then switch to <b>Edit</b> Mode. If you haven't created an own integration package yet, navigate to [Create an Integration package](/exercises/ex0/#create-an-integration-package), create a new package and then return. Otherwise, proceed with the next steps.

<br>![](/exercises/ex3/images/1.OpenPreviousPackage.png)

2. Click on <b>Migrate</b> to start the migration wizard.

<br>![](/exercises/ex3/images/2.0_ClickOnMigrate.png)

3.	Select the SAP Process Orchestration system **J2E** from the drop down menu, then click <b>Next Step</b>.

<br>![](/exercises/ex3/images/3.0_Migrate_SelectPO_System.png)

4. In SAP Process Orchestration, only Integrated Configuration Objects (ICO) are supported. So keep the Object Type as **Integrated Configuration**. You can use the filter to filter out the list of ICOs and choose the appropriate scenario. Click on the <b>Selection</b> icon. 

<br>![image](/exercises/ex3/images/ShowFilters.png)

5. In the filter of the upcoming dialog, fill in **bootcamp** as <b>Namespace</b>, then select button **Go** to restrict the list of Items. Choose the interface **SI_Employee_Out** with sender **PIMAS_Sender** from the Items list.

<br>![image](/exercises/ex3/images/ChooseScenario.png)

6. Once you have selected the scenario, click <b>Next Step</b>.

<br>![image](/exercises/ex3/images/ChooseScenarioNext.png)

7.	The best fit pattern **Point-to-Point Synchronous** is proposed. Click <b>Next Step</b>.

<br>![](/exercises/ex3/images/P2PSyncPattern.png)

8. In the next step, you can choose whether you create reusable message mapping artifacts or not. In this exercise, let's opt for using local resources. So, unselect the **Enable Reusable Message Mapping Artifacts** flag. Then, click **Next Step**.

<br>![](/exercises/ex3/images/3.4_Migrate_SelectPO_NoReuse.png)

9.	Maintain a **Name** for your integration flow, e.g., following the pattern **soap_to_rest_sync_userXX** where <b>XX</b> is your user number from 00 to 99. Then, click on <b>Review</b>.

<br>![image](/exercises/ex3/images/ex3-6.png)

10.	Verify the information and click on <b>Migrate</b>.

<br>![image](/exercises/ex3/images/ex3-7.png)

11.	Again, the integration flow will be generated within your integration package. As you can see from the summary page, the REST receiver adapter on SAP Process Orchestration has been mapped to the HTTP adapter in Cloud Integration. Click on  **View Artifact** to take a closer look. 

<br>![](/exercises/ex3/images/4.0_Migration_Success.png)

**Note**: for this particular scenario, not all attributes of the ICO on SAP Process Orchestration could be mapped to the parameters in the integration flow on Cloud Integration, so a couple of manual adjustments need to be carried out. The attribute mapping will be improved with future increments of the migration tool so that manual interaction is reduced to a bare minimum.

12. Switch to <b>Edit</b> mode at the top right corner.

<br>![image](/exercises/ex3/images/ex3-13.png)

13. In the integration flow properties, switch to tab **Runtime Configuration**, and add the following **Namespace Mapping**. Once done, click <b>Save</b> and then <b>Deploy</b> to deploy the integration flow.

```yaml
xmlns:ns0=http://pi-elevation.bootcamp.com
```

<br>![](/exercises/ex3/images/5.0_View_iFlow_Changes_to_Make.png)


14. In the upcoming dialog, select the **Cloud Integration** runtime and select **Yes**. Then, confirm the next dialog.

<br>  ![image](/exercises/ex3/images/ex3-17a.png)

15. You can check the deployment status via the monitor dashboard. Navigate to **Monitor > Integrations and APIs**. On the monitoring page, select the <b>Manage Integration Content</b> tile.

<br>   ![image](/exercises/ex3/images/ex3-18.png)
   
16. Your integration flow should be in status <b>Started</b>. From here, you get the endpoint that you need to call to test the scenario. <b>Copy the endpoint</b> to the clipboard as we will use it in the next step.

<br>![image](/exercises/ex3/images/ex3-19.png)


## Verify the Interface

After completing these steps you will be able to test the interface.

**Note**: You have two options to execute and test your integration scenario:
- The quickest option is to use the Bruno API client application for which we have provided a collection with pre-configured sample request. As a prerequisite to test your integration scenario using the Bruno API client, you should have gone through [Setup Bruno API client](../ex0#setup-bruno-api-client/). If not, do the setup, then come back and proceed with [option 1](#option-1-using-bruno-api-client).
- If you like to use your own tool, we have described in detail how to setup a sample request incl. body and authentication. This is described in [option 2](#option-2-using-your-own-api-client).

### Option 1: Using Bruno API client

1. Open the Bruno application on your laptop, expand the **Migration Exercises** collection and select the POST request **Exercise 3 - P2P SOAP to REST**. Paste the copied end point from the clipboard into the URL field or simply replace the **XX** in the URL with the id provided to you. Ensure that the **eu03** environment has been selected. Then trigger a message by selecting the **Send Request** button on the upper right.

<br>![image](/exercises/ex3/images/bruno-request-send.png)

2. Upon success, you will receive **200 OK** status.

<br>![image](/exercises/ex3/images/bruno-request-successful.png)

3. Navigate back to the monitoring page, and click the **Monitor Message Processing** link below the **Artifact Details** of your deployed SOAP to REST integration flow.

<br>![image](/exercises/ex3/images/ex3-20.png)

4. In the message monitor, you should see one new log in status **Completed**.

<br>![image](/exercises/ex3/images/ex3-21.png)

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
        <pi:MT_Employee_REQ>
            <employee_name>John Doe 124</employee_name>
            <employee_salary>320800</employee_salary>
            <employee_age>60</employee_age>
            <profile_image></profile_image>
        </pi:MT_Employee_REQ>
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

Congratulations. You have successfully migrated and tested your SOAP to REST scenario.

Continue to - [Exercise 4 - Migrate and test a Content-Based-Router scenario](../ex4/README.md)

