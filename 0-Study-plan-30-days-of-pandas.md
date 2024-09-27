>This ultimate Revision page for Pandas with Leetcode questions

Table of Content
--
- [Data Filtering](#data-filtering)
- [String Methods](#string-methods)
  - [1683. Invalid Tweets  \[`Easy`\]](#1683-invalid-tweets--easy)
  - [1873. Calculate Special Bonus \[`Easy`\]](#1873-calculate-special-bonus-easy)
  - [1667. Fix Names in a Table \[`Easy`\]](#1667-fix-names-in-a-table-easy)
    - [Solution 1](#solution-1)
    - [Solution 2](#solution-2)
  - [1517. Find Users With Valid E-Mails \[`Easy`\]](#1517-find-users-with-valid-e-mails-easy)
  - [1527. Patients With a Condition \[`Easy`\]](#1527-patients-with-a-condition-easy)
  - [177. Nth Highest Salary \[`Medium`\]](#177-nth-highest-salary-medium)
  - [176. Second Highest Salary \[`Medium`\]](#176-second-highest-salary-medium)


# Data Filtering

| Problem name | Problem Classification | Solution link | Concept links |
|---|---|---|--|
| [595. Big Countries](https://leetcode.com/problems/big-countries/) | Easy | [595-big-countries--easy](./595-big-countries--easy.md) | [.loc](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html) is used to Access a group of rows and columns by label(s) or a boolean array. |
| [757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/) | Easy | [757-recyclable-and-low-fat-products](./757-recyclable-and-low-fat-products.md) |  |
| [183. Customers Who Never Order](https://leetcode.com/problems/customers-who-never-order/) | Easy | [183-customers-who-never-order](./183-customers-who-never-order.md) |  |
| [1148. Article Views I](https://leetcode.com/problems/article-views-i/) | Easy |  [1148-article-views-i](./1148-article-views-i.md) | [.drop_duplicates](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html): Return DataFrame with duplicate rows removed.   [.sort_values](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html) : Sort by the values along either axis. | 


# String Methods
## [1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/)  [`Easy`]

Table: Tweets

| Column Name    | Type    |
|----------------|---------|
| tweet_id       | int     |
| content        | varchar |
     
tweet_id is the primary key (column with unique values) for this table.
This table contains all the tweets in a social media app.
 

Write a solution to find the IDs of the invalid tweets. The tweet is invalid if the number of characters used in the content of the tweet is strictly greater than 15.

Return the result table in any order.

The result format is in the following example.

 

Example 1:

Input: 
Tweets table:
| tweet_id | content                          |
|----------|----------------------------------|
| 1        | Vote for Biden                   |
| 2        | Let us make America great again! |


Output: 
| tweet_id |
|----------|
| 2        |   

Explanation:    
Tweet 1 has length = 14. It is a valid tweet.    
Tweet 2 has length = 32. It is an invalid tweet.

Answer: 

[.str](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.html): Vectorized string functions for Series and Index.   
[User guide](https://pandas.pydata.org/docs/user_guide/text.html): Working with text data

```
import pandas as pd

def invalid_tweets(tweets: pd.DataFrame) -> pd.DataFrame:
    return tweets[
        tweets['content'].str.len() > 15]\
        [['tweet_id']]
```
[Back to Top](#table-of-content) :arrow_up:

## [1873. Calculate Special Bonus](https://leetcode.com/problems/calculate-special-bonus/) [`Easy`]

Table: Employees

| Column Name | Type    |
|-------------|---------|
| employee_id | int     |
| name        | varchar |
| salary      | int     |

employee_id is the primary key (column with unique values) for this table.
Each row of this table indicates the employee ID, employee name, and salary.
 

Write a solution to calculate the bonus of each employee. The bonus of an employee is 100% of their salary if the ID of the employee is an odd number and the employee's name does not start with the character 'M'. The bonus of an employee is 0 otherwise.

Return the result table ordered by employee_id.

The result format is in the following example.

 

Example 1:

Input: 
Employees table:

| employee_id | name    | salary |
|-------------|---------|--------|
| 2           | Meir    | 3000   |
| 3           | Michael | 3800   |
| 7           | Addilyn | 7400   |
| 8           | Juan    | 6100   |
| 9           | Kannon  | 7700   |

Output:   

| employee_id | bonus |
|-------------|-------|
| 2           | 0     |
| 3           | 0     |
| 7           | 7400  |
| 8           | 0     |
| 9           | 7700  |

Explanation: 
The employees with IDs 2 and 8 get 0 bonus because they have an even employee_id.
The employee with ID 3 gets 0 bonus because their name starts with 'M'.
The rest of the employees get a 100% bonus.

**Answer:**    
[.assign](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.assign.html) : Assign new columns to a DataFrame.

```
import pandas as pd

def calculate_special_bonus(employees: pd.DataFrame) -> pd.DataFrame:

    return employees\
        .assign(
            bonus= employees.apply(
                lambda x: x['salary'] 
                    if(
                        x['name'][0] != 'M' and 
                        x['employee_id'] % 2  != 0
                    ) else 0,
                axis=1
            )
        )\
        [['employee_id', 'bonus']]\
        .sort_values(by='employee_id')
```
[Back to Top](#table-of-content) :arrow_up:



## [1667. Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table/) [`Easy`]

Table: Users

| Column Name    | Type    |
|----------------|---------|
| user_id        | int     |
| name           | varchar |

user_id is the primary key (column with unique values) for this table.
This table contains the ID and the name of the user. The name consists of only lowercase and uppercase characters.
 

Write a solution to fix the names so that only the first character is uppercase and the rest are lowercase.

Return the result table ordered by user_id.

The result format is in the following example.

 
Example 1:

Input: 
Users table:

| user_id | name  |
|---------|-------|
| 1       | aLice |
| 2       | bOB   |

Output:  
| user_id | name  |
|---------|-------|
| 1       | Alice |
| 2       | Bob   |

### Solution 1
```
import pandas as pd

def fix_names(users: pd.DataFrame) -> pd.DataFrame:
    return users.assign(name= users['name'].str.title()).sort_values(by='user_id')
```
### Solution 2 
```
import pandas as pd

def fix_names(users: pd.DataFrame) -> pd.DataFrame:
    users['name'] = users['name'].str.title()
    return users.sort_values(by='user_id')
```

[Back to Top](#table-of-content) :arrow_up:



## [1517. Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails/) [`Easy`]

Table: Users

| Column Name   | Type    |
|---------------|---------|
| user_id       | int     |
| name          | varchar |
| mail          | varchar |

user_id is the primary key (column with unique values) for this table.
This table contains information of the users signed up in a website. Some e-mails are invalid.
 

Write a solution to find the users who have valid emails.

A valid e-mail has a prefix name and a domain where:

The prefix name is a string that may contain letters (upper or lower case), digits, underscore '_', period '.', and/or dash '-'. The prefix name must start with a letter.
The domain is '@leetcode.com'.
Return the result table in any order.

The result format is in the following example.

 

Example 1:

Input: 
Users table:
| user_id | name      | mail                    |
|---------|-----------|-------------------------|
| 1       | Winston   | winston@leetcode.com    |
| 2       | Jonathan  | jonathanisgreat         |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |
| 5       | Marwan    | quarz#2020@leetcode.com |
| 6       | David     | david69@gmail.com       |
| 7       | Shapiro   | .shapo@leetcode.com     |

Output: 

| user_id | name      | mail                    |
|---------|-----------|-------------------------|
| 1       | Winston   | winston@leetcode.com    |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |

Explanation: 
The mail of user 2 does not have a domain.
The mail of user 5 has the # sign which is not allowed.
The mail of user 6 does not have the leetcode domain.
The mail of user 7 starts with a period.

```
import re
import pandas as pd

def valid_emails(users: pd.DataFrame) -> pd.DataFrame:
    compiled_regex = re.compile(r'^[a-zA-Z][a-zA-Z0-9\.\-\_]*\@leetcode\.com$')
    return users[users['mail'].str.match(compiled_regex)]
```

[Back to Top](#table-of-content) :arrow_up:


## [1527. Patients With a Condition](https://leetcode.com/problems/patients-with-a-condition) [`Easy`]

Table: Patients

| Column Name  | Type    |
|--------------|---------|
| patient_id   | int     |
| patient_name | varchar |
| conditions   | varchar |
patient_id is the primary key (column with unique values) for this table.
'conditions' contains 0 or more code separated by spaces. 
This table contains information of the patients in the hospital.
 

Write a solution to find the patient_id, patient_name, and conditions of the patients who have Type I Diabetes. Type I Diabetes always starts with DIAB1 prefix.

Return the result table in any order.

The result format is in the following example.

 

Example 1:

Input: 
Patients table:
| patient_id | patient_name | conditions   |
|------------|--------------|--------------|
| 1          | Daniel       | YFEV COUGH   |
| 2          | Alice        |              |
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 |
| 5          | Alain        | DIAB201      |

Output: 

| patient_id | patient_name | conditions   |
|------------|--------------|--------------|
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 |
Explanation: Bob and George both have a condition that starts with DIAB1.


```
import pandas as pd
import re

def find_patients(patients: pd.DataFrame) -> pd.DataFrame:
    regex_compiled = re.compile(r'.*\bDIAB1.*')
    return patients[patients['conditions'].str.match(regex_compiled)]
```
[Back to Top](#table-of-content) :arrow_up:


## [177. Nth Highest Salary](https://leetcode.com/problems/nth-highest-salary) [`Medium`]

Table: Employee


| Column Name | Type |
|-------------|------|
| id          | int  |
| salary      | int  |

id is the primary key (column with unique values) for this table.
Each row of this table contains information about the salary of an employee.
 

Write a solution to find the nth highest salary from the Employee table. If there is no nth highest salary, return null.

The result format is in the following example.

 

Example 1:

Input: 
Employee table:
| id | salary |
|----|--------|
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |

n = 2
Output: 

| getNthHighestSalary(2) |
|------------------------|
| 200                    |

Example 2:

Input: 
Employee table:
| id | salary |
|----|--------|
| 1  | 100    |

n = 2

Output: 
| getNthHighestSalary(2) |
|------------------------|
| null                   |


```
import pandas as pd

def nth_highest_salary(employee: pd.DataFrame, N: int) -> pd.DataFrame:
    employee_salary_list = employee['salary'].drop_duplicates().to_list()

    if len(employee_salary_list) < N:
        n_highest_salary = None
    else:
        employee_salary_list.sort(reverse=True)
        n_highest_salary = employee_salary_list[(N-1)]
    
    return pd.DataFrame([{f'getNthHighestSalary({N})': n_highest_salary}])
```



## [176. Second Highest Salary](https://leetcode.com/problems/second-highest-salary/) [`Medium`]

Table: Employee

| Column Name | Type |
|-------------|------|
| id          | int  |
| salary      | int  |

id is the primary key (column with unique values) for this table.
Each row of this table contains information about the salary of an employee.
 

Write a solution to find the second highest distinct salary from the Employee table. If there is no second highest salary, return null (return None in Pandas).

The result format is in the following example.

 

Example 1:

Input: 
Employee table:

| id | salary |
|----|--------|
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |

Output: 

| SecondHighestSalary |
|---------------------|
| 200                 |

Example 2:

Input: 
Employee table:

| id | salary |
|----|--------|
| 1  | 100    |

Output: 
| SecondHighestSalary |
|---------------------|
| null                |

```
import pandas as pd
def second_highest_salary(employee: pd.DataFrame) -> pd.DataFrame:
    employee = employee['salary'].drop_duplicates()
    employee = employee.sort_values(ascending=False)
    if len(employee) < 2:
        return pd.DataFrame({'SecondHighestSalary' : [None]})
    else:
        return pd.DataFrame({'SecondHighestSalary' : [employee.iloc[1]]})
```
