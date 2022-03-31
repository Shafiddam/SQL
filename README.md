### Примеры запросов SQL (таблицы разные!):
_____________________________________________________
**CREATE** table author (author_id INT PRIMARY KEY AUTO_INCREMENT, name_author VARCHAR(50))  
**INSERT** into author (name_author) VALUES ('Булгаков М.А.'), ('Достоевский Ф.М.'), ('Есенин С.А.'), ('Пастернак Б.Л.')  
**SELECT** title, amount, amount * 1.65 AS pack FROM book  
**SELECT** title, author, amount, ROUND(price * 0.7,2) AS new_price FROM book  
**SELECT** author, title, ROUND(IF(author='Булгаков М.А.', price * 1.1, IF(author='Есенин С.А.', price * 1.05, price)),2) AS new_price FROM book  
**SELECT** title, author, price, amount FROM book WHERE (price<500 OR price>600) AND price * amount >= 5000  
**SELECT** title, author FROM book WHERE (price BETWEEN 540.50 AND 800) AND amount IN (2,3,5,7)  
**SELECT** author, title FROM book WHERE amount BETWEEN 2 AND 14 ORDER BY author DESC, title  



