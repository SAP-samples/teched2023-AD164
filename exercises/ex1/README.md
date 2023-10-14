# Exercise 1 - Create Your Own Transaction UI Service

After the **[Getting Started](../ex0/README.md)**, you will create your own RAP business object (BO) in the present exercise.

This RAP BO represents an Travel Booking Approval application , where you can Approve OR Reject travel booking as a booking approver.

## Exercise 1.1 Create ABAP Package
[^Top of page](#)

 <details>
  <summary>Click to expand!</summary>
  
0.  Optional [ If already exists ]   : Add **ZLOCAL** to **Favorite Packages** by right-click on the favourite packages and select **Add Package..**. 
   ![](images/AD164_E1_1_Step0_0.png)
    In the pop up for **Select an ABAP Package**, type ZLOCAL as the search term and choose the option **ZLOCAL** under the **Matching items:** window and click on **OK**.
  ![](images/AD164_E1_1_Step0_1.png) 
   
1.	Right-click on the package **`ZLOCAL** and select **New > ABAP Package** from the context menu. 
   ![](images/AD164_E1_1_Step1.png)
  	
3.	Maintain the information provided below and click **Next >**.  
    - Name: **`ZAD164_TRAVEL_XXX`**
    - Description: `Travel Approval App XXX`
    - Check ** `Add to favorite packages` **
    ![](images/AD164_E1_1_Step2_1.png) 
    - Select TR `HE4K917646` from option **Choose from requests in which i am involved** OR choose option **Enter a request number** and  provide a transport request number `HE4K917646`
     ![](images/AD164_E1_1_Step2_2.png)
     ![](images/AD164_E1_1_Step2_3.png) 
 
4.	Click **Finish** to finish creation of the package and add the package to favorite pacakges list.
   You should now see your new package in your Project Explorer.
     ![](images/AD164_E1_1_Final.png) 
  
</details>


## Exercise 1.2 Create Database Table
[^Top of page](#)

<details>
  <summary>Click to expand!</summary>
 
Create a database table ![table](images/adt_tabl.png) to store the _TravelBooking_ data.   
A TravelBooking entity defines general data, such as the agency, customer, begin and end date of the travel, total price with the currency, description of the travel and overall status denoting the approval status 

   1. Right-click on your ABAP package **`ZAD164_TRAVEL_###`** and select **New** > **Other ABAP Repository Object** from the context menu.
    ![](images/AD164_E1_2_1.png)
    
   3. Search for **database table**, select it, and click **Next >**.
    ![](images/AD164_E1_2_2.png)

   5. Maintain the required information (`###` is your group ID) and click **Next >**.
      - Name: **`ZAD164TRAVEL_###`**  
      - Description: _**`Persistence for Travel Booking ###`**_                  
    ![](images/AD164_E1_2_3.png)

   6. Select your transport request, and click **Finish** to create the database table.
    ![](images/AD164_E1_2_4.png)

   7. Replace the default code with the code snippet provided below and replace all occurences of the placeholder **`###`** with your group ID using the **Replace All** function (**Ctrl+F**).    
 
      **Hint**: Hover the code snippet and choose the _Copy raw contents_ icon <img src="images/CopyRawContents.png" alt="" width="30px"> appearing in the upper-right corner to copy it. Ensure to replace all occurences of XXX with your user group number
         
  <pre lang="ABAP">
  @EndUserText.label : 'Persistence for Travel Booking XXX'
  @AbapCatalog.enhancement.category : #NOT_EXTENSIBLE
  @AbapCatalog.tableCategory : #TRANSPARENT
  @AbapCatalog.deliveryClass : #A
  @AbapCatalog.dataMaintenance : #RESTRICTED
  define table zad164travel_XXX {
    key client            : abap.clnt not null;
    key travel_uuid       : sysuuid_x16 not null;
    travel_id             : zad164_travel_id not null;
    agency_id             : zad164_agency_id not null;
    customer_id           : zad164_customer_id not null;
    begin_date            : zad164_begin_date;
    end_date              : zad164_end_date;
    @Semantics.amount.currencyCode : 'zad164travel_000.currency_code'
    booking_fee           : zad164_booking_fee;
    @Semantics.amount.currencyCode : 'zad164travel_000.currency_code'
    total_price           : zad164_total_price;
    currency_code         : zad164_currency_code;
    description           : zad164_description;
    overall_status        : zad164_overall_status;
    local_created_by      : abp_creation_user;
    local_created_at      : abp_creation_tstmpl;
    local_last_changed_by : abp_locinst_lastchange_user;
    local_last_changed_at : abp_locinst_lastchange_tstmpl;
    last_changed_at       : abp_lastchange_tstmpl;
  
  }
  </pre>
       
   8. Save ![save icon](images/adt_save.png) and activate ![activate icon](images/adt_activate.png) the changes.
</details>

## Exercise 1.3 Create CDS data model
[^Top of page](#)

 <details>
  <summary>Click to expand!</summary>
  
  1.	Right-click on the data base table  **`ZAD164TRAVEL_XXX`** and select **New Data Definition** from the context menu.
     ![](images/AD164_E1_3_1.png)

  2. Maintain the information provided below and click **Next >**.

   - Name: **`ZAD164_R_TRAVEL_XXX`**
   - Description: **`Data model for Travel App XXX`** .   
   ![](images/AD164_E1_3_2.png)
    
  3.Select your transport request and click **Next**.
    ![](images/AD164_E1_3_3.png)
    
  4. Select **Define Root View Entity** from the list of templates and click on **Finish**
    ![](images/AD164_E1_3_4.png)

  5. A CDS entity with the following data definition should get generated
     ![](images/AD164_E1_3_5.png)
     
  7. Replace the default source code with following code snippet:
   
   **Hint**: Hover the code snippet and choose the _Copy raw contents_ icon <img src="images/CopyRawContents.png" alt="" width="30px"> appearing in the upper-right corner to copy it. Ensure to replace all occurences of XXX with your user group number
     
    ```ABAP
     @AccessControl.authorizationCheck: #NOT_REQUIRED
     @EndUserText.label: 'Data model for Travel App XXX'
     define root view entity zad164_r_travel_XXX 
       as select from zad164travel_000 as travel_XXX
       
       association [0..1] to zad164_r_agency             as _Agency         on $projection.AgencyId = _Agency.AgencyId
       association [0..1] to zad164_r_customer           as _Customer       on $projection.CustomerId = _Customer.CustomerID
       association [1..1] to zad164_r_overall_status_vh  as _OverallStatus  on $projection.OverallStatus = _OverallStatus.OverallStatus
       association [0..1] to I_Currency                  as _Currency       on $projection.CurrencyCode = _Currency.Currency
     {
       key travel_uuid as TravelUuid,
       travel_id             as TravelId,
       agency_id             as AgencyId,
       customer_id           as CustomerId,
       begin_date            as BeginDate,
       end_date              as EndDate,
       @Semantics.amount.currencyCode: 'CurrencyCode'
       booking_fee           as BookingFee,
       @Semantics.amount.currencyCode: 'CurrencyCode'
       total_price           as TotalPrice,
       currency_code         as CurrencyCode,
       description           as Description,
       overall_status        as OverallStatus,
       @Semantics.user.createdBy: true
       local_created_by      as LocalCreatedBy,
       @Semantics.systemDateTime.createdAt: true
       local_created_at      as LocalCreatedAt,
       @Semantics.user.lastChangedBy: true
       local_last_changed_by as LocalLastChangedBy,
       @Semantics.systemDateTime.localInstanceLastChangedAt: true
       local_last_changed_at as LocalLastChangedAt,
     
       @Semantics.systemDateTime.lastChangedAt: true
       last_changed_at       as LastChangedAt,
       
       /* Associations */
       _Agency,
       _Customer,
       _OverallStatus,
       _Currency
       
     }

     ```
     
   8.	Save and activate the object.
   9.	Define Access Control for the above CDS Root view by right-click on the CDS root entity  **`ZAD164_R_TRAVEL_XXX`** and select **New Access Control** from the context menu.
      ![](images/AD164_E1_3_6_0.png)
  10. Maintain the information provided below and click **Next >**.

   - Name: **`ZAD164_R_TRAVEL_XXX`**
   - Description: **`Access Control for ZAD164_R_TRAVEL_XXX`** .   
    ![](images/AD164_E1_3_6.png)

  11. Select your transport request and click **Next**.
    ![](images/AD164_E1_3_7.png)
  12. An access control for the CDS projection entity with the following access control definition should get generated
     ![](images/AD164_E1_3_8.png)

  14. Replace the default source code with following code snippet:
   
   **Hint**: Hover the code snippet and choose the _Copy raw contents_ icon <img src="images/CopyRawContents.png" alt="" width="30px"> appearing in the upper-right corner to copy it. Ensure to replace all occurences of XXX with your user group number

     
    ```ABAP
     @EndUserText.label: 'Access Control for ZAD164_R_TRAVEL_XXX'
     @MappingRole: true
     define role ZAD164_R_TRAVEL_XXX {
       grant
         select
           on
             zad164_r_travel_000
               where
                 1 = 1;
                 
     }
     
     ```
     
   15.	Save and activate the object.
      
 </details>
 
## Exercise 1.4 Create CDS projection views
[^Top of page](#)

 <details>
  <summary>Click to expand!</summary>
  
  1.	Right-click on the CDS root entity  **`ZAD164_R_TRAVEL_XXX`** and select **New Data Definition** from the context menu.
    ![](images/AD164_E1_4_1.png)

  2. Maintain the information provided below and click **Next >**.

   - Name: **`ZAD164_C_TRAVEL_XXX`**
   - Description: **`Projection for Travel App XXX`** .   
    ![](images/AD164_E1_4_2.png)
    
  3.Select your transport request and click **Next**.
    ![](images/AD164_E1_4_3.png)
    
  4. Select **Define Projection View** from the list of templates and click on **Finish**
    ![](images/AD164_E1_4_4.png)

  5. A CDS projection entity with the following data definition should get generated
     ![](images/AD164_E1_4_5.png)
     
  7. Replace the default source code with following code snippet:
   
   **Hint**: Hover the code snippet and choose the _Copy raw contents_ icon <img src="images/CopyRawContents.png" alt="" width="30px"> appearing in the upper-right corner to copy it. Ensure to replace all occurences of XXX with your user group number

     
    ```ABAP
     @EndUserText.label: 'Travel Projection View'
     @AccessControl.authorizationCheck: #CHECK
     
     @Metadata.allowExtensions: true
     @Search.searchable: true
     @ObjectModel.semanticKey: ['TravelID']
     define root view entity zad164_c_travel_XXX 
       provider contract transactional_query
       as projection on zad164_r_travel_XXX
     {
       key TravelUuid,
           
           @Search.defaultSearchElement: true
           TravelId,
     
           @Search.defaultSearchElement: true
           @ObjectModel.text.element: ['AgencyName']
           AgencyId,
           _Agency.Name              as AgencyName,
     
     
           @Search.defaultSearchElement: true
           @ObjectModel.text.element: ['CustomerName']
           CustomerId,
           _Customer.LastName        as CustomerName,
     
           BeginDate,
           EndDate,
     
           BookingFee,
           TotalPrice,
           CurrencyCode,
     
           Description,
     
           @ObjectModel.text.element: ['OverallStatusText']
           OverallStatus,
           _OverallStatus._Text.Text as OverallStatusText : localized,
     
           LocalLastChangedAt,
     
           _Agency,
           _Currency,
           _Customer,
           _OverallStatus
     }

     ```
     
   8.	Save and activate the object.
   9.	Define Access Control for the above projection CDS Root view by right-click on the CDS root entity  **`ZAD164_C_TRAVEL_XXX`** and select **New Access Control** from the context menu.
      ![](images/AD164_E1_4_6_0.png)
  10. Maintain the information provided below and click **Next >**.

   - Name: **`ZAD164_C_TRAVEL_XXX`**
   - Description: **`Access Control for ZAD164_C_TRAVEL_XXX`** .   
    ![](images/AD164_E1_4_6.png)

  11. Select your transport request and click **Next**.
    ![](images/AD164_E1_4_7.png)

  13. An access control for the CDS projection entity with the following access control definition should get generated
     ![](images/AD164_E1_4_8.png)

  14. Replace the default source code with following code snippet:
   
   **Hint**: Hover the code snippet and choose the _Copy raw contents_ icon <img src="images/CopyRawContents.png" alt="" width="30px"> appearing in the upper-right corner to copy it. Ensure to replace all occurences of XXX with your user group number

     
    ```ABAP
     @EndUserText.label: 'Access Control for ZAD164_C_TRAVEL_000'
     @MappingRole: true
     define role ZAD164_C_TRAVEL_000 {
       grant
         select
           on
             ZAD164_C_TRAVEL_000
               where
                 inheriting conditions from entity ZAD164_R_Travel_000;
     }
     
     ```
     
   15.	Save and activate the object.
       
 </details>
 
## Exercise 1.5 Create Behavior Defintion for CDS data model
[^Top of page](#)

 <details>
  <summary>Click to expand!</summary>
 </details>
 
## Exercise 1.6 Create Behavior Defintion for projection views
[^Top of page](#)

 <details>
  <summary>Click to expand!</summary>
 </details>
 
## Exercise 1.7 Create Your Service Definition
[^Top of page](#)

 <details>
  <summary>Click to expand!</summary>
 </details>
 
## Exercise 1.8 Create Your Service Binding and Test using Fiori Elements Preview
[^Top of page](#)

 <details>
  <summary>Click to expand!</summary>
 </details>
    
2.	Click here.
<br>![](/exercises/ex1/images/01_02_0010.png)


## Summary

You've now ...

Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)

