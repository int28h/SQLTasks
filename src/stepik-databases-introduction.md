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
  
  
  
