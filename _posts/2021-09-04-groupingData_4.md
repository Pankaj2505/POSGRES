---
layout: post
title:  "4-Grouping Data"
date:   2021-09-04 09:04:08 +0530
categories: Notes
permalink: '/postgres/groupingdata'
---
### Topic To Cover 
    - order of execution 
	- Why Group by?
    - How group by?
    - Why having ?
    - How Having ?

#### order of execution 
FROM, JOIN,WHERE, GROUP BY, HAVING, SELECT, DISTINCT, ORDER BY and LIMIT clauses

#### Group by 

1. Why 
    - The GROUP BY clause divides the rows returned from the SELECT statement into groups.
    - For each group, you can apply an aggregate function.
2. How  

    - Select query will contain  column which are part of group by 
        - In this case, the GROUP BY works like the DISTINCT clause that removes duplicate rows from the result set.
        ```
            SELECT
                customer_id
            FROM
                payment
            GROUP BY
                customer_id;
        ```
    - Select query with agreggate fucntion can use column other than columns used in group by clause
        ```
            SELECT
                customer_id,
                SUM (amount)
            FROM
                payment
            GROUP BY
                customer_id;
        ```
        - The GROUP BY clause sorts the result set by customer id and adds up the amount that belongs to the same customer. Whenever the customer_id changes, it adds the row to the returned result set.


    
#### having
    1. Why ?
        - The HAVING clause is often used with the GROUP BY clause to filter groups or aggregates based on a specified condition.
    2. How ?
        ```
            SELECT
                column1,
                aggregate_function (column2)
            FROM
                table_name
            GROUP BY
                column1
            HAVING
                condition;
        ```

    3. HAVING vs. WHERE
        - The WHERE clause allows you to filter rows based on a specified condition.
        - The HAVING clause allows you to filter groups of rows according to a specified condition.