# Exercise 4 - Migrate and Test a Content-Based-Router Scenario

In this exercise, we will create and migrate a Content-Based-Router scenario, i.e., the source Integrated Configuration Object contains xpath conditions that are carried out to determine the receiver that the message should be sent to.

## Run the Migration Wizard

1. Open your previously created package, and switch to the <b>Artifacts</b> tab, then switch to <b>Edit</b> Mode. If you haven't created an own integration package yet, navigate to [Create an Integration package](/exercises/ex0/#create-an-integration-package), create a new package and then return. Otherwise, proceed with the next steps.

<br>![](/exercises/ex4/images/04_01.png)

2. Click on <b>Migrate</b> to start the migration wizard.

<br>![](/exercises/ex4/images/04_02.png)

3.	Select the SAP Process Orchestration system **J2E** from the drop down menu, then click <b>Next Step</b>.

<br>![](/exercises/ex4/images/04_03.png)

4.	Click on <b>Show Filters</b> and fill in **bootcamp** for the **Namespace**. Choose the interface **SI_Employee_Out** with sender **CBR_blah** from the drop-down list. Click <b>Next Step</b>.

<br>![](/exercises/ex4/images/04_04.png)

5.	The best fit template is identified. This time, the template **P2P_SYNC_JSON_REC_0001** is proposed. Click <b>Next Step</b>.

<br>![](/exercises/ex4/images/04_05.png)

6. In the next step, you can choose whether you create reusable message mapping artifacts or not. In this exercise, let's opt for using local resources. So, select the **Enable Reusable Message Mapping Artifacts** flag. Then, click **Next Step**.

<br>![](/exercises/ex4/images/04_06.png)

7. xxxx

<br>![](/exercises/ex4/images/04_07.png)

7.	Maintain a **Name** for your integration flow, e.g., following the pattern **soap_to_rest_sync_userXX** where <b>XX</b> is your user number from 00 to 99. Then, click on <b>Review</b>.

<br>![](/exercises/ex4/images/04_08.png)

8.	Verify the information and click on <b>Migrate</b>.

<br>![](/exercises/ex4/images/04_09.png)

9.	Again, the integration flow will be generated within your integration package. As you can see from the summary page, the REST receiver adapter on SAP Process Orchestration has been mapped to the HTTP adapter in Cloud Integration. Click on  **View Artifact** to take a closer look. 

<br>![](/exercises/ex4/images/04_10.png)

10.	For this particular scenario, not all attributes of the ICO on SAP Process Orchestration could be mapped to the parameters in the integration flow on Cloud Integration, so a couple of manual adjustments need to be carried out.

Note, the attribute mapping will be improved with future increments of the migration tool so that manual interaction is reduced to a bare minimum.

Click on <b>Configure</b>.

<br>![](/exercises/ex4/images/04_11.png)

11. Switch to tab <b>More</b> and select **XML to JSON Converter** as Type.

<br>![](/exercises/ex4/images/04_12.png)

12. Enable **Suppress JSON Root Element** and click **Save**.

<br>![](/exercises/ex4/images/04_13.png)

13. Press <b>Close</b> to close the Message box and <b>close</b> the configure Pop-Up as well.

<br>![](/exercises/ex4/images/04_14.png)

14. Switch to <b>Edit</b> mode at the top right corner

<br>![](/exercises/ex4/images/04_15.png)

15. In the integration flow properties, switch to tab **Runtime Configuration**, and add the following **Namespace Mapping**:

```yaml
xmlns:ns0=http://pi-elevation.bootcamp.com
```

<br>![](/exercises/ex4/images/04_16.png)

16.	In the HTTP connection of the **Request Reply** step, verify that the parameters are automatically set based on the receiver channel of the ICO. The values for the Address, the Authentication, and the Credential Name should be preset. Ensure that Authentication is set to **Basic**, and the Credential Name should be **PIMAS_Demo**. If not, change the parameters accordingly.

<br>![](/exercises/ex4/images/04_17.png)

17.	Next, click on the  **JSON to XML Converter** and switch to the **Processing** tab. Select the previously created **Namespace Mapping** by clicking **Select**. Furthermore, enter the **Name** of the root element as follows:

```yaml
MT_Employee_RESP
```

<br>![](/exercises/ex4/images/04_18.png)

18.	Click <b>Save</b> and then <b>Deploy</b> to deploy the integration flow.

<br>![](/exercises/ex4/images/04_19.png)

19. You can check the deployment status via the monitor dashboard. Navigate to **Monitor > Integrations and APIs**

<br>![](/exercises/ex4/images/04_20.png)

20. On the monitoring page, select the <b>Manage Integration Content</b> tile.

<br>![](/exercises/ex4/images/04_21.png)
   
21. Your integration flow should be in status <b>Started</b>. From here, you get the endpoint that you need to call to test the scenario. <b>Copy the endpoint</b> to the clipboard as we will use it in the next step.

<br>![](/exercises/ex4/images/04_22.png)


## Verify the Interface via Insomnia

1.	Open Insomnia and <b>duplicate</b> the Request you created in exercise 2. 

<br>![image](/exercises/ex4/images/Insomnia-1.png)

2. Maintain a new name and click <b>Create</b>.

<br>![image](/exercises/ex4/images/Insomnia-2.png)

3. <b>Replace the URL</b> with the endpoint of your new integration flow.

<br>![image](/exercises/ex4/images/Insomnia-3.png)

4. Ensure that the following credentials are maintained (note, should be the case as you copied the request):

<br>USERNAME =
```yaml
sb-3009327f-3dc1-4e3e-9853-5bd7c23e221d!b44358|it-rt-cpisuite-europe-03!b18631
```
<br>PASSWORD = 
```yaml 
e507568e-892c-443f-a6ba-4d53f76fecac$wS5Kq2nV25PlNT-U8bh8Yd-HGoBZpO-XW7Za9X3URE0=
```

5. Replace the XML Payload with the following value:

  ```xml
<pi:MT_SalesOrder_0001 xmlns:pi="http://pi-elevation.bootcamp.com">
    <salesOrder>
        <orderNumber>00005</orderNumber>
        <orderDate>10/01/2023</orderDate>
        <customer>
            <firstName>Amruta</firstName>
            <lastName>Kamble</lastName>
            <street>Hauptstrasse</street>
            <number>89</number>
            <country>US</country>
        </customer>
        <items>
            <itemNumber>Test</itemNumber>
            <material>Test_material</material>
            <quantity>5</quantity>
            <price>550</price>
        </items>
    </salesOrder>
</pi:MT_SalesOrder_0001>
```

<br>![image](/exercises/ex4/images/Insomnia-4.png)

6. Click <b>Send</b>. The response should be "200 OK".

<br>![image](/exercises/ex4/images/Insomnia-5.png)

7. Navigate back to the monitoring page, and click the **Monitor Message Processing** link below the **Artifact Details** of your deployed SOAP to REST integration flow.

<br>![](/exercises/ex4/images/04_23.png)

8. In the message monitor, you should see one new log in status **Completed**.

<br>![](/exercises/ex4/images/04_24.png)

## Summary

Congratulations. You have successfully migrated and tested your Content-Based-Router scenario.

