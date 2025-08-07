https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data

Lab objective: `To display one or more unreleased products.`
# Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

From the lab we know that this lab contains a SQL injection vulnerability in the product category filter. So we will use the section.

It is home section

![[Lab 1.png]]

After clicking the Accessories category we will use burpsuit

![[Lab 1-1.png]]

Now send the request to the repeater tab and check category is vulnerable or not.

`category=Accessories' and 1=1--`
is ok
![[Lab 1-2.png]]

`category=Accessories' and 1=2--`
is not ok

![[Lab 1-3.png]]

From the question section we know that the query is: `SELECT * FROM products WHERE category = 'Gifts' AND released = 1`

On the query we know that category = category name and if released =1 then the product will show from the category but if released = 0 then the product will not show.
So we will make the category section true and released section comment out.

We know that, anything OR true = true.

![[Lab 1-4.png]]

Then we will see in browser we solve the lab.

![[Lab 1-5.png]]

#sql #sqli 