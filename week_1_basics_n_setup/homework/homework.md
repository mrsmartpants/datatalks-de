

1. Which tag has the following text? - Write the image ID to the file

    --imageid string
    --iidfile string
    --idimage string
    --idfile string

Answer : --iidfile string


2. Run docker with the python:3.9 image in an iterative mode and the entrypoint of bash. docker run -it --entrypoint=bash python:3.9

Now check the python modules that are installed ( use pip list). How many python packages/modules are installed?

    1
    6
    3
    7


Anser : 3


3. How many taxi trips were totally made on January 15?

Tip: started and finished on 2019-01-15.

Remember that lpep_pickup_datetime and lpep_dropoff_datetime columns are in the format timestamp (date and hour+min+sec) and not in date.

    20689
    20530
    17630
    21090

Answer: 20530

select
    count(1)
from
    green_taxi_trips
where 
    lpep_pickup_datetime > '2019-01-15 00:00:00' 
    and
    lpep_dropoff_datetime < '2019-01-16 00:00:00'
	

4. Which was the day with the largest trip distance Use the pick up time for your calculations.

    2019-01-18
    2019-01-28
    2019-01-15
    2019-01-10

Answer : 2019-01-15

select
    tpep_pickup_datetime
from
    green_taxi_trips
where 
    trip_distance =
    (select max(trip_distance) from green_taxi_trips)
	
	
5. In 2019-01-01 how many trips had 2 and 3 passengers?

    2: 1282 ; 3: 266
    2: 1532 ; 3: 126
    2: 1282 ; 3: 254
    2: 1282 ; 3: 274

Answer : 2: 1282 ; 3: 254

select
    passenger_count, count(*)
from
    green_taxi_trips
where 
    cast(tpep_pickup_datetime as date)= '2019-01-01'
group by passenger_count
having passenger_count <=3


6. For the passengers picked up in the Astoria Zone which was the drop off zone that had the largest trip? We want the name of the zone, not the id.


    Central Park
    Jamaica
    South Ozone Park
    Long Island City/Queens Plaza

Answer: Long Island City/Queens Plaza

select
    t.tip_amount,
    pul."Zone" as pickup,
    dul."Zone" as dropoff
from
    green_taxi_trips t,
    zones pul,
    zones dul
where 
    t."PULocationID" = pul."LocationID"
    and
    t."DOLocationID" = dul."LocationID"
    and
    pul."Zone" like "Astoria"
order by
    t.tip_amount desc limit 1 


