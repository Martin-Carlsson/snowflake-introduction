# Snowflake introduction

Content for the Snowflake introduction course

# Preparation before the course 

1. [Create Snowflake trial](#create-snowflake-trial)
1. [Take Snowflake for a spin](#take-snowflake-for-a-spin)
1. [Install Python](#install-python)
1. [Install Docker Desktop](#install-docker-desktop)
1. [Install git](#install-git)

## Create Snowflake trial

Go to [signup.snowflake.com](https://signup.snowflake.com/) and create a trial

Choose
 - Enterprise (the higher the tier, the more features and more expensive compute)
 - AWS (newer Snowflake features are rolled out on AWS before other platforms)
 - Location (just what is closest to you)

<img width="365" alt="image" src="https://user-images.githubusercontent.com/7769335/159672379-fd9e5cfa-a318-4b15-8d24-e730877d4909.png">

Activate your account via your e-mail

Write down:
- User name
- Password
- Link to your account (the part before ".snowflakecomputing.com" is the important part)
  - Example: xy97133.eu-central-1.snowflakecomputing.com
<img width="363" alt="image" src="https://user-images.githubusercontent.com/7769335/159674460-7efb31f1-9d25-47f3-9dc2-6a4d6af1f15f.png">


## Take Snowflake for a spin

- Click on **Worksheets**
- Click on **+ Worksheet**

<img width="1399" alt="image" src="https://user-images.githubusercontent.com/7769335/159688978-9f65593a-b58d-440e-a963-6d415c57840d.png">

Run the following code:
```sql
select top 100 
    *
from
    snowflake_sample_data.tpch_sf10.orders;
```

To run code, hit the run button in the top left:

<img width="46" alt="image" src="https://user-images.githubusercontent.com/7769335/159689722-20a486cd-fa4e-4281-9d1a-2bb0cfaa5427.png">
 

If you see this, congratulations you are a now a Snowflake user ❄️💪
<img width="1437" alt="image" src="https://user-images.githubusercontent.com/7769335/159690141-75d376c3-eaf4-4b64-8e30-814351d82c6d.png">

### 50,400,240,948

To feel the power of Snowflake.

```sql
use schema snowflake_sample_data.tpcds_sf10tcl; --50b
use schema snowflake_sample_data.tpcds_sf10tcl; --500b

alter session set use_cached_result = true;

-- Count
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


with store_sales_fields as (
    select
        'store_sales' as sales_type,
        ss_sold_date_sk as date_id,
        ss_net_profit as profit 
    from
        store_sales
),

catalog_sales_fields as (
    select
        'catalog_sales' as sales_type,
        cs_sold_date_sk as date_id,
        cs_net_profit as profit
    from
        catalog_sales
),

 web_sales_fields as (
    select
        'web_sales' as sales_type,
        ws_sold_date_sk as date_id,
        ws_net_profit as profit
    from
        web_sales
),
 
unioned_sales as (
    select * from store_sales_fields
        union all
    select * from catalog_sales_fields
        union all
    select * from web_sales_fields
),

date_fields as (
    select
        d_date_sk as date_id,
        d_year as year
    from
        date_dim
)

-- Group By with Sum and Count
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

alter warehouse xxlargewarehouse suspend;
```

## The advanced part

We will use a Python, git and, docker to load data into Snowflake.

### Install Python

Go to [python.org](https://www.python.org/), download and install Python.

<img width="971" alt="image" src="https://user-images.githubusercontent.com/7769335/159690661-6719e4d4-74e8-4fcf-be20-90d02ba2cb42.png">

On Windows you should choose **Add Python to PATH**
![image](https://user-images.githubusercontent.com/7769335/159690932-944f52aa-f543-4b3b-8501-f72ceead2530.png)

### Test Python installation

- **On Windows:** open CMD
- **On Mac:** open Terminal

Run the following command:

```bash
python --version
```
*Or, if that didn't work, try:*
```bash
python3 --version
```

If you see something like this, Python is installed correctly:

<img width="419" alt="image" src="https://user-images.githubusercontent.com/7769335/159692201-b225e9b3-75df-44b0-93bb-03502940d49c.png">


### Install docker desktop

Install Docker desktop from: [www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

You may need to create an account on [hub.docker.com/signup](https://hub.docker.com/signup)

### Install git 

#### On Mac

Type this in to the Terminal:

```bash
git --version
```

If git is installed, you will see the installed version number.

If git inn't installed, the installation will start.

#### On Windows

Install from [git-scm.com/download/win](https://git-scm.com/download/win) choose **64-bit Git for Windows Setup.**
