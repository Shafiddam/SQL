### Примеры запросов SQL (таблицы разные!):
_____________________________________________________
**CREATE** TABLE author (author_id INT PRIMARY KEY AUTO_INCREMENT, name_author VARCHAR(50))  
**INSERT** INTO author (name_author) VALUES ('Булгаков М.А.'), ('Достоевский Ф.М.'), ('Есенин С.А.'), ('Пастернак Б.Л.')  
**INSERT** INTO supply (title, author, price, amount) VALUES ('Лирика', 'Пастернак Б.Л.', 518.99, 2), ('Черный человек', 'Есенин С.А.', 570.20, 6) 
**INSERT** INTO book (title, author, price, amount) SELECT title, author, price, amount FROM supply where author != 'Булгаков М.А.' AND author != 'Достоевский Ф.М.'  
**UPDATE** book SET price = 0.9 * price WHERE amount IN (5,10) 
**UPDATE** book SET price = IF(buy != 0, price, price * 0.9), buy = if (buy > amount, amount, buy)  
**UPDATE** book, supply SET book.amount = book.amount + supply.amount, book.price = (book.price + supply.price)/2 WHERE book.title = supply.title AND book.author = supply.author  
**DELETE** FROM supply WHERE author IN(SELECT author FROM book GROUP BY author HAVING SUM(amount) > 10)  
**CREATE** TABLE ordering AS SELECT author, title, (SELECT ROUND(AVG(amount)) FROM book) AS amount FROM book WHERE amount < 4  
**SELECT** title, amount, amount * 1.65 AS pack FROM book  
**SELECT** title, author, amount, ROUND(price * 0.7,2) AS new_price FROM book  
**SELECT** author, title, ROUND(IF(author='Булгаков М.А.', price * 1.1, IF(author='Есенин С.А.', price * 1.05, price)),2) AS new_price FROM book  
**SELECT** title, author, price, amount FROM book WHERE (price<500 OR price>600) AND price * amount >= 5000  
**SELECT** title, author FROM book WHERE (price BETWEEN 540.50 AND 800) AND amount IN (2,3,5,7)  
**SELECT** author, title FROM book WHERE amount BETWEEN 2 AND 14 ORDER BY author DESC, title  
**SELECT** title, author FROM book WHERE title LIKE '% %' AND title NOT LIKE ' ' AND author LIKE '%С.%' ORDER BY title  
**SELECT** "Донцова Дарья" AS author, CONCAT("Евлампия Романова и ", title) AS title, ROUND((price * 1.42),2) AS price FROM book ORDER BY 3 DESC, 2 DESC  
**SELECT** author AS 'Автор', COUNT(title) ASs 'Различных_книг', SUM(amount) AS 'Количество_экземпляров' FROM book GROUP BY author  
**SELECT** DISTINCT amount FROM book  
**SELECT** author, MIN(price) AS 'Минимальная_цена', MAX(price) AS 'Максимальная_цена', AVG(price) AS 'Средняя_цена' FROM book GROUP BY author  
**SELECT** author, round(sum(price * amount),2) as 'Стоимость', round(sum(price * amount) * 0.18/ 1.18, 2) AS 'НДС', round(sum(price * amount)/ 1.18, 2) AS 'Стоимость_без_НДС' FROM book GROUP BY author  
**SELECT** author, sum(price * amount) as 'Стоимость' from book where title <> 'Идиот' and title <> 'Белая гвардия' group by author having Стоимость > 5000 order by Стоимость desc  
**SELECT** title, author, amount, price FROM book WHERE author IN (SELECT author FROM book GROUP BY author HAVING SUM(amount) >= 12)  
<br>
-- Вывести два города, в которых чаще всего были в командировках сотрудники. Вычисляемый столбец назвать Количество:  
**SELECT** city, count(city) AS Количество FROM trip GROUP BY city ORDER BY Количество DESC LIMIT 2  






