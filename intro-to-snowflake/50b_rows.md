# Snowflake SQL for testrunning 50.000.000.000 rows

## Setup 
```sql
use database snowflake_sample_data;

use schema tpcds_sf10tcl; --50b
use schema tpcds_sf100tcl; --500b

--use role accountadmin;

--use warehouse xxlargewarehouse;

--alter warehouse xxlargewarehouse resume;

--alter session set use_cached_result = true;
```


## Count rows

```sql
with row_count as (
    select 'store_sales' as name, count(*) as row_count from store_sales
        union all
    select 'catalog_sales' as name, count(*) as row_count from catalog_sales
        union all
    select 'web_sales' as name, count(*) as row_count from web_sales
        union all
    select 'date_dim' as name, count(*) as row_count from date_dim
),

row_count_total as (
    select 'row_count_total' as name, sum(row_count) from row_count
)

select * from row_count
    union all
select * from row_count_total;
```


## Group By with Sum and Count
```sql
select
    unioned_sales.sales_type,
    date_fields.year, 
    sum(abs(profit)) as sum_of_profit,
    count(*) as number_of_rows
from
    unioned_sales
    left join date_fields on unioned_sales.date_id = date_fields.date_id
where
    date_fields.year is not null
group by
    1, 2
order by 
    1,2;
```

## Clean up
```sql
alter warehouse xxlargewarehouse suspend;
```
