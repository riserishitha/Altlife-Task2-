# 📚 Altlife Task 2 - Library Management System  

## 📖 Overview  
This project involves SQL queries to manage a library system, including retrieving books that were never borrowed, listing outstanding books, and identifying the most borrowed books.  

## 📌 SQL Queries  

### 1️⃣ Get all books that have never been borrowed  
This query retrieves books that have never been issued to any member.  

```sql
SELECT 
    b.book_name, 
    b.book_publisher AS author
FROM Book b
LEFT JOIN Issuance i ON b.book_id = i.book_id
WHERE i.book_id IS NULL;

### 2️⃣ List the outstanding books at any given point in time

```sql
SELECT 
    m.mem_name AS "Member Name",
    b.book_name AS "Book Name",
    i.issuance_date AS "Issued Date",
    i.target_return_date AS "Target Return Date",
    b.book_publisher AS "Author"
FROM Issuance i
JOIN Book b ON i.book_id = b.book_id
JOIN Member m ON i.issuance_member = m.mem_id
WHERE i.issuance_status = 'Borrowed';

### 3️⃣ Get the top 10 most borrowed books

```sql
SELECT 
    b.book_name AS "Book Name",
    COUNT(i.issuance_id) AS "# of times borrowed",
    COUNT(DISTINCT i.issuance_member) AS "# of Members that borrowed"
FROM Issuance i
JOIN Book b ON i.book_id = b.book_id
GROUP BY b.book_id, b.book_name
ORDER BY COUNT(i.issuance_id) DESC
LIMIT 10;


