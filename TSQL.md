## Database Normalization

  - I NF
    - One cell has one value.
    - All cells in each column have the same data type.
    - Each column has a unique name.
    - The order of rows doesn't matter.
   - II NF
    - All from I NF.

     


	
```diff 
+ Mark is functionality dependent on both StudentId and SubjectId.
- The teacher is partially dependent - only on SubjectId.
```


## Types of joins

![Types of Joins](T-SQL%20Joins.png "Types of Joins")
