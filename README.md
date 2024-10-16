# PostgreSQL DOCUMENT
## PostgreSQL Joins
### Inner Join
 An INNER JOIN is used in SQL to select records that have matching values in both tables involved in the join. When performing an INNER JOIN, only the rows where there is a match in both tables are returned. This is useful for retrieving data that has related information across multiple tables.

 #### Examples:
 Suppose you have two tables: students and courses. You want to retrieve the student name and courses details for each student:

  **students table**
  ![students data](images/students.png)
  **courses table**
 ![courses data](images/courses.png)

 To get the student name along with course details, you can use:

 ![inner join query](images/query.png)

 **Explanation of the Query**
 
 **SELECT Statement:** This selects the studentname and emailaddress from the students table (s) and the course from the courses table (c).
**FROM Clause:** It specifies that you are working with the students table (aliased as s).
**INNER JOIN Clause:** This joins the courses table (aliased as c) on the condition that s.courseid matches c.courseid. This means only the records where there is a corresponding courseid in both tables will be included in the result set.

 **Final result:**

 ![inner join result](images/result.png)


### Left Join
The LEFT JOIN keyword selects ALL records from the "left" table, and the matching records from the "right" table. The result is 0 records from the right side if there is no match.

**students**
![left join students data](images/leftstudent.png)
**courses**
![courses data](images/courses.png)

Now, we want to join these two tables so that we can see all students and their corresponding courses, if available. We'll use a left join to do this:

![left join query](images/leftquery.png)
**Final result**
![left join result](images/leftresult.png)

### Right join

The RIGHT JOIN keyword selects ALL records from the "right" table, and the matching records from the "left" table. The result is 0 records from the left side if there is no match.

**students**
![left join students data](images/leftstudent.png)
**courses**
![courses data](images/courses.png)

![right join query](images/rightquery.png)
 **Final result**

The RIGHT JOIN returns all records from the courses table.
Since there are no courses corresponding to courseid 450 in the courses table, the studentname, emailaddress, and studentid fields return NULL for that row.

![right join result](images/rightresult.png)

### Full Join

The FULL JOIN keyword selects ALL records from both tables, even if there is not a match. For rows with a match the values from both tables are available, if there is not a match the empty fields will get the value NULL.

**students**
![left join students data](images/leftstudent.png)
**courses**
![courses data](images/courses.png)

![full join query](images/fulljoin.png)

**Final result**
![full join result](images/fulljoinresult.png)







 



