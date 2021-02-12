## Database Normalization

  - I NF
    - One cell has one value.
    - All cells in each column have the same data type.
    - Each column has a unique name.
    - The order of rows doesn't matter.
    
- II NF
    - All from I NF.
    - No partial dependencies
  
<br />

| StudentId | SubjectId | Mark | Teacher |
|-----------|-----------|------|---------|
|     1     |     1     | 5.00 |  John   |  
|     1     |     2     | 6.00 |  Tom    |  
|     2     |     1     | 5.50 |  John   |  
     
```diff 
+ Mark is functionality dependent on both StudentId and SubjectId.
- The teacher is partially dependent - only on SubjectId.
@@ A possible solution is to move the Teacher column in the Subject table. @@
```

- III NF
    - All from II NF.
    - No transitional dependencies.

<br />    

| Id | StudentId | SubjectId | Mark |   Exam   | Max Score |
|----|-----------|-----------|------|----------|-----------|
| 1  |     1     |     1     | 3.50 |  Theory  |   6.00    |
| 2  |     1     |     2     |  85  | Practice |    100    |
| 3  |     2     |     1     |  82  | Practice |    100    |


## Types of joins

![Types of Joins](T-SQL%20Joins.png "Types of Joins")
