## Database Normalization

### I NF
- One cell has one value.
- All cells in each column have the same data type.
- Each column has a unique name.
- The order of rows doesn't matter.
    
### II NF
- All from I NF.
- No partial dependencies
  
<br />

| StudentId | SubjectId | Mark | Teacher |
|-----------|-----------|------|---------|
|     1     |     1     | 5.00 |  John   |  
|     1     |     2     | 6.00 |  Tom    |  
|     2     |     1     | 5.50 |  John   |  
     
```diff 
# P is primary column NP is non-primary
+ Mark is functionality dependent on both StudentId and SubjectId. (P -> NP)
- The Teacher is partially dependent - only on SubjectId. (0.5 P => NP)
@@ A possible solution is to move the Teacher column in the Subject table. @@
```

### III NF
- All from II NF.
- No transitional dependencies.

<br />    

| Id | StudentId | SubjectId | Mark |   Exam   | Max Score |
|----|-----------|-----------|------|----------|-----------|
| 1  |     1     |     1     | 3.50 |  Theory  |   6.00    |
| 2  |     1     |     2     |  85  | Practice |    100    |
| 3  |     2     |     1     |  82  | Practice |    100    |


```diff 
# P is primary column NP is non-primary
- The Max Score is dependant on the Exam column, which is not a key column (transitional dependency). (A -> B, B -> C => A -> C) (NP -> NP)
+ And Exam is dependant on SubjectId (functionally dependency). (P -> NP)
@@ A possible solution is to move the Exam and Max Score to a new table and add a column with a foreign key pointing to the new table. @@
```

| Id | StudentId | SubjectId | Mark | ExamMaxScoreId |
|----|-----------|-----------|------|----------------|
| 1  |     1     |     1     | 3.50 |       1        |
| 2  |     1     |     2     |  85  |       2        |
| 3  |     2     |     1     |  82  |       2        |

<br />

| Id |   Exam   | Max Score |
|----|----------|-----------|
| 1  |  Theory  |   6.00    |
| 2  | Practice |    100    |

### III.V NF (BCNF)
- All from III NF.
- If A -> B, but A must be super-key.

<br />
    
| StudentId |  Subject  |  Teacher  |  Mark  |
|-----------|-----------|-----------|--------|
|     1     |     C#    |   Jhon    |  5.00  |
|     2     |   Python  |    Tom    |  5.50  |
|     3     |     C#    |    Bob    |  6.00  |


| Id |  Subject  |  Teacher  |
|----|-----------|-----------|
| 1  |     C#    |   Jhon    |
| 2  |   Python  |    Tom    |
| 3  |     C#    |    Bob    |

```diff 
# P is primary column NP is non-primary
+ Mark is functionality dependent on both StudentId and SubjectId. (P -> NP)
- Teacher defines Subject which is super-key (A -> B, but B is super-key) (NP -> P)
@@ A possible solution is to remove the Teacher and Subject columns and to point to Teacher table @@
```

| StudentId |  TeacherId  |  Mark  |
|-----------|-------------|--------|
|     1     |      1      |  5.00  |
|     2     |      2      |  5.50  |
|     3     |      3      |  6.00  |


| Id |  Subject  |  Teacher  |
|----|-----------|-----------|
| 1  |     C#    |   Jhon    |
| 2  |   Python  |    Tom    |
| 3  |     C#    |    Bob    |

### IV NF
- All from III.V NF (BCNF).
- No multi-valued dependency.

<br />

| StudentId |  Course  |  Hobby   |
|-----------|----------|----------|
|     1     |    C#    | Football |
|     2     |    PHP   |  Tenis   |
|     1     |  Python  |   SC2    |

```diff 
- Columns Course and Hobby are not rellated (multi-valued dependency).
@@ A possible solution is to split this table into two tables @@
```

| Id | StudentId |  Course  |
|----|-----------|----------|
| 1  |     1     |    C#    |
| 2  |     2     |    PHP   |
| 3  |     1     |  Python  |

   
| Id | StudentId |  Hobby   |
|----|-----------|----------|
| 1  |     1     | Football |
| 2  |     2     |  Tenis   |
| 3  |     1     |   SC2    |

## Types of joins

![Types of Joins](T-SQL%20Joins.png "Types of Joins")
