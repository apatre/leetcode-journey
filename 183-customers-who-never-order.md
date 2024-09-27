# [183. Customers Who Never Order](https://leetcode.com/problems/customers-who-never-order/)  [`Easy`]
> appeared in [30 Days Of Pandas](./0-Study-plan-30-days-of-pandas.md)

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
