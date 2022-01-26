---
layout: post
title:  "5-Aggregate Function"
date:   2021-09-05 09:04:08 +0530
categories: Notes
permalink: '/postgres/aggregatefunction'
---
### Topic To Cover 
    1. Count
    2. AVG
	3. array_agg
	4. sum
	5. String_agg
	6. max , min

    
#### COUNT
	- COUNT(*) function 
		1. returns the number of rows , including NULL and duplicates.
		2. PostgreSQL has to scan the whole table sequentially.
		
	- COUNT(column) function 
		1. returns the number of rows , it does not consider NULL values in the column but consider duplicates
		
	- COUNT(DISTINCT column) 
		1. returns the number of unique non-null values in the column.

	> We often use the COUNT() function with the GROUP BY clause to return the number of items for each group.
	> check for duplicate row 
		```
			select name , count(*)
			from student 
			group by name 
			having count(name) > 1
		```
	
	
#### AVG
	> AVG() function ignores NULL values.
    > this will include duplicate also 
	
	1. AVG() function allows you to calculate the average value of a set.  
        ```
            SELECT AVG( amount)::numeric(10,2)
            FROM payment;
        ```
	    
	
	2. You can use the AVG() function in the SELECT and HAVINGclauses.
	
	3. AVG(DISTINCT column)  
        ```
        SELECT AVG(DISTINCT amount)::numeric(10,2)
        FROM payment;
        ```    
	    > this will avoid avg of duplicate amounts
	
	4. with group by   
	```
		SELECT
			customer_id,
			first_name,
			last_name,
			AVG (amount)::NUMERIC(10,2)
		FROM
			payment
		INNER JOIN customer USING(customer_id)
		GROUP BY
			customer_id
		ORDER BY
		customer_id;
	```


 #### array_agg()

	1. array_agg(col) will create array with col element for each group. 
	2. __return the list of film title and a list of actors for each film:__  
	3. syntax: ARRAY_AGG(expression [ORDER BY [sort_expression {ASC | DESC}], [...])
	
	```	
		table used public.film,public.film_actor,public.actor

		select f.title,a.first_name||' '||a.last_name as actor

		from public.film f join public.film_actor fa 
		on f.film_id= fa.film_id
		join public.actor a
		on fa.actor_id = a.actor_id;


		select 
			f.title,
			array_agg (a.first_name||' '||a.last_name) as actor
		from 
			public.film f join public.film_actor fa 
			on f.film_id= fa.film_id
			join public.actor a
			on fa.actor_id = a.actor_id
		group by 
			f.title;

```
	
	|actor|movie|
	|-----|-----|
	|"Ace Goldfinger"	| "{""Minnie Zellweger"",""Chris Depp"",""Bob Fawcett"",""Sean Guiness""}" |
	|"Adaptation Holes"	| "{""Cameron Streep"",""Bob Fawcett"",""Nick Wahlberg"",""Ray Johansson"",""Julianne Dench""}" |
	|"Affair Prejudice"	| "{""Jodie Degeneres"",""Kenneth Pesci"",""Fay Winslet"",""Oprah Kilmer"",""Scarlett Damon""}" |



#### SUM()
	- The SUM() function ignores NULL. It means that SUM() doesn’t consider the NULL in calculation.

	- If you use the DISTINCT option, the SUM() function calculates the sum of distinct values.

	```
		SELECT SUM (amount) AS total
		FROM payment
		WHERE customer_id = 2000;
	```

	- let say there is no row for customer_id = 2000;
	- function will return null
	- now if you want to return 0 instead use coalesce function
	- The COALESCE( first, second) function returns the first non-null argument. In other words, it returns the second argument if the first argument is NULL.

	```
		SELECT 
			COALESCE(SUM(amount),0) AS total
		FROM 
			payment
		WHERE 
			customer_id = 2000;
	```

#### string_agg()
 - The STRING_AGG() is similar to the ARRAY_AGG() function except for the return type. - The return type of the STRING_AGG() function is the string.
 - The return type of the ARRAY_AGG() function is the array.

	```
		SELECT
			f.title,
			STRING_AGG (
			a.first_name || ' ' || a.last_name,
				','
			ORDER BY
				a.first_name,
				a.last_name
			) actors
		FROM
			film f
		INNER JOIN film_actor fa USING (film_id)
		INNER JOIN actor a USING (actor_id)
		GROUP BY
			f.title;
	```


#### MAX () or min()

- The max() function ignores NULL.
