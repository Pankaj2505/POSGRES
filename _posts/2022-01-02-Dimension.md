---
layout: post
title:  "Understanding Dimension"
date:   2022-01-02 09:04:08 +0530
categories: Notes
---
- challange 
	> from available data set which entity is fact and which entity is dimesion 

- Example 
	retail data set [date , store , product, quantity , unit price, sales amount , transaction no, saletax, product in hand]
	
	1. first check how many entities are text and number
		- text[date , store , product]
		- Number [ quantity , unit price, sales amount , transaction no,saletax, product in hand]
		
	2. Fact - in general [any numeric entity which is measurable]  
		- for example quantity , unit price, sales amount . they all are measurable.
		- if you write fact as number , they are meaning less, you will not know what this no is.
		- it provide quantitative information about business like total sale in an year.
		- we should ask question like , what is total no of product sold for product A ?
		- Not all numeric values are Fact, for example Transaction no is numeric but its a degenerated dimensions.
	
	3. Dimension - [dimensions are those entities which explain about facts.dimension has attribute.
		- for example [date , store , product] 
		- dimensions are explaining these features[ what, time, geography,product]
		- These are descriptive entities.
		- __some time we define number values are dimensions also called degenerated dimensions__		
		- example 
			- people [customer, vendors, patient , providers]
			- product [eatable, machinery, eductaional]
			- place [country, continent , city , street, landmark,house no]
			- time [year, month, day, hours ,minute, second]

- Challange
	> how to categorise dimension,
	Retail transaction data[Date , Product, Store, orderNo, Paymant mode, Storetype, CustomerAssistence , quantity, UnitPrice]
	Fact - [quantity, UnitPrice]
	dimesnion -[Date , Product, Store, orderNo, Paymant mode, Storetype, CustomerAssistence] 
		
	fact table-[PK_No, dateFK, ProductFK, StoreFK]	
		
		1. Junk Dimension:
			- __why do we need__
				- out of all dimensional entities  there can be entities which contain categorical data.
				- if they contain only 2 repetitive data, its waste to have a saperate dimesion for them.
				- but if they have large no of categorical data , we should create saperat dimension .
				- it means they contain highest duplicates for example [Paymant mode(Cash, cedit, check ), Store Type(offline , online), Customer assistence(yes ,no)]
				- so here rather than keeping saperate dimesnion for them , its better to create a dimension table with cartisian product of them .
			-__How to create it__
				- let say emtities - 3 , each categorical value is 3. so how many cartisian product needed , 3*3*3 = 27.
				- we can keep the surrgate key of this junk dimesnion with fact table.
				- let say there are 10 entities with categorise = 2 , so total needed row, 2^10 = 1024
				- entitiy 3, categorise = 4 so row = 3*4 = 81
				- now if 4 entities has 100 categorical values, we can create saperate dimesnion for each entity as this will create a huge JUnk dimension table .
			
		2. Conformed Dimension:
			- __Why do we need it __
				- if two fact table uses common dimesnion like date. then we can write one dimension table in such a way that all fact tables can use it.
				- for example - finance:[budgetyear] HR:[calenderyear]
				- __Disadvantage__ - More maintenance , ETL work, Joining multiple data mart.
				- we can use it to link two datamart  like: return sale and product quantity when date is 31-jan-2121
			- __What__
				- when we refer two fact table, if they contain common dimesion having same description,same PK or one is subset of other are called Conformed Dimesnion.
				- This dimension can be resued accross project.
				- we should maintain integrity. keep single table accross project.
				
		3. Role -Playing Dimension:
			- __Why__
				- same dimension is used for different purpose
				- Date [manufacturing date, packaging date, sale date, expiry date, shipping date]
				- Address [shipping address, customer address, shipped address]
			- __question__ : How to Store this dimension in fact table
				- we should create one master time dimesion and then create multiple views for each date table, and then add PK of each view as FK in Fact table.
				
		4. Degenrate Dimension:
			- __Why __ 
				- those entities why can not be measured and they does not have further attribute, like transaction No.
				- these entitites has one on one relation with fact, like order no,transaction no.
				- these Dimension sits on fact table with each fact.
				
> Challange 
	- Structure of dimension table 
		- Retail[date , store, product , transaction] are dimesion 
		- Attribute assosicated with store Dimension
			- StoreSurrogate Key
			- StorePK
			- street name 
			- city name
			- state 
			- country 
			- zip code
	- propertise
		- denormallize
		- Verbose
		- it contain unique meaning
			
				
				
				