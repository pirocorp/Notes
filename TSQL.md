## Database Normalization

  - I NF
    - One cell has one value.
    - All cells in each column have the same data type.
    - Each column has a unique name.
    - The order of rows doesn't matter.
   - II NF
    - All from I NF
    - No partial dependencies.
     

	| StdId | SubjectId | Mark | Teacher |
	|-------|-----------|------|---------|
	|	|	    |```diff|         |
	|   1   |     1     |- 5.00|  Niki   |  
	|       |           |```   |         |
	|   1   |     2     | 6.00 |  Pesho  |  
	|   2   |     1     | 5.50 |  Niki   |  
	
```diff 
- text in red 
```


## Types of joins

![Types of Joins](T-SQL%20Joins.png "Types of Joins")
