with df as (select distinct o.customerNumber, 
TIMESTAMPDIFF(DAY, MAX(orderDate), ('2005-05-31')) as Recency, 
count(distinct o.orderNumber) as Frequency, 
SUM(priceEach*quantityOrdered) as Monetary 
from orders as o 
inner join orderdetails o2 on o.orderNumber = o2.orderNumber 
group by customerNumber) 
select customerNumber, Frequency, Recency, Monetary, 
case when ROUND(PERCENT_RANK() OVER (order by Frequency),3)<0.20 then '1' 
when ROUND(PERCENT_RANK() OVER (order by Frequency),3) BETWEEN 0.20 and 0.40 then '2' 
when ROUND(PERCENT_RANK() OVER (order by Frequency),3) BETWEEN 0.40 and 0.60 then '3' 
when ROUND(PERCENT_RANK() OVER (order by Frequency),3) BETWEEN 0.60 and 0.80 then '4' 
else '5' end as Frequency_rank, 
case when ROUND(PERCENT_RANK() OVER (order by Recency),3)<0.20 then '1' 
when ROUND(PERCENT_RANK() OVER (order by Recency),3) BETWEEN 0.20 and 0.40 then '2' 
when ROUND(PERCENT_RANK() OVER (order by Recency),3) BETWEEN 0.40 and 0.60 then '3' 
when ROUND(PERCENT_RANK() OVER (order by Recency),3) BETWEEN 0.60 and 0.80 then '4' 
else '5' end as Recency_rank, 
case when ROUND(PERCENT_RANK() OVER (order by Monetary),3)<0.20 then '1' 
when ROUND(PERCENT_RANK() OVER (order by Monetary),3) BETWEEN 0.20 and 0.40 then '2' 
when ROUND(PERCENT_RANK() OVER (order by Monetary),3) BETWEEN 0.40 and 0.60 then '3' 
when ROUND(PERCENT_RANK() OVER (order by Monetary),3) BETWEEN 0.60 and 0.80 then '4' 
else '5' end as Monetary_rank 
from df 
group by customerNumber, Frequency,Recency,Monetary
