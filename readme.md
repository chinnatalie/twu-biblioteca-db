# Biblioteca SQL Assignment

1.	Anand Beck

```sql
SELECT * 
FROM   member 
WHERE  id = 
       ( 
              SELECT member_id 
              FROM   checkout_item 
              WHERE  book_id = 
                     ( 
                            SELECT id 
                            FROM   book 
                            WHERE  title = “the Hobbit”));
```

2.	37

```sql
SELECT Count(*) 
FROM   member 
WHERE  id NOT IN (SELECT member_id 
                  FROM   checkout_item); 
```

3.	1984, Catcher in the Rye, Crouching Tiger, Hidden Dragon, Domain Driven Design, Fellowship of the Ring, Lawrence of Arabia, Office Space,Thin Red Line, To Kill a Mockingbird, Tom Sawyer

```sql
SELECT title 
FROM   book 
WHERE  id NOT IN (SELECT book_id 
                  FROM   checkout_item 
                  WHERE  book_id IS NOT NULL) 
UNION 
SELECT title 
FROM   movie 
WHERE  id NOT IN (SELECT movie_id 
                  FROM   checkout_item 
                  WHERE  movie_id IS NOT NULL);
```

4.	*(see script below)*

```sql
INSERT INTO book 
            ( 
                        id, 
                        title 
            ) 
            VALUES 
            ( 
                        11, 
                        “the pragmatic programmer” 
            );INSERT INTO member 
            ( 
                        id, 
                        NAME 
            ) 
            VALUES 
            ( 
                        43, 
                        “natalie chin” 
            );INSERT INTO checkout_item 
            ( 
                        member_id, 
                        book_id 
            ) 
            VALUES 
            ( 
                        43, 
                        11 
            );
```

5.	Anand Beck & Frank Smith

```sql
SELECT NAME 
FROM   member 
WHERE  id IN (SELECT member_id 
              FROM   (SELECT member_id, 
                             Count(*) AS c 
                      FROM   checkout_item 
                      GROUP  BY member_id) 
              WHERE  c > 1); 
```
