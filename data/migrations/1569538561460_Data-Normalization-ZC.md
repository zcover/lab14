CREATE DATABASE lab14_normal WITH TEMPLATE lab14;
    -- This creates a new database with the same data as the lab14 database


CREATE TABLE BOOKSHELVES (id SERIAL PRIMARY KEY, name VARCHAR(255));
    --  This adds a new table to the new db called bookshelves


INSERT INTO bookshelves(name) SELECT DISTINCT bookshelf FROM books;
    --  This selects all the unique values from the bookshelf row in books


ALTER TABLE books ADD COLUMN bookshelf_id INT;
    -- This adds a column called bookshelf_id to the books table and gives it an integer value


UPDATE books SET bookshelf_id=shelf.id FROM (SELECT * FROM bookshelves) AS shelf WHERE books.bookshelf = shelf.name;
    -- This query will prepare a connection between the two tables. It works by running a subquery for every row in the books table. The subquery finds the bookshelf row that has a name matching the current book’s bookshelf value. The id of that bookshelf row is then set as the value of the bookshelf_id property in the current book row


ALTER TABLE books DROP COLUMN bookshelf;
    -- This will drop the column bookshelf from the books table


ALTER TABLE books ADD CONSTRAINT fk_bookshelves FOREIGN KEY (bookshelf_id) REFERENCES bookshelves(id);
    -- This adds the foreign key to books which will link it to bookshelves.
