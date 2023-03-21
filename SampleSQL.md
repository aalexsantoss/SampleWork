# SQL Concepts

## Sections:
1. [SELECT basics](#select-basics)
2. [JOIN basics](#join-basics)

## SELECT basics
### 1.
[<font size = 2>]:#
[<font color = blue>*comment line to copy if needed here*</font></font>]:#
    
```sql
select country_name from global_sales
where continent = 'Europe'
and total_sales_dollars/items_sold >
(select total_sales_dollars/items_sold from global_sales
where country_name = 'United States')
```
<div class="alert alert-block alert-info">
<b>Query:</b> Find name of countries in Europe with larger $ amount spent per item than United States.
</div>

### 2.
```sql
select country_name, total_sales_dollars from global_sales
where total_sales_dollars > 
(select total_sales_dollars from global_sales
where country_name = 'Canada')
and total_sales_dollars <
(select total_sales_dollars from global_sales
where country_name = 'United States')'
```
<div class="alert alert-block alert-info">
<b>Query:</b> Find name of countries and $ sales that have more sales in Canada but less than United States.
</div>

### 3.
```sql
select continent, country_name, total_sales_dollars from global_sales x
where x.total_sales_dollars>= 
ALL(select total_sales_dollars from global_sales y
where y.continent=x.continent
and y.total_sales_dollars>0)
```

<div class="alert alert-block alert-info">
<b>Query:</b> Find the country (and show continent, name, & dollar sales) with the highest dollar sales in each continent.
</div>

### 4.
```sql
select x.country_name, x.continent from global_sales x
where total_sales_dollars >= 
ALL(select total_sales_dollars*3
from global_sales y
where x.continent = y.continent
and y.country_name != x.country_name)
```
<div class="alert alert-block alert-info">
<b>Query:</b> Find the country (and show country & continent) who has sales of 3 times or more compared to all the other countries in the same continent.
</div>

## JOIN basics
### 1.
```sql
select t.team_name, p.name, t.yr
from teams t join full_roster f on (f.teamid=t.id)
join player p on (a.id=f.playerid)
where f.positionid = 1
and t.id in
(select t.id from teams t join full_roster f on (f.teamid=t.id)
join player p on (p.id=f.playerid)
where p.name='Joe Smith')
```
<div class="alert alert-block alert-info">
<b>Query:</b> List the team name, starting quarterback, and year for all the teams Joe Smith played on.
</div>

```sql
select
```
<div class="alert alert-block alert-info">
<b>Query:</b> List the team name, starting quarterback, and year for all the teams Joe Smith played on.
</div>