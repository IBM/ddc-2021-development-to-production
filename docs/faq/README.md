# Frequently Asked Questions & Helpful Tips / Tricks

## [Account and Service Creation](#account-sign-up-and-service-creation)

  1. Q: I don't have all the services needed
  1. Q: I get a `That email address is already registered to an IBM Cloud account.` messsage
  1. Q: I get a `Your Watson Studio, Watson Knowledge Catalog, and Watson Machine Learning Lite services must be created in the same service region.` error

***

### Account Sign up and Service Creation

#### Q: I don't have all the services needed

  A: In some rare cases, the services will not automatically provision for you. You can do that manually by following these instructions:

  1. Once you are on IBM Cloud Pak for Data, on the top right corner click on your avatar, and then click on `Profile and settings`. Go to the `Services` tab.
  
  1. If the `Machine Learning` service instance is not listed under `You Cloud Pak for Data Services` then find it in the `Try our Available Services` section and click on the `Add` button.

  1. Next, note down the name of the `Machine Learning` service instance in your `Cloud Pak for Data` section. This is the blue hyperlink underneeth the `Machine Learning` card title. You will need to provide this name in future steps.

#### Q: I get the `That email address is already registered to an IBM Cloud account.` messsage

  A: You must already have an IBMid account. Follow the login link provided in the error message to login to your existing account.

#### Q: I get the `Your Watson Studio, Watson Knowledge Catalog, and Watson Machine Learning Lite services must be created in the same service region.` error

  A: This means you have previously created some Watson services in a different region. To resolve this, go to the [CP4DaaS Login](https://dataplatform.cloud.ibm.com/registration/stepone?context=cpdaas&apps=all) page, select the region you had previously used and then login using the login link at the bottom right. Alternatively, you can create a new account and proceed as a new user to follow along.
