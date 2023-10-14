[![REUSE status](https://api.reuse.software/badge/github.com/SAP-samples/teched2023-AD164)](https://api.reuse.software/info/github.com/SAP-samples/teched2023-AD164)

# AD164 - Introduction of ABAP Cloud to classic ABAP developers

## Description

This repository contains the material for the SAP TechEd 2023 session called AD164 - Introduction of ABAP Cloud to classic ABAP developers.  

## Overview

This course uses the well known travel booking reference app to classic ABAPers. During the course of this session, we will go through two demos and then followed by a hands-on providing an experience on how to handcode the same in ABAP Cloud with our well known ABAP Restful Application Programming Model ( RAP ). We will have short overview of the RAP artefacts thats gets generated and will see a Fiori elements preview of the app to check the developed OData UI service. 
Additionaly, we have a short optional HandsOn exercise to enrich our existing fiori preview and hence our app utilizing ratings from the underlying Agency data model.
We also have demos showcasing - 
1. Behaviour Implementations - Managed, Managed with Additional Save and Unmanaged
2. Ways to consume existing WRICEF Objects in new ABAP Cloud 

### Business Scenario 

<details>
 <summary>Click to expand!</summary>
 
 **Create a custom BO for a specific business context**

 - An existing customer/partner wants to create a new business application for Travel Booking Approvals. Users of this approval App can either Approve or Reject a travel booking that is posted in the system. This has to be realized with RESTful ABAP Programming Model(RAP). 

 - You’ll build the application step-by-step, starting with creating the database table to hold all the relevant travel booking, you will then create the RAP BOs ( interface and projections ) with the relevant nodes data modeled with CDS entities to read and expose relevant data to the oData UI service ( please note this is the similar data model that was also used in the second demo involving ALV with IDA ), we will enrich the generated data model with relevant UI annotations that help us define the how the data needs to be presented in the UI by defining these in CDS Medata Data Extensions ( MDE ),  you will then enable transactional capabilities to the RAP BO using Behavior Definitions ( BDEFs ) and their Behavior implemtations ( BIL ) whilc also includes two user defined custom actions APPROVE and REJECT, you will then expose releavnt RAP artefacts using a Service Definition and bind it to an oDATA V2 / V4 UI protocol using the Service Binding.
We then preview the generated OData UI service using the Fiori elements preview to see how the created UI service is rendered using the UI annotations we have enriched our data model in the MDE.
Your application will look like this:
 ![Custom business application]( ex0/images/Introduction2.png )
 
 - Now, the customer/partner wishes to enhance the existing travel booking approval  application with ratings from the Agency.  When an travel booking is being approved, it is good to see the agency review rating in the list. Using the developer extensibility and underlying datamodels in SAP S/4HANA OnPremise ABAP Environment, custom code can be added to existing business logic of the travel approval BO to fulfill this requirement.

 Your application will finally look like this:

 ![Custom business application]( ex0/images/Introduction2.png )
 
</details>

### Architecture Overview
<details>
 <summary>Click to expand!</summary>

 The figure below illustrates the high-level architecture components of the ABAP RESTful Application Programming Model (RAP). It shows the main technologies and artefacts needed to build an SAP Fiori app or a Web API with RAP from a design time perspective.  
 
 ![architecture](ex0/images/rap_bigpicture.png)
 
 You can find a more information on the various RAP concepts on the SAP Help Portal.

 </details>
 

## Exercises
[^Top of page](#)


## Requirements

To carry out the exercises of this repository, you need to
1. Install the ABAP Development Tools (ADT) for the ABAP development parts
2. Have a browser ready, preferably Google Chrome, to see Fiori Elements preview

The users for the development environment during the course will be provided to you by the hosts.

Go to Getting Started - Preparation to find out the installation details, URLs, then start with the first exercise.

## Exercises

Provide the exercise content here directly in README.md using [markdown](https://guides.github.com/features/mastering-markdown/) and linking to the specific exercise pages, below is an example.

- [Getting Started](exercises/ex0/)
- [Exercise 1 - First Exercise Description](exercises/ex1/)
    - [Exercise 1.1 - Exercise 1 Sub Exercise 1 Description](exercises/ex1#exercise-11-sub-exercise-1-description)
    - [Exercise 1.2 - Exercise 1 Sub Exercise 2 Description](exercises/ex1#exercise-12-sub-exercise-2-description)
- [Exercise 2 - Second Exercise Description](exercises/ex2/)
    - [Exercise 2.1 - Exercise 2 Sub Exercise 1 Description](exercises/ex2#exercise-21-sub-exercise-1-description)
    - [Exercise 2.2 - Exercise 2 Sub Exercise 2 Description](exercises/ex2#exercise-22-sub-exercise-2-description)

  
**OR** Link to the Tutorial Navigator for example...

Start the exercises [here](https://developers.sap.com/tutorials/abap-environment-trial-onboarding.html).

**IMPORTANT**

Your repo must contain the .reuse and LICENSES folder and the License section below. DO NOT REMOVE the section or folders/files. Also, remove all unused template assets(images, folders, etc) from the exercises folder. 

## Contributing
Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) to understand the contribution guidelines.

## Code of Conduct
Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2023 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
