## Database Normalization

  - I NF
    - One cell has one value.
    - All cells in each column have the same data type.
    - Each column has a unique name.
    - The order of rows doesn't matter.
   - II NF
    - All from I NF.
    - The order of rows doesn't matter.
    - aaa
     

	| StudentId | SubjectId | Mark | Teacher |
	|-----------|-----------|------|---------|
	|     1     |     1     | 5.00 |  Niki   |  
	|     1     |     2     | 6.00 |  Pesho  |  
	|     2     |     1     | 5.50 |  Niki   |  
	
```diff 
+ Mark is functionality dependent on both StudentId and SubjectId.
- The teacher is partially dependent - only on SubjectId.
```


## Types of joins

![Types of Joins](T-SQL%20Joins.png "Types of Joins")
