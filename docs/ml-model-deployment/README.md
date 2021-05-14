# Machine Learning Model Online Deployment and Scoring

In this module, we will learn how to deploy our Machine Learning models. By doing so, we make them available for use in production such that applications and business processes can derive insights from them. There are several types of deployments available ([depending on the model framework used](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/wsj/analyze-data/pm_service_supported_frameworks.html)). In this lab, we will explore:

* Online Deployments - Allows you to run the model on data in real-time, as data is received by a web service.

This lab will build an online deployment and test the model endpoint using both the built in testing tool as well as external testing tools.

> **Note:** You can click on any image in the instructions below to zoom in and see more details. When you do that just click on your browser's back button to return to the previous page.

> **Note:** The lab instructions below assume you have completed the setup section already, if not, be sure to complete the setup first to create a project and a deployment space. If you would have any issues, check the [FAQ section](../faq/README.md).

## Create Online Model Deployment

After a model has been created, saved and promoted to our deployment space, we can proceed to deploying the model. For this section, we will be creating an online deployment. This type of deployment will make an instance of the model available to make predictions in real time via an API. Although we will use the Cloud Pak for Data UI to deploy the model, the same can be done programmatically.

* Navigate to the left-hand (☰) hamburger menu, expand the `Deployments` section and click on `View all spaces`.

    [![Analytics Analyze deployments](../images/navigation/menu-analytics-deployments.png)](../images/navigation/menu-analytics-deployments.png)

* Click on the `Spaces` tab and then choose the deployment space you setup previously by clicking on the name of your space.

* From your deployment space overview, click the `Assets` tab and in the 'Models' table, find the model name for the model you previously built and now want to create a deployment against. Use your mouse to hover over the right side of that table row and click the `Deploy` rocket icon (the icons are not visible by default until you hover over them).

    > Note: There may be more than one model listed in them 'Models' section. This can happen if you have run the Jupyter notebook that creates SparkML models more than once or if you have run through both the Jupyter notebook and AutoAI modules to create models.

    [![Actions Deploy model](../images/deployment/deploy-autoai-model-icon.png)](../images/deployment/deploy-autoai-model-icon.png)

* On the `Create a deployment` screen, choose `Online` for the `Deployment Type`, give the Deployment a name and optionally a description and click the `Create` button.

    [![Online Deployment Create](../images/deployment/deploy-online-deployment.png)](../images/deployment/deploy-online-deployment.png)

* Click on the `Deployments` tab. The new deployment status will show as `In progress` and then switch to `Deployed` when it is complete.

    [![Status Deployed](../images/deployment/deploy-status-deployed.png)](../images/deployment/deploy-status-deployed.png)

## Test Online Model Deployment

Cloud Pak for Data offers tools to quickly test out Watson Machine Learning models. We begin with the built-in tooling.

* From the Model deployment page, once the deployment status shows as `Deployed`, click on the name of your deployment. The deployment `API reference` tab shows how to use the model using `cURL`, `Java`, `Javascript`, `Python`, and `Scala`.

* To get to the built-in test tool, click on the `Test` tab and then click on the `Provide input data as JSON` icon.

    [![Test deployment with JSON](../images/deployment/deploy-model-test-page.png)](../images/deployment/deploy-model-test-page.png)

* Copy and paste the following data objects into the `Body` panel (replace the text that was in the input panel).

    > *Note: Click the tab appropriate for the model you are testing (either an AutoAI model or the SparkML one built using the Jupyter notebook). Also make sure the input below is the only content in the field. Do not append it to the default content `{ "input_data": [.......] }` that may already be in the test input panel.*

    === "AutoAI Model"

        ```json
        {
            "input_data": [
                {
                    "fields": [
                        "CustomerID",
                        "LoanDuration",
                        "LoanPurpose",
                        "LoanAmount",
                        "InstallmentPercent",
                        "OthersOnLoan",
                        "EmploymentDuration",
                        "Sex",
                        "CurrentResidenceDuration",
                        "OwnsProperty",
                        "Age",
                        "Housing",
                        "Job",
                        "Dependents",
                        "Telephone",
                        "ForeignWorker",
                        "CheckingStatus",
                        "CreditHistory",
                        "ExistingSavings",
                        "InstallmentPlans",
                        "ExistingCreditsCount"
                    ],
                    "values": [
                        [
                            "1",
                            13,
                            "car_new",
                            1343,
                            2,
                            "none",
                            "1_to_4",
                            "female",
                            3,
                            "savings_insurance",
                            46,
                            "own",
                            "skilled",
                            1,
                            "none",
                            "yes",
                            "no_checking",
                            "credits_paid_to_date",
                            "100_to_500",
                            "none",
                            2
                        ]
                    ]
                }
            ]
        }
        ```

    === "Jupyter Spark Model"

        ```json
        { "input_data": [{
            "fields": [ "CheckingStatus", "LoanDuration", "CreditHistory", "LoanPurpose", "LoanAmount", "ExistingSavings", "EmploymentDuration", "InstallmentPercent", "Sex", "OthersOnLoan", "CurrentResidenceDuration", "OwnsProperty", "Age", "InstallmentPlans", "Housing", "ExistingCreditsCount", "Job", "Dependents", "Telephone", "ForeignWorker"],
            "values": [[ "no_checking", 13, "credits_paid_to_date", "car_new", 1343, "100_to_500", "1_to_4", 2, "female", "none", 3, "savings_insurance", 46, "none", "own", 2, "skilled", 1, "none", "yes"]]
        }]}
        ```

* Click the *`Predict`* button. The model will be called with the input data and the results will display in the *Result* window. Scroll down to the bottom of the result to see the prediction (i.e "Risk" or "No Risk").

    [![Testing the deployed model](../images/deployment/deploy-test-model-prediction.png)](../images/deployment/deploy-test-model-prediction.png)

    > **Note:** For some deployed models (for example AutoAI based models), you can provide the request payload using a generated form by clicking on the `Provide input using form` icon and providing values for the input fields of the form. If the form is not available for the model you deployed, the icon will not be present or will remain grayed out.

    > [![Input to the fields](../images/deployment/deploy-test-input-form.png)](../images/deployment/deploy-test-input-form.png)

* ***Important: If you have completed this section and do not plan on completing the other optional deployment approaches below, please go ahead and cleanup your deployment. Follow the [Cleanup Deployment instructions below.](#cleanup-deployments)***

## (Optional) Test Online Model Deployment using cURL

Now that the model is deployed, we can also test it from external applications. One way to invoke the model API is using the cURL command. For simplicity, we will be using the IBM Cloud shell to run these cURL commands. If you have the IBM Cloud CLI and associated command line utilities installed locally, you are free to attempt these steps on your own machine.

* In a new browser window/tab, go to the [IBM Cloud Home Page](https://cloud.ibm.com) and click the terminal icon in the upper right-hand bar. The cloud shell will launch a new browser tab with a web terminal.

    [![Terminal Button](../images/setup/access-cloud-shell.png)](../images/setup/access-cloud-shell.png)

* In order to invoke the model endpoints, we need to authorize using an access token. To get an access token you will use the `IBM Cloud API Key`, which you created during the setup section.

* In the cloud shell window, run the following command to get a token to access the API. Replace `<API Key>` with the api key that you got from running above command.

    ```bash
    curl -X POST 'https://iam.cloud.ibm.com/identity/token' -H 'Content-Type: application/x-www-form-urlencoded' -H 'Accept: application/json' --data-urlencode 'grant_type=urn:ibm:params:oauth:grant-type:apikey' --data-urlencode 'apikey=<API Key>'
    ```

* A json string will be returned with a value for `accessToken` that will look *similar* to this:

    ```json
    {
        "access_token":"AAAAAAAfakeACCESSTOKENNNNNNN",
        "refresh_token":"BBBBBBBBBBBFAKEREFRESHTOKENNNNNNNNNNNNN",
        "token_type":"Bearer",
        "expires_in":3600,
        "expiration":1601317201,
        "scope":"ibm openid"
    }
    ```

* You will save the access token value shown after the `access_token` key in a temporary environment variable in your terminal. Copy the access token value (without the quotes) in the terminal and then use the following export command to save the "accessToken" to a variable called `WML_AUTH_TOKEN`.

    ```bash
    export WML_AUTH_TOKEN=<value-of-access-token>
    ```

* Back on the Cloud Pak for Data model deployment page, go to the `API reference` tab and copy the `Endpoint` value (an example endpoint would be: *`"https://us-south.ml.cloud.ibm.com/ml/v4/deployments/<DEPLOYMENT_ID>/predictions?version=2020-09-01"`*).

    [![Model Deployment Endpoint](../images/deployment/deploy-model-endpoint.png)](../images/deployment/deploy-model-endpoint.png)

* In your cloud shell terminal, save that endpoint to a variable named `URL` by exporting the value. (*Note: the URL should end with a version query parameter*).

    ```bash
    export WML_URL=<value-of-endpoint>
    ```

* Now run this curl command from the terminal to invoke the model with the same payload we used previousy:

    ```bash
    curl -k -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer  $WML_AUTH_TOKEN" -d '{"input_data": [{"fields": ["CustomerID","LoanDuration","LoanPurpose","LoanAmount","InstallmentPercent","OthersOnLoan","EmploymentDuration","Sex","CurrentResidenceDuration","OwnsProperty","Age","Housing","Job","Dependents","Telephone","ForeignWorker","CheckingStatus","CreditHistory","ExistingSavings","InstallmentPlans","ExistingCreditsCount"],"values": [["1",13,"car_new",1343,2,"none","1_to_4","female",3,"savings_insurance",46,"own","skilled",1,"none","yes","no_checking","credits_paid_to_date","100_to_500","none",2]]}]}' $WML_URL
    ```

* A json string will be returned with the response, including a  prediction from the model (i.e a "Risk" or "No Risk" at the end indicating the prediction of this loan representing risk).

* ***Important: If you have completed this section and do not plan on completing the other optional deployment approaches below, please go ahead and cleanup your deployment. Follow the [Cleanup Deployment instructions below.](#cleanup-deployments)***

## Cleanup Deployments

You can clean up the deployments created for your models. To remove the deployment:

* Navigate to the left-hand (☰) hamburger menu, expand the `Deployments` section and click on `View all spaces`.

    [![Analytics Analyze deployments](../images/navigation/menu-analytics-deployments.png)](../images/navigation/menu-analytics-deployments.png)

* Choose the deployment space you setup previously by clicking on the name of your space.

* From your deployment space overview, click the `Assets` tab and in the 'Model' table, click on the model name that you previousely promoted and created deployments against.

* Under 'Deployment Types', click on `Online` to view the online deployments you have created for this model.

* In the table on the main panel, click on the three vertical dots at the right of the row for the online deployment you created. Select the `Delete` option from the menu.

    > *Note: The vertical dots are hidden until you hover over them with your mouse*

    [![Delete online deployments](../images/deployment/delete-deployment.png)](../images/deployment/delete-deployment.png)

* In the subsequent pop up window, click on the `Delete` button to confirm you want to delete this deployment.

* You can follow the same process to delete other deployments as needed.

## Conclusion

Congratulations. You've completed this lab and seen how to create and test online deployments for your machine learning models.

Feel free to explore the additional (optional) deployment labs, which show you how to:

* [Create and test a batch deployments.](batch-model-deployment.md)
* [Integrate the online deployment to an application.](sample-application-integration.md)
