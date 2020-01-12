### Assin 1 for psql


###### 1. list of consultants having more than one submission
~~~Sql
select * from consultant c where c.id in (
    select consultant_id from submission 
        group by consultant_id having count(consultant_id) > 1
)
~~~

###### 2. list all the interviews of consultants.
~~~Sql
select * from interview order by sub_id, round asc;
~~~

###### 3. list all PO of marketers.

~~~Sql
select * from employee e inner join submission s on e.id = s.emp_id 
    inner join purchase_order p on s.id = p.sub_id; 
~~~

###### 4. unique vendor company name for which client location is the same.

~~~Sql
select distinct id, city, name from vendor v 
    inner join submission s on v.city = s.city;
~~~

###### 5. count of consultants which submitted in the same city.

~~~Sql
select * from consultant c inner join submission s on c.city = s.city;
~~~

###### 6. name of consultant and client who have been submitted on the same vendor.
~~~Sql
Select c.name from client c where c.id in (
	select distinct s.client_id from submission s
)
UNION
Select ct.name from consultant ct where ct.id in (
	select distinct s.consultant_id from submission s
)
~~~