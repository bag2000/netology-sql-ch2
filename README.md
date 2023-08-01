## SQL. Часть 2 - Поляков Р.В.
### Задание 1  
#### Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:
- фамилия и имя сотрудника из этого магазина;  
- город нахождения магазина;  
- количество пользователей, закреплённых в этом магазине.  
```
select concat(stf.first_name, ' ', stf.last_name) as fio, ct.city, count(c.customer_id) as cnt
from customer c
join store stor on stor.store_id = c.store_id
join staff stf on stf.staff_id = stor.manager_staff_id 
join address addr on addr.address_id = stf.address_id 
join city ct on ct.city_id = addr.city_id
group by stf.staff_id 
having cnt > 300;
```
### Задание 2  
#### Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.
```
select count(`length`) 
from film
where `length` > (select sum(f.length) / count(f.film_id) from film f); 
```
### Задание 3  
#### Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.
```
select count(p.rental_id) as cnt_rental, sum(p.amount) as sum_amount, month(p.payment_date) as pay_month
from payment p
group by pay_month
order by sum_amount desc 
limit 1;
```
