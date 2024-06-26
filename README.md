
# SQL- Here are some SQL exercises

Exercise: --Goal: Figure out what percent of users have ever viewed the user profile page.  

SELECT 
(case when first_view is null then FALSE 
  ELSE true END) as has_viewed_profile_page
COUNT(user_id) as users
FROM 
  (SELECT 
  user.id as user_id,
  min(event_time) as users
  FROM 
  dsv1069.users
  left outer JOIN
  dsv1069.events 
  ON 
  events.user_id = user.id 
  AND
  events.event_name = 'view_user_profile'
  group by
  users.id 
  ) first_profile_view 
  group by 
  (case when first_view is null then FALSE
    ELSE then END)

Exercise: Find the number of companies that one investor has funded any amount in usa and then find the biggest sector. Then show the number of investments each sector has.
select investor_name, 
count(*) as num_of_investments 
from tutorial.crunchbase_investments 
where company_country_code = 'USA'
group by  investor_name
order by num_of_investments DESC 
;

select company_category_code, 
count(company_category_code) as num_of_dept_investments
from tutorial.crunchbase_investments 
where company_country_code = 'USA'
group by company_category_code
order by num_of_dept_investments DESC 
;

Exercise: --Goal: For each user figure out IF a user has ordered something, and when their first purchase 
was. The query below doesn’t return info for any of the users who haven’t ordered anything.  

SELECT
  users.id as user_id,
  min(orders.paid_at) as min_paid_at
FROM
  dsv1069.users
  LEFT JOIN dsv1069.orders ON orders.user_id = users.id
GROUP BY
  users.id

Exercise: --Goal: Compute the number of items in the items table which have been ordered. The query 
below runs, but it isn’t right. Determine the correct query. 
fixed code

SELECT 
  COUNT(item_id)
from dsv1069.orders
inner join dsv1069.items
on orders.item_id = items.id;

Exercise: --Goal: Check out the query below. This is not the right way to count the number of viewed_item 
events. Determine what is wrong and correct the error.  

SELECT
COUNT(event_name)
FROM dsv1069.events
WHERE event_name = 'view_item';

Exercise: --Goal: Select all of the columns from the result when you JOIN the users​ table to the orders 
select  * 
from 
 dsv1069.users a join  dsv1069.orders b 
 on a.id = b.user_id ;

Exercise 2: --Goal: Use the items​ table to count the number of items for sale in each category 

select category, count(*) as items_sold from dsv1069.items group by category;


Exercise: 
Goal: Here we use users ​ table to pull a list of user email addresses. Edit the query to pull email addresses, but only for non-deleted users. 

select email_address FROM dsv1069.users
where deleted_at is null;


















