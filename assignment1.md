### Assin 1 for psql
###### 1. list of consultants having more than one submission
~~~Sql
select * from consultant c where c.id in (
    select consultant_id from submission 
        group by consultant_id having count(consultant_id) > 1
);
~~~
###### 2. list all the interviews of consultants.
~~~Sql
select i.id interview_id, c.id consultant_id, s.id submission_id, c.name, i.round, i.result, i.remark 
from submission s inner join consultant c on c.id = s.consultant_id 
inner join interview i on s.id = i.sub_id;
~~~
###### 3. list all PO of marketers.
~~~Sql
select e.id marketer_id, e.name marketer_name, p.sub_id submission_id, p.id po_id, p.status, p.remark 
from employee e inner join submission s on e.id = s.emp_id 
inner join purchase_order p on s.id = p.sub_id;
~~~
###### 4. unique vendor company name for which client location is the same.
~~~Sql
select distinct v.id, v.name, v.city, s.city from vendor v 
inner join submission s on v.city = s.city;
~~~
###### 5. count of consultants which submitted in the same city.
~~~Sql
select s.city, count(s.city), c.city from submission s 
inner join consultant c on c.id = s.consultant_id group by s.city, c.city;
~~~
###### 6. name of consultant and client who have been submitted on the same vendor.
~~~Sql
select c.id, c.name Consulatant_Name, cl.id, cl.name Client, v.id vedor_id, v.name vendor 
from consultant c, client cl, submission s, vendor v 
where s.client_id = cl.id and s.consultant_id = c.id;
~~~