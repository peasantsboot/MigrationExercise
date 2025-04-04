# Exercise 4 - Migrate and Test a Content-Based-Router Scenario

In this exercise, we will create and migrate a Content-Based-Router scenario, i.e., the source Integrated Configuration Object (ICO) contains xpath conditions that are carried out to determine the receiver that the message should be sent to. In our case. the xpath conditions check the country code, in case of DE the message is sent to receiver 1, in case of IN to receiver 2 and in case of US to receiver 3. If the condition is not met, the message runs into an error. Furthermore, we will use reusable aritfacts in Cloud Integration, i.e., a message mapping and a function library which have been already uploaded from the SAP Process Orchestration system.

## Run the Migration Wizard

1. Open your previously created package, and switch to the <b>Artifacts</b> tab, then switch to <b>Edit</b> Mode. If you haven't created an own integration package yet, navigate to [Create an Integration package](/exercises/ex0/#create-an-integration-package), create a new package and then return. Otherwise, proceed with the next steps.

<br>![](/exercises/ex4/images/04-01.png)

2. Click on <b>Migrate</b> to start the migration wizard.

<br>![](/exercises/ex4/images/new-04-09.png)

3.	In the migration wizard, select the SAP Process Orchestration system **J2E** from the drop down menu, then click <b>Next Step</b>.

<br>![](/exercises/ex4/images/04-05.png)

4. In SAP Process Orchestration, only Integrated Configuration Objects (ICO) are supported. So keep the Object Type as **Integrated Configuration**. You can use the filter to filter out the list of ICOs and choose the appropriate scenario. Click on the <b>Selection</b> icon. 

<br>![image](/exercises/ex4/images/ShowFilters.png)

5. In the filter of the upcoming dialog, fill in **CBR_S02** for the **Sender Communication Component**, then select button **Go** to restrict the list of Items. Choose the interface **SI_SalesOrder_Out** with sender **CBR_S02** from the Items list.

<br>![image](/exercises/ex4/images/ChooseScenario.png)

6. Once you have selected the scenario, click <b>Next Step</b>.

<br>![image](/exercises/ex4/images/ChooseScenarioNext.png)

7.	The best fit pattern is identified. Whether your ICO is of pattern Content Based Routing or Recipient List depends on the xpath conditions to determine the receivers. If the xpaths conditions are exclusive, i.e., only one condition applies and as such the message is sent to only one receiver, then the ICO is of pattern Content Based Routing. Otherwise, if many conditions may apply for a message, and hence the message may be sent to multiple receivers, then the ICO is of pattern Recipient List. Right now however, for content-based routing as well as recipient list scenarios, the **Recipient List Asynchronous** pattern is proposed. This may change in future to simplify the integration flow model for content-based routing scenarios. Click <b>Next Step</b>.

<br>![](/exercises/ex4/images/04-08.png)

8. In the next step, you can choose whether you like to work with reusable message mapping artifacts or not. In this exercise, we like to reuse artifacts which have been already uploaded to Cloud Integration. So, keep the **Enable Reusable Message Mapping Artifacts** flag selected. As you can see, you have the option to select the integration package where the reusable artifact should be uploaded to. By default, the integration package is preset from where you started the migration wizard. Let's change the default setting. Click **Select** next to the artifact package.

<br>![](/exercises/ex4/images/new-04-10.png)

9. In the upcoming dialog, select the integration package **Migration Reusable Artifacts**. That's where we have uploaded the mapping including the function library to.

<br>![](/exercises/ex4/images/new-04-11.png)

10. The wizard detects that the message mapping with name **MM_SalesOrderWithFuncLib** has been already uploaded from the ESR of SAP Process Orchestration, so the Import Method is set to **Reuse**. If not, change to **Reuse** and select the exisitng mapping from the drop down menu.

<br>![](/exercises/ex4/images/new-04-12.png)

11. Click **Next Step**.

<br>![](/exercises/ex4/images/new-04-13.png)

12. In the next step, you can see the message mapping resources. No new message is created, the existing one is used. Click **Next Step**.

<br>![](/exercises/ex4/images/new-04-14.png)

13.	Maintain a **Name** for your integration flow, e.g., following the pattern **cbr_userXX** where <b>XX</b> is your user number from 00 to 99. Then, click on <b>Review</b>.

<br>![](/exercises/ex4/images/04-14.png)

14.	Verify the information and click on <b>Migrate</b>.

<br>![](/exercises/ex4/images/04-15.png)

15.	The integration flow will be generated within your integration package. Click on  **View Artifact** to take a closer look. 

<br>![](/exercises/ex4/images/04-17.png)

16.	As you can see from the generated integration flow model, two integration processes are decoupled via JMS. In the first integration process, the xpath conditions to determine the receivers are carried out in a groovy script. For each receiver that meets the xpath condition, the message is then stored in a JMS queue. The second integration process picks up the messages from this very JMS queue and forwards the message to the right route based on the receiver name. In each route, a mapping is carried out and then the mapped message is sent out to the receiver.

<br>![](/exercises/ex4/images/04-17x.png)

17. Open the **Runtime Configuration** tab and check if the namespaces are properly set. You should see two namespaces. If not, add the following namespaces to the **Namespace Mapping** list separated by semicolon. Then **Save** your changes.

```yaml
xmlns:sys=http://sap.com/xi/XI/System;xmlns:p1=http://pi-elevation.bootcamp.com
```
<br>![](/exercises/ex4/images/04-17ns.png)

18. Click on **Configure** to configure the sender and receiver adapters.

<br>![](/exercises/ex4/images/04-18.png)

19.	In the upcoming dialog, on tab **Sender**, select the Sender **CBR_S02** and maintain the endpoint of your generated integration flow. The endpoint needs to be unique within the tenant, so append **/userXX** to the Address with **XX** the user number assigned to you.

```yaml
/cbr/s02/userXX
```

<br>![](/exercises/ex4/images/04-27.png)

20. Select the Sender of type JMS, here **JMSSender_4** (generated name may vary), and maintain the Queue Name **userXX** with **XX** the user number assigned to you.

<br>![](/exercises/ex4/images/04-27a.png)

21.	Switch to tab **Receiver**, and maintain the credential alias **PIMAS_Demo** for each of the three receivers **CBR_R01**, **CBR_R02**, and **CBR_R03**.

```yaml
PIMAS_Demo
```

<br>![](/exercises/ex4/images/04-28.png)

22.	Select the Receiver of type JMS, here **JMSReceiver_1**, and maintain exactly the same Queue Name as before, i.e., **userXX** with **XX** the user number assigned to you. Once done, click **Save** and then **Deploy**.

<br>![](/exercises/ex4/images/04-28a.png)

23.	Confirm the upcoming dialog to deploy the integration flow on the **Cloud Integration** runtime.

<br>![](/exercises/ex4/images/04-29.png)

24. You can check the deployment status via the monitor dashboard. Navigate to **Monitor > Integrations and APIs**. On the monitoring page, select the <b>Manage Integration Content</b> tile.

<br>![](/exercises/ex4/images/04-32.png)
   
25. Your integration flow should be in status <b>Started</b>. You can also see that the resuable function libraries artifact and message mapping has been already deployed. From here, you get the endpoint that you need to call to test the scenario. <b>Copy the endpoint</b> of your integraiton flow to the clipboard as we will use it in the next steps.

<br>![](/exercises/ex4/images/new-04-16.png)


## Verify the Interface

After completing these steps you will be able to test the interface.

**Note**: You have two options to execute and test your integration scenario:
- The quickest option is to use the Bruno API client application for which we have provided a collection with pre-configured sample request. As a prerequisite to test your integration scenario using the Bruno API client, you should have gone through [Setup Bruno API client](../ex0#setup-bruno-api-client/). If not, do the setup, then come back and proceed with [option 1](#option-1-using-bruno-api-client).
- If you like to use your own tool, we have described in detail how to setup a sample request incl. body and authentication. This is described in [option 2](#option-2-using-your-own-api-client).

### Option 1: Using Bruno API client

1. Open the Bruno application on your laptop, expand the **Migration Exercises** collection and select the POST request **Exercise 4 - Content-Based-Router**. Paste the copied end point from the clipboard into the URL field or simply replace the **XX** in the URL with the id provided to you. Ensure that the **eu03** environment has been selected. Then trigger a message by selecting the **Send Request** button on the upper right.

<br>![image](/exercises/ex4/images/bruno-04-01.png)

2. Upon success, you will receive **200 OK** status.

<br>![image](/exercises/ex4/images/bruno-04-02.png)

3. Navigate back to the monitoring page, and click the **Monitor Message Processing** link below the **Artifact Details** of your deployed integration flow.

<br>![](/exercises/ex4/images/new-04-17.png)

4. In the message monitor, you should see two new logs in status **Completed**, one for the integration process writing to the JMS queue, and one for the integration process reading from the very same queue. In the **Properties** section of the logs, you should see that the message was sent to the **third** receiver.

<br>![](/exercises/ex4/images/04-35.png)

5. Navigate back to Bruno. Change the country code to **DE**, then click <b>Send</b> again. The response should be "200 OK".

<br>![image](/exercises/ex4/images/bruno-04-03.png)

6. Navigate back to the monitoring page, and refresh. You should see two more new logs in status **Completed**. In the **Properties** section of the logs, you should see that the message was sent to the **first** receiver.

<br>![](/exercises/ex4/images/04-36.png)

### Option 2: Using your own API client

Skip this option if you have used the Bruno API client to test the integration scenario.

1. Open your own API client and create a new **POST** request.

2. Paste the copied end point from the clipboard into the URL field.

3. Define the payload of type XML as follows.

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
6.	Change the country code to **DE** and resend.
7.	For monitoring the message in the message monitor of SAP Integration Suite, see from step 3 on in [option 1](#option-1-using-bruno-api-client).

## Summary

Congratulations. You have successfully migrated and tested your Content-Based-Router scenario.

