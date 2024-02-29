# SQL CRUD

An assignment to design relational database tables with particular applications in mind.

The contents of this file will be deleted and replaced with the content described in the [instructions](./instructions.md)

### 1. the SQL code to create each of the required tables

Create the table for the imported restaurants.csv

```sql
CREATE TABLE restaurants (
   id INTEGER PRIMARY KEY,
   Category TEXT,
   Price Tier TEXT,
   Neighborhood TEXT,Opening Time REAL,
   Closing Time REAL,
   Average Rating INTEGER,
   Good for kid Boolean
   );

```

Import the csv file created from mockaroo

```sql
.import /Users/brandongao/restaurant/data/restaurants.csv

```

Create the Review Table and INSERT the review:

```sql
CREATE TABLE reviews (
    id INTEGER PRIMARY KEY,
    restaurant_id INTEGER,
    review_text TEXT,
    rating INTEGER,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (restaurant_id) REFERENCES restaurant(id)
);
INSERT INTO reviews VALUES(1,1,'Great ambiance and friendly staff',5,'2024-02-29 18:25:14');

```

## Links to data

Restaurant data:
[Link Text](data/restaurants.csv)

## Sqlite code for each task

1. Find all cheap restaurants in a particular neighborhood (pick any neighborhood as an example).

```sql
SELECT * FROM restaurants
   ...> WHERE Neighborhood = 'Upper East Side' AND "Price Tier" = 'Low';
```

2. Find all restaurants in a particular genre (pick any genre as an example) with 3 stars or more, ordered by the number of stars in descending order.

```sql
SELECT * FROM restaurants
   ...> WHERE Category = 'Korean' AND "Average Rating" >= 3 ORDER BY "Average Rating" DESC;
```

3. Find all restaurants that are open now (see hint below).

```sql
SELECT * FROM restaurants
   ...> WHERE strftime('%H:%M','now','localtime') BETWEEN "Opening Time" AND "Closing Time";
```

4. Leave a review for a restaurant (pick any restaurant as an example; note that leaving a review has no automatic effect on the average rating of the restaurant).

```sql
INSERT INTO reviews VALUES(1,1,'Great ambiance and friendly staff',5,'2024-02-29 18:25:14');
```

5. Delete all restaurants that are not good for kids.

```sql
DELETE FROM restaurants WHERE "Good for kid" = 'false';
```

6. Find the number of restaurants in each NYC neighborhood.

```sql
SELECT Neighborhood, COUNT(*) AS numberofrestaurants FROM restaurants GROUP BY Neighborhood;
```
