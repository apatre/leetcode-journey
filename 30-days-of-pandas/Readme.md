>This ultimate Revision page for Pandas with Leetcode questions

Table of Content
--
- [Data Filtering](#data-filtering)
  - [595. Big Countries  \[`Easy`\]](#595-big-countries--easy)
  - [757. Recyclable and Low Fat Products  \[`Easy`\]](#757-recyclable-and-low-fat-products--easy)
  - [183. Customers Who Never Order  \[`Easy`\]](#183-customers-who-never-order--easy)
  - [1148. Article Views I  \[`Easy`\]](#1148-article-views-i--easy)
- [String Methods](#string-methods)
  - [1683. Invalid Tweets  \[`Easy`\]](#1683-invalid-tweets--easy)
  - [1873. Calculate Special Bonus \[`Easy`\]](#1873-calculate-special-bonus-easy)


# Data Filtering
## [595. Big Countries](https://leetcode.com/problems/big-countries/)  [`Easy`]

Table: World

| Column Name | Type    |
|---|---|
| name        | varchar |
| continent   | varchar |
| area        | int     |
| population  | int     |
| gdp         | bigint  |

name is the primary key (column with unique values) for this table.
Each row of this table gives information about the name of a country, the continent to which it belongs, its area, the population, and its GDP value.
 

A country is big if:

it has an area of at least three million (i.e., 3000000 km2), or
it has a population of at least twenty-five million (i.e., 25000000).
Write a solution to find the name, population, and area of the big countries.

Return the result table in any order.

The result format is in the following example.

 

Example 1:

Input: 
World table:
| name        | continent | area    | population | gdp          |
|-------------|-----------|---------|------------|--------------|
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |

Output:   
| name        | population | area    |
|-------------|------------|---------|
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |

**Answer # 1: Using .loc**   
[.loc](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html) is used to Access a group of rows and columns by label(s) or a boolean array.


```
import pandas as pd

def big_countries(world: pd.DataFrame) -> pd.DataFrame:
    return world.loc[
        ((world['area'] >= 3000000)
        | (world['population'] >= 25000000)), ['name', 'population', 'area']]
```
**Answer #2: Using Slicing**

```
import pandas as pd

def big_countries(world: pd.DataFrame) -> pd.DataFrame:
    big_countries_df = world[
        ((world['area'] >= 3000000)
        | (world['population'] >= 25000000))]

    return big_countries_df[['name', 'population', 'area']]
```
[Back to Top](#table-of-content) :arrow_up:

## [757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/)  [`Easy`]

Table: Products

| Column Name | Type    |
|-------------|---------|
| product_id  | int     |
| low_fats    | enum    |
| recyclable  | enum    |

product_id is the primary key (column with unique values) for this table.
low_fats is an ENUM (category) of type ('Y', 'N') where 'Y' means this product is low fat and 'N' means it is not.
recyclable is an ENUM (category) of types ('Y', 'N') where 'Y' means this product is recyclable and 'N' means it is not.
 

**Write a solution to find the ids of products that are both low fat and recyclable.**
**Return the result table in any order.**

The result format is in the following example.

 

Example 1:

Input: 
Products table:
| product_id  | low_fats | recyclable |
|-------------|----------|------------|
| 0           | Y        | N          |
| 1           | Y        | Y          |
| 2           | N        | Y          |
| 3           | Y        | Y          |
| 4           | N        | N          |

Output:   
| product_id  |
|-------------|
| 1           |
| 3           |

Explanation: Only products 1 and 3 are both low fat and recyclable.

Answer: 

```
import pandas as pd

def find_products(products: pd.DataFrame) -> pd.DataFrame:
    return pd.DataFrame(products.loc[
        (
            (products['low_fats'] == 'Y')
            & (products['recyclable'] == 'Y')
        ), 'product_id'])
```
[Back to Top](#table-of-content) :arrow_up:

## [183. Customers Who Never Order](https://leetcode.com/problems/customers-who-never-order/)  [`Easy`]

Table: Customers

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |

id is the primary key (column with unique values) for this table.
Each row of this table indicates the ID and name of a customer.
 

Table: Orders

| Column Name | Type |
|-------------|------|
| id          | int  |
| customerId  | int  |

id is the primary key (column with unique values) for this table.
customerId is a foreign key (reference columns) of the ID from the Customers table.
Each row of this table indicates the ID of an order and the ID of the customer who ordered it.
 

**Write a solution to find all customers who never order anything.**   
**Return the result table in any order.**   
**The result format is in the following example.**


Example 1:

Input: 
Customers table:

| id | name  |
|----|-------|
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |

Orders table:
| id | customerId |
|----|------------|
| 1  | 3          |
| 2  | 1          |

Output:   

| Customers |
|-----------|
| Henry     |
| Max       |


**Answer:**   
[.isin](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.isin.html) : It is used to check Whether each element in the DataFrame is contained in values.   
[.rename](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.rename.html) : Rename columns or index labels.

```import pandas as pd

def find_customers(customers: pd.DataFrame, orders: pd.DataFrame) -> pd.DataFrame:
    return customers[~customers.id.isin(orders.customerId)][['name']].rename(columns={'name': 'Customers'})
```
[Back to Top](#table-of-content) :arrow_up:

## [1148. Article Views I](https://leetcode.com/problems/article-views-i/?envType=study-plan-v2&envId=30-days-of-pandas&lang=pythondata#:~:text=1148.%20Article%20Views%20I)  [`Easy`]

Table: Views

| Column Name   | Type    |
|---------------|---------|
| article_id    | int     |
| author_id     | int     |
| viewer_id     | int     |
| view_date     | date    |

There is no primary key (column with unique values) for this table, the table may have duplicate rows.
Each row of this table indicates that some viewer viewed an article (written by some author) on some date. 
Note that equal author_id and viewer_id indicate the same person.
 

Write a solution to find all the authors that viewed at least one of their own articles.

Return the result table sorted by id in ascending order.

The result format is in the following example.

 

Example 1:

Input: 
Views table:
| article_id | author_id | viewer_id | view_date  |
|------------|-----------|-----------|------------|
| 1          | 3         | 5         | 2019-08-01 |
| 1          | 3         | 6         | 2019-08-02 |
| 2          | 7         | 7         | 2019-08-01 |
| 2          | 7         | 6         | 2019-08-02 |
| 4          | 7         | 1         | 2019-07-22 |
| 3          | 4         | 4         | 2019-07-21 |
| 3          | 4         | 4         | 2019-07-21 |

Output:  

| id   |
|------|
| 4    |
| 7    |

**Answer**:   
[.drop_duplicates](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html): Return DataFrame with duplicate rows removed.  
[.sort_values](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html) : Sort by the values along either axis.

```
import pandas as pd

def article_views(views: pd.DataFrame) -> pd.DataFrame:

    return views\
        .loc[(views.author_id == views.viewer_id), ['author_id']]\
        .drop_duplicates()\
        .sort_values('author_id')\
        .rename(
            columns={
                'author_id': 'id'
            }
        )
```
[Back to Top](#table-of-content) :arrow_up:

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