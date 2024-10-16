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

**Full join Query**
![full join query](images/fulljoin.png)

**Final result**
![full join result](images/fulljoinresult.png)



### ACID properties
#### PostgreSQL transaction
*What is a database transaction?*

A database transaction is a single unit of work that consists of one or more operations.

**Example**

A bank transfer from one account to another. A complete transaction must ensure a balance between the sender and receiver accounts.
 This implies that if the sender account transfers X amount, the receiver receives exactly X amount, neither more nor less.

A PostgreSQL transaction is atomic, consistent, isolated, and durable. These properties are often referred to collectively as ACID:

**Atomicity** guarantees that the transaction is completed in an all-or-nothing manner.

**Consistency** ensures that changes to data written to the database are valid and adhere to predefined rules.

**Isolation** determines how the integrity of a transaction is visible to other transactions.

**Durability** ensures that transactions that have been committed are permanently stored in the database.

Sample table

![sample table](images/sampletable.png)

![table data](images/sampledata.png)

![accounts table](images/accountstable.png)

1. **Atomicity**

Atomicity ensures that all parts of a transaction are completed or none are. If you perform a transaction that involves updating multiple accounts, it will either fully succeed or fully fail.

![atomicity](images/atomicity.png)

![atomic balance](images/atomicbalance.png)

2. **Consistency**

Consistency guarantees that transactions bring the database from one valid state to another, maintaining all rules (like the positive_balance constraint).

![consistency](images/consistency.png)

If this transaction results in a negative balance, it will fail and the COMMIT will not go through, ensuring data integrity.

3. **Isolation**

Isolation ensures that concurrent transactions don’t interfere. For example, if two users attempt to read and update Nina's balance simultaneously, one of them will need to wait until the other completes.



![isolation](images/isolation.png)

**Example: Transaction A:**
![isolation](images/transaction1.png)
 **Transaction B:**
![isolation](images/transaction2.png)


**Result of Isolation**

**Transaction A:** After committing, Nina Namalwa's balance is updated from $500 to $200.

**Transaction B:**

 Even if it starts before Transaction A commits, it sees Nina's balance as $500 at the time of the SELECT, not affected by Transaction A’s withdrawal until it commits.
After both transactions are complete:

Nina Namalwa: $200

Eva Nekesa: $3000

![isolation](images/finalisolation.png)

4.**Durability**

Durability ensures that once a transaction is committed, the data is permanently saved to the database, even if there’s a crash right afterward.

![durability](images/durability.png)

![durability result](images/durabilityresult.png)

Once committed, the change to Eva's balance is durable. Even if the database server crashes immediately afterward, Eva’s new balance will be preserved.

Each of these properties works to ensure that your data remains reliable, accurate, and resilient under various conditions.

 



