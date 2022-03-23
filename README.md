# Snowflake introduction

Content for the Snowflake introduction course

# Preparation before the course 

1. [Create Snowflake trial](#create-snowflake-trial)
1. [Take Snowflake for a spin](#take-snowflake-for-a-spin)
1. [Install Python](#install-python)


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

## Install Python
