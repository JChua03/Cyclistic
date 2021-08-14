# Cyclistic
Case study from Google Analytic.

# Scenario

I am a junior data analyst in a marketing analyst team at Cyclistic, a bike-share company in Chicago. 
Director of Marketing, Lily Moreno believes that company's future success depends on maximizing the number of annual memberships.

## About Cyclistic

Cyclistic launched in 2016 and grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago.

Until now, Cyclistic marketing strategy relied on building general awareness and appealing to broad consumer segments. There are different pricing plans which offers flexibility to the users. Pricing plans are as : single-ride passes, full-day passes, and annual memberships. Casual riders are customer who purchase single-ride and full-day passes whereas Cyclistic members are those who purchased annual memberships.

Financial analyst in Cyclistic has concluded that annual members are much more profitable than casual riders. Therefore, it is believe that the key to future growth was to maximize the number of annual members. It is also believe that it will be more beneficial to create a marketing campaign that targets casual members to become Cyclistic members. 

*For this case study, I will be using the Google Data Analytics Certificate processes to provide recommendation to the Director of Marketing.*

# Ask
Business Task: To launch a marketing campaign targeted to casual riders by identifying how casual and member riders uses Cyclistic differently.

# Prepare
Data source: [Data for Cyclistic](https://divvy-tripdata.s3.amazonaws.com/index.html)

Data license: [License for Cyclistic](https://www.divvybikes.com/data-license-agreement)

The data is organized monthly and broken down into multiple columns which are:

|Column 		| Explaination						|
| --------------------- |-------------------------------------------------------|
|ride_id 		| The ID for each ride 					|
|rideable_type		| The type of bike used 				|
|started_at 		| The date and time where the ride started 		|
|ended_at 		| The date and time where the ride ended 		|
|start_station_name 	| Station name where the ride started 			|
|start_station_id 	| Station ID where the ride started 			|
|end_station_name 	| Station name where the ride ended 			|
|end_station_id 	| Station ID where the ride ended 			|
|start_lat 		| The latitude of the station where the ride started 	|
|start_lng 		| The longitude of the station where the ride started 	|
|end_lat 		| The latitude of the station where the ride ended 	|
|end_lng 		| The longitude of the station where the ride ended 	|
|member_casual 		| The membership type of the riders 			|


The data is **Reliable** and **Original** as it is collected by Cyclistc.

It is also **Comprehensive** and **Current** as it only contains the data we need within the time frame we are interested in, which is a *12 month period*.


We will be able to use this data collected to find the difference between casual and members. 


# Process
The tools that I am using to process the dataset are Microsoft SQL and Excel.

Firstly, I am using the data from *July 2020 to June 2021* which is a 12 month period to study the difference of how casual and members uses Cyclistic.

I download and **Extract** the .zip file while using the appropriate **file-naming convention**.

While loading the data into Microsoft SQL the data type for every month is selected as follows.

``` sql
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
```

Then, I merge all the data from the past 12 months into a single table.

``` sql
--- This creates cyclistic_v1 with 4,460,151 rows.
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
  2. Some of the `start_station` and `end_station` consists of data where the bikes are sent to maintenance or testing which needs to be removed.


```sql
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

I also added a constraint to check that there are no duplicates on `ride_id`, `started_at` and `ended_at`.
This constraints ensure that there are no single ride ID which started and ended on the exact same time.

```sql
alter table [dbo].[cyclistic_v1]
add constraint UC_ridejourney Unique (started_at, ended_at, ride_id)
```

Then, I would want to know how does each ride took in minutes.

```sql 
select datediff(minute,started_at, ended_at) as ride_length_min, *
from [dbo].[cyclistic_v1]
```

Upon checking the query, I noticed that some of the `ride_length_min` are negative values. This does not make sense as it suggests that the ride ended earlier than it started. 

I also noticed that some rides took more than 24 hours. I removed them as [this link](https://help.divvybikes.com/hc/en-us/articles/360033484791-What-if-I-keep-a-bike-out-too-long-) suggest that bike rental longer than 24 hours (1440 minutes) are considered lost.

```sql
--- Delete negative value ride_length and ride_length that exceed 24 hours. 5107 rows affected.

delete
from [dbo].[cyclistic_v1]
where datediff(minute,started_at, ended_at) > 1440
	OR 
	datediff(minute,started_at, ended_at) <0
```

# Analyze
I begin my analysis by analyzing the most obvious to more specific details.

I started with the **number of rides** from July 2020 to June 2021.

```sql
--- Total rides from July 2020 to June 2021. 4,016,917 rides.

select count(*) as total_rides
from [dbo].[cyclistic_v1]
```

Does the **type of bikes** affect how Cyclistic user uses the bikes?

``` 
select rideable_type,
		count(*) as num_rides_by_type,
		member_casual
from [dbo].[cyclistic_v1]
group by rideable_type,
		member_casual
```

I was curious as to how does **time, day and month** affect the user type. Therefore, I ran the below query.

```sql

select member_casual,
		--- time
		datepart(hour,started_at) as hour_start,
		--- daylight
		(case when datepart(hour,started_at) in (0,1,2,3,4,5,6,7,8,9,10,11) then 'morning'
			when datepart(hour,started_at) in (12,13,14,15,16,17) then 'afternoon'
			when datepart(hour,started_at) in (18,19,20,21,22,23) then 'evening'
		end) as daylight,
		--- day 
		datepart(day,started_at) as day_start,
		--- weekday
		datepart(weekday,started_at) as weekday_start,
		--- month
		datepart(month,started_at) as month_start,
		--- season
		(case when datepart(month,started_at) in (12,1,2) then 'winter'
			when datepart(month,started_at) in (3,4,5) then 'spring'
			when datepart(month,started_at) in (6,7,8) then 'summer'
			when datepart(month,started_at) in (9,10,11) then 'autumn'
		end) as season, 
		count(*) as num_rides
from [dbo].[cyclistic_v1]
group by datepart(hour,started_at),
		datepart(day,started_at),
		datepart(month,started_at),
		datepart(weekday,started_at),
		member_casual
order by datepart(hour,started_at),
		datepart(day,started_at),
		datepart(month,started_at),
		datepart(weekday,started_at)
```

Does user have a preference of where the bikes are **located**?

```
--- Start station preference

select count(start_station_name) as most_frequent_start_station_name, 
		start_station_name, 
		member_casual
from [dbo].[cyclistic_v1]
group by start_station_name,
		member_casual
order by count(start_station_name) DESC

--- End station preference

select count(end_station_name) as most_frequent_end_station_name,
		end_station_name, 
		member_casual
from [dbo].[cyclistic_v1]
group by end_station_name, 
		member_casual
order by count(end_station_name) DESC
```

# Share
Please refer to [Tableau] for the visualization.

# Act
**1. Marketing campaign launch on the busiest month of the year from June to August.**

**2. Increase price for single-ride and single-day passes on weekends to promote membership subscription.**

**3. Advertisement place around the coast to promote annual membership benefits.**

**4. Increase the number of bike station furthe away from the coast to promote Cyclistic as the main type of transport.**



