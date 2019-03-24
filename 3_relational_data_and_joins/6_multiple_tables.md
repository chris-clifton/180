1. Import db: https://raw.githubusercontent.com/launchschool/sql_course_data/master/sql-and-relational-databases/relational-data-and-joins/working-with-multiple-tables/theater_full.sql

2. Write a query that determines how many tickets have been sold
  `SELECT count(*) FROM tickets;`

3. Write a query that determines how many different customers purchased tickets to at least one event
  `SELECT COUNT(DISTINCT customer_id) FROM tickets;`

4. Write a query that determines what percentage of customers in the database have purchased a ticket to one or more of the events
  - select COUNT(DISTINCT customer_id) FROM tickets THEN SOMEHOW DIVIDE BY CUSTOMERS::float
  - Division between integers in PostgreSQL always returns integer results but by casting one of the values in division into a floating point number, fractional values will then be returned
    - Ex: `SELECT 1 / 2` returns 0 but `SELECT 1 / 2::float;` returns 0.5
    - `SELECT COUNT(DISTINCT tickets.customer_id) / COUNT(DISTINCT) customers.id)::float * 100 AS percent FROM customers LEFT OUTER JOIN tickets ON tickets.customer_id = customers.id`

5. Write a query that returns the name of each event and how many tickets were sold for it, in order form most populat to least popular
  `SELECT e.name, COUNT(t.id) AS popularity FROM events AS e LEFT OUTER JOIN tickets AS t ON t.event_id = e.id GROUP BY e.id ORDER BY popularity DESC;`

6. Write a query that returns the user id, email address, and number of events for all customers that have purchased tickets to three events
  `SELECT customers.id, customers.email COUNT(DISTINCT tickets.event_id) FROM customers INNER JOIN tickets on tickets.customer_id = customers.id GROUP BY customers.id HAVING COUNT(DISTINCT tickets.event_id) = 3;

7. Write a query to print out a report of all tickets purchased by the customer with the email address 'gennaro.rath@mcdermott.co'
  ` SELECT events.name AS event, events.starts_at, sections.name AS section, seats.row, seats.number AS seat
    FROM tickets
      INNER JOIN events ON tickets.event_id = events.id
      INNER JOIN customers ON tickets.customer_id = customers.id
      INNER JOIN seats ON tickets.seat_id = seats.id
      INNER JOIN sections ON seats.section_id = sections.id
    WHERE customers.email = 'gennaro.rath@mcdermott.co';

    