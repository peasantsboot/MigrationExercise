# Exercise 3 - Migrate and Test SOAP to REST Scenario

In this exercise, we will create and migrate a SOAP to REST scenario.	For this particular scenario, not all attributes of the Integrated Configuration Object (ICO) on SAP Process Orchestration could be mapped to the parameters in the integration flow on Cloud Integration, so a couple of manual adjustments will need to be carried out which we will do as a part of the exercise.

1. Open your previously created package, and switch to the <b>Artifacts</b> tab, then switch to <b>Edit</b> Mode. If you haven't run through the previous step, you first need to create an own integration package. In this case, navigate to [Create an Integration package](/exercises/ex2/#create-an-integration-package), create a new package and then return. Otherwise, proceed with the next steps.

<br>![](/exercises/ex3/images/1.OpenPreviousPackage.png)

2. Click on <b>Migrate</b> to start the migration wizard.

<br>![](/exercises/ex3/images/2.0_ClickOnMigrate.png)

3.	Select the SAP Process Orchestration system **J2E** from the drop down menu, then click <b>Next Step</b>.

<br>![](/exercises/ex3/images/3.0_Migrate_SelectPO_System.png)

4.	Click on <b>Show Filters</b> and fill in **bootcamp** for the **Namespace**. Choose the interface **SI_Employee_Out** with sender **PIMAS_Sender** from the drop-down list. Click <b>Next Step</b>.

<br>![](/exercises/ex3/images/3.1_Migrate_SelectPO_Artifacts.png)

5.	The best fit template is identified. This time, the template **P2P_SYNC_JSON_REC_0001** is proposed. Click <b>Next Step</b>.

<br>![](/exercises/ex3/images/3.2_Migrate_SelectPO_Template.png)

6. In the next step, you can choose whether you create reusable message mapping artifacts or not. In this exercise, let's opt for using local resources. So, unselect the **Enable Reusable Message Mapping Artifacts** flag. Then, click **Next Step**.

<br>![](/exercises/ex3/images/3.4_Migrate_SelectPO_NoReuse.png)

7.	Maintain a **Name** for your integration flow, e.g., following the pattern **soap_to_rest_sync_userXX** where <b>XX</b> is your user number from 00 to 99. Then, click on <b>Review</b>.

<br>![image](/exercises/ex3/images/ex3-6.png)

8.	Verify the information and click on <b>Migrate</b>.

<br>![image](/exercises/ex3/images/ex3-7.png)

9.	Again, the integration flow will be generated within your integration package. As you can see from the summary page, the REST receiver adapter on SAP Process Orchestration has been mapped to the HTTP adapter in Cloud Integration. Click on  **View Artifact** to take a closer look. 

<br>![](/exercises/ex3/images/4.0_Migration_Success.png)

10.	For this particular scenario, not all attributes of the ICO on SAP Process Orchestration could be mapped to the parameters in the integration flow on Cloud Integration, so a couple of manual adjustments need to be carried out.

Note, the attribute mapping will be improved with future increments of the migration tool so that manual interaction is reduced to a bare minimum.

Click on <b>Configure</b>.

<br>![image](/exercises/ex3/images/ex3-9.png)

11. Switch to tab <b>More</b> and select **XML to JSON Converter** as Type.

<br>![image](/exercises/ex3/images/ex3-10.png)

12. Enable **Suppress JSON Root Element** and click **Save**.

<br>![image](/exercises/ex3/images/ex3-11.png)

13. Press <b>Close</b> to close the Message box and <b>close</b> the configure Pop-Up as well.

![image](/exercises/ex3/images/ex3-12.png)

14. Switch to <b>Edit</b> mode at the top right corner

<br>![image](/exercises/ex3/images/ex3-13.png)

15. In the integration flow properties, switch to tab **Runtime Configuration**, and add the following **Namespace Mapping**:

```yaml
xmlns:ns0=http://pi-elevation.bootcamp.com
```

<br>![](/exercises/ex3/images/5.0_View_iFlow_Changes_to_Make.png)

16.	In the HTTP connection of the **Request Reply** step, verify that the parameters are automatically set based on the receiver channel of the ICO. The values for the Address, the Authentication, and the Credential Name should be preset. Ensure that Authentication is set to **Basic**, and the Credential Name should be **PIMAS_Demo**. If not, change the parameters accordingly.

<br>![](/exercises/ex3/images/5.2_Edit_iFlow_Request_Reply.png)

17.	Next, click on the  **JSON to XML Converter** and switch to the **Processing** tab. Select the previously created **Namespace Mapping** by clicking **Select**. Furthermore, enter the **Name** of the root element as follows:

```yaml
MT_Employee_RESP
```

<br>![](/exercises/ex3/images/5.3_Edit_iFlow_JSON_to_XML.png)

18.	Click <b>Save</b> and then <b>Deploy</b> to deploy the integration flow.

<br>  ![image](/exercises/ex3/images/ex3-17.png)

19. You can check the deployment status via the monitor dashboard. Navigate to **Monitor > Integrations and APIs**

<br>   ![image](/exercises/ex3/images/ex3-17a.png)

20. On the monitoring page, select the <b>Manage Integration Content</b> tile.

<br>   ![image](/exercises/ex3/images/ex3-18.png)
   
21. Your integration flow should be in status <b>Started</b>. From here, you get the endpoint that you need to call to test the scenario. <b>Copy the endpoint</b> to the clipboard as we will use it in the next step.

<br>![image](/exercises/ex3/images/ex3-19.png)


## Verify the Interface via Insomnia

1.	Open Insomnia and <b>duplicate</b> the Request you created in exercise 2. 

<br>![image](/exercises/ex3/images/Insomnia-1.png)

2. As name provide **Employee** and click <b>Create</b>.

<br>![image](/exercises/ex3/images/Insomnia-2.png)

3. <b>Replace the URL</b> with the endpoint of your new integration flow.

<br>![image](/exercises/ex3/images/Insomnia-3.png)

4. Replace the XML Payload with the following value:

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

<br>![image](/exercises/ex3/images/Insomnia-4.png)

5. Ensure that the following credentials are maintained (note, should be the case as you copied the request):

<br>USERNAME =
```yaml
sb-3009327f-3dc1-4e3e-9853-5bd7c23e221d!b44358|it-rt-cpisuite-europe-03!b18631
```
<br>PASSWORD = 
```yaml 
e507568e-892c-443f-a6ba-4d53f76fecac$wS5Kq2nV25PlNT-U8bh8Yd-HGoBZpO-XW7Za9X3URE0=
```

6. Click <b>Send</b>. The response should be "200 OK".

<br>![image](/exercises/ex3/images/Insomnia-5.png)

7. Navigate back to the monitoring page, and click the **Monitor Message Processing** link below the **Artifact Details** of your deployed SOAP to REST integration flow.

<br>![image](/exercises/ex3/images/ex3-20.png)

8. In the message monitor, you should see one new log in status **Completed**.

<br>![image](/exercises/ex3/images/ex3-21.png)

## Summary

Congratulations. You have successfully migrated and tested your SOAP to REST scenario.

Continue to - [Exercise 4 - Migrate and test a Content-Based-Router scenario](../ex4/README.md)

