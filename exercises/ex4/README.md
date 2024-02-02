# Exercise 4 - Migrate and Test a Content-Based-Router Scenario

In this exercise, we will create and migrate a Content-Based-Router scenario, i.e., the source Integrated Configuration Object (ICO) contains xpath conditions that are carried out to determine the receiver that the message should be sent to. In our case. the xpath conditions check the country code, in case of DE the message is sent to receiver 1, in case of IN to receiver 2 and in case of US to receiver 3. If the condition is not met, the message runs into an error. Furthermore, we will use reusable aritfacts in Cloud Integration, i.e., a message mapping and a function library which have been already uploaded from the SAP Process Orchestration system.

## Run the Migration Wizard

1. Open your previously created package, and switch to the <b>Artifacts</b> tab, then switch to <b>Edit</b> Mode. If you haven't created an own integration package yet, navigate to [Create an Integration package](/exercises/ex0/#create-an-integration-package), create a new package and then return. Otherwise, proceed with the next steps.

<br>![](/exercises/ex4/images/04-01.png)

2. Click on <b>Migrate</b> to start the migration wizard.

<br>![](/exercises/ex4/images/new-04-09.png)

3.	In the migration wizard, select the SAP Process Orchestration system **J2E** from the drop down menu, then click <b>Next Step</b>.

<br>![](/exercises/ex4/images/04-05.png)

4.	In the next step, click on <b>Show Filters</b>.

<br>![](/exercises/ex4/images/04-06.png)

5.	Fill in **CBR_S02** for the **Sender Communication Component**, and choose the interface **SI_SalesOrder_Out** with sender **CBR_S02** from the drop-down list. Click <b>Next Step</b>.

<br>![](/exercises/ex4/images/04-07.png)

6.	The best fit templates are identified. Beside the default template, you get two migration templates proposed. It is not possible to automatically identify which kind of pattern apply here. Whether your ICO is of pattern Content Based Routing or Recipient List depends on the xpath conditions to determine the receivers. If the xpaths conditions are exclusive, i.e., only one condition applies and as such the message is sent to only one receiver, then the ICO is of pattern Content Based Routing. Otherwise, if many conditions may apply for a message, and hence the message may be sent to multiple receivers, then the ICO is of pattern Recipient List. In our case, select the template **CBR_ASYNC_0001**.

<br>![](/exercises/ex4/images/04-08.png)

7.	Click <b>Next Step</b>.

<br>![](/exercises/ex4/images/04-09.png)

8. In the next step, you can choose whether you create reusable message mapping artifacts or not. In this exercise, we like to reuse artifacts which have been already uploaded to Cloud Integration. So, keep the **Enable Reusable Message Mapping Artifacts** flag selected. As you can see, you have the option to select the integration package where the reusable artifact should be uploaded to. By default, the integration package is preset from where you started the migration wizard. Let's change the default setting.

<br>![](/exercises/ex4/images/new-04-10.png)

9. In the upcoming dialog, select the integration package ****

<br>![](/exercises/ex4/images/new-04-11.png)

10. The message mapping hasn't been uploaded yet, so the Import Method is set to **Create**. Click **Next Step**.

<br>![](/exercises/ex4/images/new-04-12.png)

11. In the next step, you can see the message mapping resources. Before we are able to continue, you need to select the function library container that the function library should be added to. Select **Select** next to the **Function Library** type.

<br>![](/exercises/ex4/images/04-11.png)

12. In the upcoming dialog, select your beforehand created function library container, and click **Select**.

<br>![](/exercises/ex4/images/04-12.png)

13. Click **Next Step**.

<br>![](/exercises/ex4/images/04-13.png)

14.	Maintain a **Name** for your integration flow, e.g., following the pattern **cbr_userXX** where <b>XX</b> is your user number from 00 to 99. Then, click on <b>Review</b>.

<br>![](/exercises/ex4/images/04-14.png)

15.	Verify the information and click on <b>Migrate</b>.

<br>![](/exercises/ex4/images/04-15.png)

16.	Again, the integration flow will be generated within your integration package. Click on  **View Artifact** to take a closer look. 

<br>![](/exercises/ex4/images/04-17.png)

17.	As you can see from the generated integration flow model, a router with four routes have been added: three routes for the three receivers, and one route for the exception case in case that no xpath condition is met. Navigate back to your package.

<br>![](/exercises/ex4/images/04-18.png)

18. As you can see from the list of artifacts, besides the integration flow a message mapping has been created as well. Let's first open your function library container by clicking the same.

<br>![](/exercises/ex4/images/04-19.png)

19. You can see that a function library with one user defined function has been added. Click **Deploy**.

<br>![](/exercises/ex4/images/04-20.png)

20. Confirm the upcoming dialog.

21. A toast message will eventually appear informing you that the function libraries artifact has been successfully deployed. Navigate back to your package.

<br>![](/exercises/ex4/images/04-22.png)

22. Next, deploy the generated message mapping **MM_SalesOrderWithFuncLib** by selecting the entry **Deploy** from the action menu.

<br>![](/exercises/ex4/images/04-23.png)

23.	Before deploying the generated integration flow, we first need to configure the sender and receiver adapters. Select the entry **Configure** from the action menu of the integration flow **cbr_userXX** with **XX** your user number.

<br>![](/exercises/ex4/images/04-26.png)

24.	In the upcoming dialog, on tab **Sender**, maintain the endpoint of your generated integration flow. The endpoint needs to be unique within the tenant, so append **/userXX** to the Address with **XX** the user number assigned to you.

```yaml
/cbr/s02/userXX
```

<br>![](/exercises/ex4/images/04-27.png)

25.	Switch to tab **Receiver**, and maintain the credential alias **PIMAS_Demo** for each of the three receivers. Once done, click **Save** and then **Deploy**.

```yaml
PIMAS_Demo
```

<br>![](/exercises/ex4/images/04-28.png)

26.	Confirm the upcoming dialog.

27. You can check the deployment status via the monitor dashboard. Navigate to **Monitor > Integrations and APIs**

<br>![](/exercises/ex4/images/04-31.png)

28. On the monitoring page, select the <b>Manage Integration Content</b> tile.

<br>![](/exercises/ex4/images/04-32.png)
   
29. Your function libraries artifact, your message mapping, and your integration flow should be in status <b>Started</b>. From here, you get the endpoint that you need to call to test the scenario. <b>Copy the endpoint</b> of your integraiton flow to the clipboard as we will use it in the next steps.

<br>![](/exercises/ex4/images/04-33.png)


## Verify the Interface via Insomnia

1.	Open Insomnia and <b>duplicate</b> the Request you created in one of the previous exercise. If you haven't run through the previous exercises, create a new request with operation POST.

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

7. Navigate back to the monitoring page, and click the **Monitor Message Processing** link below the **Artifact Details** of your deployed integration flow.

<br>![](/exercises/ex4/images/04-34.png)

8. In the message monitor, you should see one new log in status **Completed**. In the **Properties** section of the log, you should see that the message was sent to the **third** receiver.

<br>![](/exercises/ex4/images/04-35.png)

9. Navigate back to Insomnia. Change the country code to **DE**, then click <b>Send</b> again. The response should be "200 OK".

<br>![image](/exercises/ex4/images/Insomnia-6.png)

10. Navigate back to the monitoring page, and refresh. You should see one more new log in status **Completed**. In the **Properties** section of the log, you should see that the message was sent to the **first** receiver.

<br>![](/exercises/ex4/images/04-36.png)

## Summary

Congratulations. You have successfully migrated and tested your Content-Based-Router scenario.

