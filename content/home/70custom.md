+++
weight = 70
+++

{{% section %}}

##  Build Custom Formula Fields

Create 'Power of One' fields in the Opportunity Object:<br>
```
IF(ISPICKVAL( StageName , "X"), 1, NULL)
```
<small>X = Disqualified, Nurture, Closed Lost, Closed Won</small><br>

<br>
<small>
navigate down for more formulas
</small>
<br>
<a href="#" class="navigate-down">🔽</a>

---

Create 'Age Won' field in the Opportunity Object:<br>
```
IF(ISPICKVAL( StageName , "Closed Won"), CloseDate - DATEVALUE(CreatedDate), NULL)
```
<br>
<a href="#" class="navigate-down">🔽</a>
___

Create 'Avg Age Won' & 'Avg Value Won' columns in an Opportunity Report:<br>
```
Opportunity.Age_Won__c:SUM/Opportunity.Won__c:SUM 
```
```
Opportunity.Amount:SUM/Opportunity.Won__c:SUM
```
<br>
<small>Use standard Amount field only if annual is the longest contract term.</small>
<br>
<a href="#" class="navigate-down">🔽</a>

---

Create 'Win Rate' & 'Sales Velocity' columns in an Opportunity Report:<br>
```
Opportunity.Won__c:SUM/(RowCount-Opportunity.DQ__c:SUM-Opportunity.Nurture__c:SUM)
```
```
RowCount*(Opportunity.Amount:SUM/Opportunity.Won__c:SUM)*(WON:SUM/(RowCount-Opportunity.DQ__c:SUM-Opportunity.Nurture__c:SUM))/(Opportunity.Age__c:SUM/Opportunity.Won__c:SUM)
```

{{% note %}}
If you have multi-year terms, you need to create a field for Annual Contract Value (ACV). Otherwise your Sales Velocity will be artificially inflated by the standard Opportunity Amount field.
{{% note %}}

{{% /section %}}
