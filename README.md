
# AD164 - Introduction of ABAP Cloud to classic ABAP developers

## Description

This repository contains the material for the SAP TechEd 2023 session called AD164 - Introduction of ABAP Cloud to classic ABAP developers.  

## Overview

This course uses the well known travel booking reference app to classic ABAPers. During the course of this session, we will go through two demos and then followed by a hands-on providing an experience on how to handcode the same in ABAP Cloud with our well known ABAP Restful Application Programming Model ( RAP ). We will have short overview of the RAP artefacts thats gets generated and will see a Fiori elements preview of the app to check the developed OData UI service. 
Additionaly, we have a short optional HandsOn exercise to enrich our existing fiori preview and hence our app utilizing ratings from the underlying Agency data model.
We also have demos showcasing - 
1. Behaviour Implementations - Managed, Managed with Additional Save and Unmanaged
2. Use ABAP Repository Object Generator in ADT to quickly generate RAP artefacts
3. Ways to consume existing WRICEF Objects in new ABAP Cloud 

### Business Scenario 

<details>
 <summary>Click to expand!</summary>
 
 **Create a custom BO for a specific business context**

 - An existing customer/partner wants to create a new business application for Travel Booking Approvals. Users of this approval App can either Approve or Reject a travel booking that is posted in the system. This will be realized with RESTful ABAP Programming Model(RAP). 

 - You’ll build the application step-by-step, starting with creating the database table to hold all the relevant travel booking, you will then create the RAP BOs ( interface and projections ) with the relevant nodes data modeled with CDS entities to read and expose relevant data to the oData UI service ( please note this is the similar data model that was also used in the second demo involving ALV with IDA ), we will enrich the generated data model with relevant UI annotations that help us define the how the data needs to be presented in the UI by defining these in CDS Medata Data Extensions ( MDE ),  you will then enable transactional capabilities to the RAP BO using Behavior Definitions ( BDEFs ) and their Behavior implemtations ( BIL ) whilc also includes two user defined custom actions APPROVE and REJECT, you will then expose releavnt RAP artefacts using a Service Definition and bind it to an oDATA V2 / V4 UI protocol using the Service Binding.
We then preview the generated OData UI service using the Fiori elements preview to see how the created UI service is rendered using the UI annotations we have enriched our data model in the MDE.

Your application will look like this:
 ![Custom business application]( ex0/images/TravelBookingApprovalApp.png )
 
 - Now, the customer/partner wishes to enhance the existing travel booking approval  application with ratings from the Agency.  When an travel booking is being approved, it is good to see the agency review rating in the list. Using the developer extensibility and underlying datamodels in SAP S/4HANA OnPremise ABAP Environment, custom code can be added to existing business logic of the travel approval BO to fulfill this requirement.

 Your application will finally look like this:

 ![Custom business application]( ex0/images/TravelBookingApprovalAppWithAgencyRating.png )
 
</details>

### Architecture Overview
<details>
 <summary>Click to expand!</summary>

 The figure below illustrates the high-level architecture components of the ABAP RESTful Application Programming Model (RAP). It shows the main technologies and artefacts needed to build an SAP Fiori app or a Web API with RAP from a design time perspective.  
 
 ![architecture](ex0/images/RAP_bigpicture.png)
 
 You can find a more information on the various RAP concepts on the SAP Help Portal.

 </details>
 

## Requirements

To carry out the exercises of this repository, you need to
1. Install the ABAP Development Tools (ADT) for the ABAP development parts
2. Have a browser ready, preferably Google Chrome, to see Fiori Elements preview

The users for the development environment during the course will be provided to you by the hosts.

Go to Getting Started - Preparation to find out the installation details, URLs, then start with the first exercise.

## Exercises
[^Top of page](#)

- [Getting Started](exercises/ex0/)
- [Exercise 1 - Create Your Own Transaction UI Service](exercises/ex1/)
    - [Exercise 1.1 - Create ABAP Package](exercises/ex1#exercise-11-sub-exercise-1-description)
    - [Exercise 1.2 - Create Database Table](exercises/ex1#exercise-12-sub-exercise-2-description)
    - [Exercise 1.3 - Create CDS data model](exercises/ex1#exercise-13-sub-exercise-3-description)
    - [Exercise 1.4 - Create CDS projection views ](exercises/ex1#exercise-14-sub-exercise-4-description)
    - [Exercise 1.5 - Create Behavior Defintion for CDS data model](exercises/ex1#exercise-15-sub-exercise-5-description)
    - [Exercise 1.6 - Create Behavior Defintion for projection views](exercises/ex1#exercise-16-sub-exercise-6-description)
    - [Exercise 1.7 - Create Your Service Definition](exercises/ex1#exercise-17-sub-exercise-7-description)
    - [Exercise 1.8 - Create Your Service Binding and Test using Fiori Elements Preview](exercises/ex1#exercise-18-sub-exercise-8-description)
    - [Exercise 1.9 - Generate Test data and Test using Fiori Elements Preview](exercises/ex1#exercise-19-sub-exercise-9-description)


- [Exercise 2 - Enhance the app with Agency ratings](exercises/ex2/)
    - [Exercise 2.1 - Use Extended BO for Agency Review Ratings in the current data model](exercises/ex2#exercise-21-sub-exercise-1-description)
    - [Exercise 2.2 - Test](exercises/ex2#exercise-22-sub-exercise-2-description)

## How to obtain support
[^Top of page](#)

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../../../issues) tab.


## Further Information
[^Top of page](#)

You can find further information on the different topics here: 
- [SAP S/4HANA Cloud ABAP Environment](https://www.sap.com/about/events/teched-news-guide/composable-enterprise-solutions.html)
- [New ABAP Platform Extensibility Options for SAP S/4HANA](https://blogs.sap.com/2021/11/19/new-abap-platform-extensibility-options-in-2021/)
- [Getting Started with the ABAP RESTful Application Programming Model (RAP)](https://blogs.sap.com/2019/10/25/getting-started-with-the-abap-restful-programming-model/)
- [ABAP Extensibility Topic Page @SAP Community](https://community.sap.com/topics/abap-extensibility)


## License
Copyright (c) 2023 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
