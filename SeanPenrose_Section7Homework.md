# 7.1 HW Questions 


1. Using EVregistry, Write a query to select the `ModelYear`, `Make`, and `Model` off all of the vehicles in the registry.
```SQL
--1.
SELECT ModelYear, Make, Model
From EVRegistry
```
2. Using the EVRegistry table, Write a query that lists all of the unique types of EV's. your reult set should have one column, `ElectricVehicleType`. 
```SQL
--2.
SELECT DISTINCT ElectricVehicleType
FROM EVRegistry
```
3. Using the EVRegistry, Write a query that shows all of the information on Battery Electric Vehicles (BEV) that are in the registry. 
```SQL
--3.
Select DISTINCT *
from EVRegistry
WHERE ElectricVehicleType = 'Battery Electric Vehicle (BEV)'
```
4. Using the EVRegistry, wirte a query that returns the `Make` and `Model` of all of the EV's that have a BaseMSRP between 20000 and 35000?  

```SQL
--4.
SELECT DISTINCT Make, Model
FROM EVRegistry
WHERE BaseMSRP BETWEEN 20000 AND  35000

```
# 7.2 HW Questions 

1. Using EVRegistry, write a query to find a record  where the `City` attribute is NULL. Return all of the available columns. 
```SQL
--1.
SELECT *
FROM EVRegistry
WHERE CITY IS NULL
```
2. Write a query to find the `make`, `model`, and `ElectricVehicleType` where the VIN number has  that ends in '3E1EA1J'.
```SQL
--2.

SELECT Make, Model, ElectricVehicleType
FROM EVRegistry
WHERE VIN LIKE '%3E1EA1J'
```
3. Select the `ModelYear`, `make`, `model`, `ElectricVehicleType`, and `range` of the Tesla vehicles or cheverolet vehicles in the registry. Order the result set by Make and Model year in from newest to oldest. 
```SQL
--3.
SELECT ModelYear, Make, Model, ElectricVehicleType, ElectricRange
FROM EVRegistry
WHERE Make = 'TESLA' OR Make = 'CHEVROLET'
ORDER BY ModelYear DESC, Make 
```
4. Using EVCharging, Write a query to find out how many many times those stations were used. Order them by the most used to the least used and limit the output to 5 records.
```SQL
--4.
SELECT StationID, Count(*) as numUses
FROM EVCharging
GROUP BY StationID 
ORDER BY COUNT(*) DESC;
``` 
5.  Using EVCharging, For the folks who charged longer than 0.5 hours, show the min and max of the charging time for each user. Your output columns should be `userid`, `minTime`, and `maxTime`. Order this result set by the last two columns respectively. 
```SQL
--5.
SELECT userId, MIN(chargeTimeHrs) as 'MinHours', MAX(chargeTimeHrs) as 'MaxHours'
FROM EVCharging
WHERE chargeTimeHrs > 0.5
GROUP BY userId
ORDER BY 2,3

```
# 7.3 HW Questions
1. Using EVCharging, Which day of the week has the highest average charging time? Round the answer to 2 decimal points.
```SQL
--1.
SELECT weekday, round(chargeTimeHrs, 2) as AvgChargeTime
FROM EVCharging
group by weekday
```
2. Using, EV charging, Find the total power consumed from charging EV's by each User. Return the `userId` and name the calculated column, `totalPower`. Round the answer to 2 deciaml points and list the out put in highest to lowest order. Limit the order to the top 15 users.
```SQL
--2.
SELECT userid, round(kwhTotal,2) as TotalPower
FROM EVCharging
GROUP by userId
ORDER by kwhtotal DESC
LIMIT 15 
``` 
3. Using dimfacility and factCharge, write a query to find out which type of facility (GROUP BY) has the most amount of charging stations. Return `type Facility` and name the calculated column `numStation`. Order the result set from highest to lowest number of charging stations.
```SQL
--3.
SELECT df.typeFacility, Count(Distinct fc.stationId) as numStation
FROM factCharge fc
INNER JOIN dimFacility df
on fc.facilityID = df.FacilityKey
GROUP by 1
ORDER by 2 DESC
```  
4. In your own words, Briefly explain Primary Keys and Foreign Keys. 

**Answer-**
A Primary Key is a column that uniquely indentifies each record in our table while not containing null vallues. Each table can only have one primary key. When you join another table you join on their primary key. This primary key you join on becomes a foreign key in your new table. A foreign key is basically a primary key from another table that is used to reference the information from another table when you do a join.


5. Using EV Charging, For the folks who charged longer than one hour, show the min and max of the charging time for each user. Your output columns should be `userid`, `minTime`, and `maxTime`. Order this result set by the last two columns respectively. HINT: USE `HAVING`

```SQL
SELECT userId, Max(chargeTimeHrs) as maxTime, MIN(chargeTimeHrs) as minTime
FROM EVCharging
Group by userId
HAVING chargeTimeHrs > 1
ORDER by 2 DESC
```



