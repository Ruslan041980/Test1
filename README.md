--Найти все товары производителей из Москвы. Вывести имена товаров, их цены и имена производителей

SELECT g.name, p.value, m.name, m.location FROM goods g
  Join quantity q ON q.goods_id = g.id
  Join prices p ON p.goods_id = g.id
  Join suppliers s ON s.id = g.supplier_id
  Join manufacturer m ON m.id = s.manufacturer_id
WHERE m.location = 'Moscow'
----------------------------------------------------------
--Найти самый дорогой товар. Вывести имя товара и его цену

SELECT g.name, MAX(p.value) FROM goods g
  Join quantity q ON q.goods_id = g.id
  Join prices p ON p.goods_id = g.id
  Join suppliers s ON s.id = g.supplier_id
  Join manufacturer m ON m.id = s.manufacturer_id
GROUP BY g.name
ORDER BY AVG(p.value)
DESC
LIMIT 1
------------------------------------------------------------
--Найти производителя с самой большой средней ценой за товары. 
--Вывести имя производителя и среднюю стоимость

SELECT m.name, ROUND(AVG(p.value),2) FROM goods g
  Join quantity q ON q.goods_id = g.id
  Join prices p ON p.goods_id = g.id
  Join suppliers s ON s.id = g.supplier_id
  Join manufacturer m ON m.id = s.manufacturer_id
GROUP BY m.name
ORDER BY ROUND(AVG(p.value),2)
DESC
LIMIT 1
-----------------------------------------------------------
--Найти товары с нулевым остатком. Вывести имя товара и его цену

SELECT g.name AS ТОВАР, q.value AS ЦЕНА FROM goods g
	Join quantity q ON q.goods_id = g.id
  	Join prices p ON p.goods_id = g.id
  	Join suppliers s ON s.id = g.supplier_id
  	Join manufacturer m ON m.id = s.manufacturer_id
WHERE q.value = (SELECT MIN(value) FROM quantity)
