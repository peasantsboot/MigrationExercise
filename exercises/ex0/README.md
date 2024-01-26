
# Prerequisites for the Migration Exercises

After having finished the assessment of the current SAP Process Orchestration landscape and having estimated the effort needed to migrate with the Migration Assessment capability, the next step is the actual migration. The goal of the Migration Tool is to provide a semi-automated migration where interfaces in Cloud Integration will be automatically created so ideally 60-70% of technical migration efforts are automated. The migration of scenarios is based on a template approach, which means that integration flow templates are used as a skeleton to migrate the content and create the final integration flows.

## Create an Integration package

 As a prerequisite, you first need to create an integration package where the automatically generated integration flows are created.

1. Switch back to the SAP Integration Suite landing page.

<br>![](/exercises/ex2/images/Navigate_Back.png)

2. Navigate to <b>Design > Integrations and APIs</b>, and select  <b>Create</b>.

<br>![](/exercises/ex2/images/Create_Pack.png)
   
3. Fill in the <b>Name</b> of the integration package, e.g. **Migration userXX** where <b>XX</b> is your user number from 00 to 99, and a short <b>Description</b>. The technical name is automatically set. Then click <b>Save</b>.

<br>![](/exercises/ex2/images/Save_Pack.png)
   
Continue to - [Exercise 2 - Migrate and test a simple P2P scenario](../ex2/README.md)
