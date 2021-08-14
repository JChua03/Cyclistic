# Cyclistic
Case study from Google Analytic

## Scenario

I am a junior data analyst in a marketing analyst team at Cyclistic, a bike-share company in Chicago. 
Director of marketing believes that company's future success depends on maximizing the number of annual memberships.

## About Cyclistic

Cyclistic launched in 2016 and grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago.

Until now, Cyclistic marketing strategy relied on building general awareness and appealing to broad consumer segments. There are different pricing plans which offers flexibility to the users. Pricing plans are as : single-ride passes, full-day passes, and annual memberships. Casual riders are customer who purchase single-ride and full-day passes whereas Cyclistic members are those who purchased annual memberships.

Financial analyst in Cyclistic has concluded that annual members are much more profitable than casual riders. Therefore, it is believe that the key to future growth was to maximize the number of annual members. It is also believe that it will be more beneficial to create a marketing campaign that targets casual members to become Cyclistic members. 

### Ask
Business Task: To launch a marketing campaign targeted to casual riders by identifying how casual and member riders uses Cyclistic differently.

### Prepare
Data source: [Data for Cyclistic] (https://divvy-tripdata.s3.amazonaws.com/index.html)
Data license: [License for Cyclistic] (https://www.divvybikes.com/data-license-agreement)

Data is organized monthly. 

Inside the data, it is broken down into multiple columns which are:
ride_id **The ID for each ride**
rideable_type **The type of bike used**
started_at **The date and time where the ride started**
ended_at **The date and time where the ride ended**
start_station_name **Station name where the ride started**
start_station_id **Station ID where the ride started**
end_station_name **Station name where the ride ended**
end_station_id **Station ID where the ride ended**
start_lat **The latitude of the station where the ride started**
start_lng **The longitude of the station where the ride started**
end_lat **The latitude of the station where the ride ended**
end_lng **The longitude of the station where the ride ended**
member_casual **The membership type of the riders**

The data is **Reliable** and **Original** as it is collected by Cyclistc.
It is also **Comprehensive** and **Current** as it only contains the data we need within the time frame we are interested in, which is a *12 month period*.

We will be able to use this data collected to find the difference between casual and members. 


### Process
The tools that I am using to process the data are Microsoft SQL and Excel.

Firstly, I am using the data from *July 2020 to June 2021* which is a 12 month period to study the difference of how casual and members uses Cyclistic.

I download and **Extract** the .zip file while using the appropriate file-naming convention.

While loading the data into Microsoft SQL the data type for every month is selected as follows.

ride_id nvarchar(50) null,
rideable_type nvarchar(50) null,
started_at datetime2(7) null,
ended_at datetime2(7) null,
start_station_name nvarchar(60) null ,
start_station_id nvarchar(60) null,
end_station_name nvarchar(60) null,
end_station_id nvarchar(60) null,
start_lat float null,
start_lng float null,
end_lat float null,
end_lng float null,
member_casual nvarchar(50) null

Then, I merge all the data from the past 12 months into a single table with 4,460,151 rows.

``` 
insert into cyclistic_v1
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
from [dbo].[Divvy_Trips_2020_07]
UNION ALL
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
from [dbo].[Divvy_Trips_2020_08]
UNION ALL
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
from [dbo].[Divvy_Trips_2020_09]
UNION ALL
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
from [dbo].[Divvy_Trips_2020_10]
UNION ALL
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
from [dbo].[Divvy_Trips_2020_11]
UNION ALL
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
from [dbo].[Divvy_Trips_2020_12]
UNION ALL
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
from [dbo].[Divvy_Trips_2021_01]
UNION ALL
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
from [dbo].[Divvy_Trips_2021_02]
UNION ALL
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
from [dbo].[Divvy_Trips_2021_03]
UNION ALL
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
from [dbo].[Divvy_Trips_2021_04]
UNION ALL
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
from [dbo].[Divvy_Trips_2021_05]
UNION ALL
select 
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual
  from [dbo].[Divvy_Trips_2021_06]
  ```

While looking through the data, I noticed that:
  1. There are `NULL` in the dataset.
  2. Some of the start station and end station consist of data where the bikes are sent to maintenance/testing. This needs to be removed.


```
--- Delete from the table where rows contain NULL as it is incomplete. 434382 rows affected.

from [dbo].[cyclistic_v1]
where ride_id is null
	OR rideable_type is null
	OR started_at is null
	OR ended_at is null
	OR start_station_name is null
	OR start_station_id is null
	OR end_station_name is null
	OR end_station_id is null
	OR start_lat is null
	OR start_lng is null
	OR end_lat is null
	OR end_lng is null
	OR member_casual is null

--- Delete from table where start or end station is a repair or maintenance site for Cyclistic. 3745 rows affected.

delete
from [dbo].[cyclistic_v1]
where start_station_id like '%test%' 
	OR start_station_name like '%test%'
	OR end_station_id like '%test%'
	OR end_station_name like '%test%'
```

I also added a constraint to check that there are no duplicates on ride_id, started_at and ended_at.
This constraints ensure that there are no single ride ID which started and ended on the exact same time.

```
alter table [dbo].[cyclistic_v1]
add constraint UC_ridejourney Unique (started_at, ended_at, ride_id)
```

Then, I would want to know how does each ride took.






