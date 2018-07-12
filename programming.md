## Programming (14 questions)

#### 1. Write a function to calculate all possible assignment vectors of 2n users, where n users are assigned to group 0 (control), and n users are assigned to group 1 (treatment).
  - Recursive programming (sol in code)
```python
def n_choose_k(n, k):
    """ function to choose k from n """
    if k == 1:
        ans = []
        for i in range(n):
            tmp = [0] * n
            tmp[i] = 1
            ans.append(tmp)
        return ans

    if k == n:
        return [[1] * n]

    ans = []
    space = n - k + 1
    for i in range(space):
        assignment = [0] * (i + 1)
        assignment[i] = 1
        for c in n_choose_k(n - i - 1, k - 1):
            ans.append(assignment + c)
    return ans

# test: choose 2 from 4
print(n_choose_k(4, 2))
```

#### 2. Given a list of tweets, determine the top 10 most used hashtags.
  - Store all the hashtags in a dictionary and use priority queue to solve the top-k problem
  - An extension will be top-k problem using Hadoop/MapReduce

#### 3. Program an algorithm to find the best approximate solution to the knapsack problem in a given time.
  - [https://en.wikipedia.org/wiki/Knapsack_problem](https://en.wikipedia.org/wiki/Knapsack_problem)
  - Greedy solution (add the best v/w as much as possible and move on to the next)
  - Dynamic programming

#### 4. Program an algorithm to find the best approximate solution to the traveling salesman problem in a given time.
  - [https://en.wikipedia.org/wiki/Travelling_salesman_problem](https://en.wikipedia.org/wiki/Travelling_salesman_problem)
  - Greedy
  - Dynamic programming

#### 5. You have a stream of data coming in of size n, but you don’t know what n is ahead of time. Write an algorithm that will take a random sample of k elements. Can you write one that takes O(k) space?
  - [Reservoir sampling](https://en.wikipedia.org/wiki/Reservoir_sampling)

#### 6. Write an algorithm that can calculate the square root of a number.
  - Binary search or Newton's method

#### 7. Given a list of numbers, can you return the outliers?
  - Sort then select the highest and the lowest 2.5%
  - Visualization can helps a lot

#### 8. When can parallelism make your algorithms run faster? When could it make your algorithms run slower?
  - Ask someone for more details.
  - compute in parallel when communication cost < computation cost
    - ensemble trees
    - minibatch
    - cross validation
    - forward propagation
    - minibatch
    - not suitable for online learning

#### 9. What are the different types of joins? What are the differences between them?
  - Inner Join, Left Join, Right Join, Outer Join, Self Join

#### 10. Why might a join on a subquery be slow? How might you speed it up?
  - Change the subquery to a join.
  - [Stack Overflow Answers](https://stackoverflow.com/questions/31724903/why-might-a-join-on-a-subquery-be-slow-what-could-be-done-to-make-it-faster-s)

#### 11. Describe the difference between primary keys and foreign keys in a SQL database.
  - Primary keys are columns whose value combinations must be unique in a specific table so that each row can be referenced uniquely.
  - Foreign keys are columns that references columns (often primary keys) in other tables.

#### 12. Given a **COURSES** table with columns **course_id** and **course_name**, a **FACULTY** table with columns **faculty_id** and **faculty_name**, and a **COURSE_FACULTY** table with columns **faculty_id** and **course_id**, how would you return a list of faculty who teach a course given the name of a course?
```SQL
SELECT f.faculty_name
FROM COURSES c
JOIN COURSE_FACULTY cf
    ON c.course_id = cf.course_id
JOIN FACULTY
    ON f.faculty_id = cf.faculty_id
WHERE c.course_name = xxx;
```

#### 13. Given a **IMPRESSIONS** table with **ad_id**, **click** (an indicator that the ad was clicked), and **date**, write a SQL query that will tell me the click-through-rate of each ad by month.
```SQL
SELECT ad_id, MONTH(date), AVG(click)
FROM IMPRESSIONS
GROUP BY ad_id, MONTH(date);
```

#### 14. Write a query that returns the name of each department and a count of the number of employees in each:  
- **EMPLOYEES** containing: **Emp_ID** (Primary key) and **Emp_Name**  
- **EMPLOYEE_DEPT** containing: **Emp_ID** (Foreign key) and **Dept_ID** (Foreign key)  
- **DEPTS** containing: **Dept_ID** (Primary key) and **Dept_Name**
```SQL
SELECT d.Dept_Name, COUNT(*)
FROM DEPTS d
LEFT JOIN EMPLOYEE_DEPT ed
    ON d.Dept_ID = ed.Dept_ID
GROUP BY d.Dept_Name;
```
