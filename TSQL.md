## Database Normalization

  - I NF
    - One cell has one value.
    - All cells in each column have the same data type.
    - Each column has a unique name.
    - The order of rows doesn't matter.
   - II NF
    - All from I NF
    - No partial dependencies.
    
    
        |-------+-----------+------+---------|  
	|&nbsp;StdId&nbsp;|&nbsp;SubjectId&nbsp;|&nbsp;Mark&nbsp;|&nbsp;Teacher&nbsp;|  
	|-------+-----------+------+---------|  
	|&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;5.00&nbsp;|&nbsp;&nbsp;Niki&nbsp;&nbsp;&nbsp;|  
	|-------+-----------+------+---------|  
	|&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;6.00&nbsp;|&nbsp;&nbsp;Pesho&nbsp;&nbsp;|  
	|-------+-----------+------+---------|  
	|&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;5.50&nbsp;|&nbsp;&nbsp;Niki&nbsp;&nbsp;&nbsp;|  
	|-------+-----------+------+---------|   

## Types of joins

![Types of Joins](T-SQL%20Joins.png "Types of Joins")
