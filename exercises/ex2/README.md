# Exercise 2 - Enrich UI oData service with Agency Ratings, Fiori feature showcase

In this exercise, we enrich our travel booking data model with agency ratings to provide a sneak preview of using a rating indicator to enrich the UI with additional information about the rating of the agency that has booked the travel for the customer..

## Exercise 2.1 Demo Only - How to add additional fields/ associations/compositions to existing data models via Developer Extensibility 

After completing this demo, we will have created a parent-child ( composition ) association between our Agency and Agency Review Rating entities and hence will be able to use this to calculate average rating for the agency. 
Showcase the following 
 - Current Agency CDS Entity : ZAD164_R_AGENCY
 - Extend View defintion on Agency Entity : ZAD164_R_AGENCY_EXTEND
 - View which is accessed as an extnesion : ZAD164_R_AGENCY_REVIEW

## Exercise 2.2 Consume the data from extended view

After completing these steps you will have included a new field for average rating in the travel booking data model which consumes the data from the entity that was added as part of developer extensibility demo.

1.	Open the data definition for view **ZAD164_R_TRAVEL_000** from the project explorer and add a new association to **ZAD164_R_AGENCY_REVIEW** and compute the average rating for the agency from the data from association.
   NOTE: While using the avg(... ) function, the CDS entity prompts to use GROUP BY clause in CDS entity -> Use the quick assist to generate the required data
The entity should now look like this
<br>![](images/AD164_E2_1_1.png)
```abap
    @AccessControl.authorizationCheck: #NOT_REQUIRED
    @EndUserText.label: 'Data model for Travel App'
    define root view entity zad164_r_travel_000 
      as select from zad164travel_000 as travel_000
      
      association [0..1] to zad164_r_agency             as _Agency         on $projection.AgencyId = _Agency.AgencyId
      association [0..*] to zad164_r_agency_review      as _AgencyReview   on $projection.AgencyId = _AgencyReview.AgencyId
      association [0..1] to zad164_r_customer           as _Customer       on $projection.CustomerId = _Customer.CustomerID
      association [1..1] to zad164_r_overall_status_vh  as _OverallStatus  on $projection.OverallStatus = _OverallStatus.OverallStatus
      association [0..1] to I_Currency                  as _Currency       on $projection.CurrencyCode = _Currency.Currency
    {
      key travel_uuid                           as TravelUuid,
      travel_id                                 as TravelId,
      agency_id                                 as AgencyId,
      avg( _AgencyReview.Rating as abap.fltp )  as AgencyRating,
      customer_id                               as CustomerId,
      begin_date                                as BeginDate,
      end_date                                  as EndDate,
      @Semantics.amount.currencyCode: 'CurrencyCode'
      booking_fee                               as BookingFee,
      @Semantics.amount.currencyCode: 'CurrencyCode'
      total_price                               as TotalPrice,
      currency_code                             as CurrencyCode,
      description                               as Description,
      overall_status                            as OverallStatus,
      @Semantics.user.createdBy: true
      local_created_by                          as LocalCreatedBy,
      @Semantics.systemDateTime.createdAt: true
      local_created_at                          as LocalCreatedAt,
      @Semantics.user.lastChangedBy: true
      local_last_changed_by                     as LocalLastChangedBy,
      @Semantics.systemDateTime.localInstanceLastChangedAt: true
      local_last_changed_at                     as LocalLastChangedAt,
    
      @Semantics.systemDateTime.lastChangedAt: true
      last_changed_at                           as LastChangedAt,
      
      /* Associations */
      _Agency,
      _AgencyReview,
      _Customer,
      _OverallStatus,
      _Currency
      
    }
    group by
      travel_uuid,
      travel_id,
      agency_id,
      customer_id,
      begin_date,
      end_date,
      booking_fee,
      total_price,
      currency_code,
      description,
      overall_status,
      local_created_by,
      local_created_at,
      local_last_changed_by,
      local_last_changed_at,
      last_changed_at
```

2.	Click here.
<br>![](/exercises/ex2/images/02_02_0010.png)

## Summary

You've now ...

Continue to - [Exercise 3 - Excercise 3 ](../ex3/README.md)
