---
layout: post
title:  "6-Window Function"
date:   2021-09-06 09:04:08 +0530
categories: postgres
permalink: /:categories/:title
---
### Topic To Cover 
   1. Row_Number
   2. Rank
   3. Dense_Rank
   4. Percent_Rank
   5. First_Value
   6. Last_Value
   7. Lead
   8. Lag
   9. NTILE
   10. CUME_DIST


#### ROW_NUMBER
-  SQL Server ROW_NUMBER() function to assign a sequential integer to each row of a result set.

- Syntax 
	```
		ROW_NUMBER() OVER (
			[PARTITION BY partition_expression, ... ]
			ORDER BY sort_expression [ASC | DESC], ...
		)		
	```
- Example
	- if only order by clause is given , rows will be ordered based on column name
	```
		SELECT 
			ROW_NUMBER() OVER (
				ORDER BY first_name
			) row_num,
			first_name, 
			last_name, 
			city
		FROM 
			sales.customers;
	```
	- if only partition by clause is given , row no will asign to each group but in any order 
	- if both are given , row no will begin from 1 for each group , ordered on mentioned column name

#### Rank()
