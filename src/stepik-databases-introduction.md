# 1  
  
База данных платежной системы `billing_simple` состоит из одной таблицы `billing` следующей структуры:  
  
	CREATE TABLE IF NOT EXISTS `billing_simple`.`billing` (
	`payer_email` VARCHAR(255) NULL,
	`recipient_email` VARCHAR(255) NULL,
	`sum` DECIMAL(18,2) NULL,
	`currency` VARCHAR(3) NULL,
	`billing_date` DATE NULL,
	`comment` TEXT NULL)
	ENGINE = InnoDB;
  
Добавьте в таблицу одну запись о платеже со следующими значениями:  
email плательщика: 'pasha@mail.com'  
email получателя: 'katya@mail.com'  
сумма: 300.00  
валюта: 'EUR'  
дата операции: 14.02.2016  
комментарий: 'Valentines day present)'  
  
	INSERT INTO billing VALUES ('pasha@mail.com', 'katya@mail.com', 300.00, 'EUR', '2016-02-14', 'Valentines day present)');
  
  
  
# 2  
  
Измените адрес плательщика на 'igor@mail.com' для всех записей таблицы, где адрес плательщика 'alex@mail.com'.  
  
	UPDATE billing SET payer_email = 'igor@mail.com' WHERE payer_email = 'alex@mail.com';
  
  
  
# 3  
  
Удалите из таблицы записи, где адрес плательщика или адрес получателя установлен в неопределенное значение или пустую строку.  
  
	DELETE FROM billing WHERE payer_email IS NULL OR payer_email = "" OR recipient_email IS NULL OR recipient_email = "";
  
  
  
# 4  
  
База данных учета проектов `project_simple` состоит из одной таблицы `project` следующей структуры:  
  
	CREATE TABLE IF NOT EXISTS `project_simple`.`project` (
	`project_name` VARCHAR(255) NULL,
	`client_name` VARCHAR(255) NULL,
	`project_start` DATE NULL,
	`project_finish` DATE NULL,
	`budget` DECIMAL(18,2) NULL)
	ENGINE = InnoDB;
  
Выведите общее количество заказов компании.  
  
	SELECT COUNT(*) FROM project;
  
  
  
# 5  
  
Выведите в качестве результата одного запроса общее количество заказов, сумму стоимостей (бюджетов) всех проектов, средний срок исполнения заказа в днях.  
  
	SELECT COUNT(project_name), SUM(budget), AVG(DATEDIFF(project_finish, project_start)) FROM project;
  
  
  
# 6  
  
База данных магазина `store_simple` состоит из одной таблицы `store` следующей структуры:  
  
	CREATE TABLE IF NOT EXISTS `store_simple`.`store` (
	`product_name` VARCHAR(255) NULL,
	`category` VARCHAR(255) NULL,
	`price` DECIMAL(18,2) NULL,
	`sold_num` INT NULL)
	ENGINE = InnoDB;
  
Выведите количество товаров в каждой категории. Результат должен содержать два столбца: 
+ название категории   
+ количество товаров в данной категории.  
  
	SELECT category, COUNT(product_name) FROM store GROUP BY category;
  
  
  
# 7  
  
Выведите 5 категорий товаров, продажи которых принесли наибольшую выручку. Под выручкой понимается сумма произведений стоимости товара на количество проданных единиц. Результат должен содержать два столбца:   
+ название категории  
+ выручка от продажи товаров в данной категории.  
  
	SELECT category, SUM(price*sold_num) result FROM store GROUP BY category ORDER BY result DESC LIMIT 5;
  
  
  
# 8  
  
База данных магазина `store` следующей структуры:  
  
![img](https://ucarecdn.com/c3cd7834-60ed-4dc6-b86e-ce4555aba914/)  
  
Выведите все позиций списка товаров принадлежащие какой-либо категории с названиями товаров и названиями категорий. Список должен быть отсортирован по названию товара, названию категории. Для соединения таблиц необходимо использовать оператор INNER JOIN.  
  
	SELECT good.name, category.name FROM category_has_good
		INNER JOIN good ON category_has_good.good_id = good.id
		NNER JOIN category ON category_has_good.category_id = category.id
	ORDER BY good.name, category.name;
  
  
  
# 9  
  
Выведите список клиентов (имя, фамилия) и количество заказов данных клиентов, имеющих статус "new".  
  
	SELECT client.first_name, client.last_name, COUNT(*) AS new_sale_num FROM client
		INNER JOIN sale ON client.id = sale.client_id
		INNER JOIN status ON sale.status_id = status.id WHERE status.name = 'new'
	GROUP BY client.first_name, client.last_name;
  
  
  
# 10  
  
Выведите список товаров с названиями товаров и названиями категорий, в том числе товаров, не принадлежащих ни одной из категорий.  
  
	SELECT good.name, category.name FROM category_has_good
		LEFT OUTER JOIN category ON category_has_good.category_id = category.id
		RIGHT OUTER JOIN good ON category_has_good.good_id = good.id;
  
  
  
# 11  
  
Выведите список товаров с названиями категорий, в том числе товаров, не принадлежащих ни к одной из категорий, в том числе категорий не содержащих ни одного товара.  
  
	SELECT good.name, category.name FROM category_has_good
		LEFT OUTER JOIN category ON category_has_good.category_id = category.id
		RIGHT OUTER JOIN good ON category_has_good.good_id = good.id
	UNION
	SELECT good.name, category.name FROM category_has_good
		RIGHT OUTER JOIN category ON category_has_good.category_id = category.id
		LEFT OUTER JOIN good ON category_has_good.good_id = good.id;
  
  
  
# 12  
  
Выведите список всех источников клиентов и суммарный объем заказов по каждому источнику. Результат должен включать также записи для источников, по которым не было заказов.  
  
	SELECT source.name, sum(sale.sale_sum) FROM source
		LEFT OUTER JOIN client ON source.id = client.source_id
		LEFT OUTER JOIN sale ON client.id = sale.client_id
	GROUP BY source.name;
  
  
  
# 13  
  
Выведите названия товаров, которые относятся к категории 'Cakes' или фигурируют в заказах текущий статус которых 'delivering'. Результат не должен содержать одинаковых записей. В запросе необходимо использовать оператор UNION для объединения выборок по разным условиям.  
  
	SELECT good.name FROM good
		LEFT JOIN category_has_good ON good.id = category_has_good.good_id
		LEFT JOIN category ON category_has_good.category_id = category.id WHERE category.name = 'Cakes'
	UNION
	SELECT good.name FROM good
		LEFT JOIN sale_has_good ON sale_has_good.good_id = good.id
		LEFT JOIN sale ON sale_has_good.sale_id = sale.id
		LEFT JOIN status ON status.id = sale.status_id WHERE status.name = 'delivering';
  
  
  
# 14  
  
Выведите список всех категорий продуктов и количество продаж товаров, относящихся к данной категории. Под количеством продаж товаров подразумевается суммарное количество единиц товара данной категории, фигурирующих в заказах с любым статусом.   
  
	SELECT category.name, count(sale.id) FROM category
		LEFT OUTER JOIN category_has_good ON category.id = category_has_good.category_id
		LEFT OUTER JOIN good ON good.id = category_has_good.good_id
		LEFT OUTER JOIN sale_has_good ON good.id = sale_has_good.good_id
		LEFT OUTER JOIN sale ON sale.id = sale_has_good.sale_id
		GROUP BY category.name;
  
  
  
# 15  
  
Выведите список источников, из которых не было клиентов, либо клиенты пришедшие из которых не совершали заказов или отказывались от заказов. Под клиентами, которые отказывались от заказов, необходимо понимать клиентов, у которых есть заказы, которые на момент выполнения запроса находятся в состоянии 'rejected'. В запросе необходимо использовать оператор UNION для объединения выборок по разным условиям.  
  
	SELECT source.name FROM source WHERE NOT EXISTS (SELECT * FROM client WHERE client.source_id = source.id)
	UNION
	SELECT source.name FROM source
		INNER JOIN client ON client.source_id = source.id
		INNER JOIN sale ON sale.client_id = client.id
		INNER JOIN status ON status.id = sale.status_id WHERE status.name = 'rejected';