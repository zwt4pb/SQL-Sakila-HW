#1
SELECT actor.first_name, actor.last_name FROM actor
JOIN film_actor ON actor.actor_id = film_actor.actor_id
JOIN film ON film_actor.film_id = film.film_id
WHERE film.title = 'ACADEMY DINOSAUR';

#2
SELECT category.name AS category_name, 
COUNT(film_category.film_id) AS film_count FROM category
JOIN film_category ON category.category_id = film_category.category_id
GROUP BY category.name;

#3
SELECT film.rating, AVG(DATEDIFF(rental.return_date, rental.rental_date)) AS avg_rental_duration FROM film
JOIN inventory ON film.film_id = inventory.film_id
JOIN rental ON inventory.inventory_id = rental.inventory_id
GROUP BY film.rating;

#4
SELECT customer.first_name, customer.last_name, COUNT(rental.rental_id) AS rental_count FROM customer
JOIN rental ON customer.customer_id = rental.customer_id
GROUP BY customer.customer_id;

#5
SELECT store.store_id, COUNT(rental.rental_id) AS rental_count FROM store
JOIN staff ON store.store_id = staff.store_id
JOIN rental ON staff.staff_id = rental.staff_id
GROUP BY store.store_id
ORDER BY rental_count DESC;

#6
SELECT category.name AS category_name, COUNT(rental.rental_id) AS rental_count FROM category
JOIN film_category ON category.category_id = film_category.category_id
JOIN film ON film_category.film_id = film.film_id
JOIN inventory ON film.film_id = inventory.film_id
JOIN rental ON inventory.inventory_id = rental.inventory_id
GROUP BY category.name
ORDER BY rental_count DESC
LIMIT 1;

#7
SELECT c.name AS category_name, AVG(f.rental_rate) AS average_rental_rate FROM category c
JOIN film_category fc ON c.category_id = fc.category_id
JOIN film f ON fc.film_id = f.film_id
GROUP BY c.name;

#8
SELECT film.title, MAX(rental.return_date) AS last_rental_date FROM film
LEFT JOIN inventory ON film.film_id = inventory.film_id
LEFT JOIN rental ON inventory.inventory_id = rental.inventory_id
GROUP BY film.film_id, film.title;

#9
SELECT customer.first_name, customer.last_name, SUM(payment.amount) AS total_spending FROM customer
JOIN rental ON customer.customer_id = rental.customer_id
JOIN payment ON rental.rental_id = payment.rental_id
GROUP BY customer.customer_id;

#10
SELECT language.name AS language, AVG(film.length) AS average_length FROM language
JOIN film ON language.language_id = film.language_id
GROUP BY language.name;
