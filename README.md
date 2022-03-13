--Найти самый дорогой товар. Вывести имя товара и его цену

SELECT g.name AS ТОВАР, p.value AS ЦЕНА FROM goods g
	Join quantity q ON q.goods_id = g.id
  	Join prices p ON p.goods_id = g.id
  	Join suppliers s ON s.id = g.supplier_id
  	Join manufacturer m ON m.id = s.manufacturer_id
WHERE p.value = (SELECT MAX(value) FROM prices)
=================================================================
--Найти товары с нулевым остатком. Вывести имя товара и его цену

SELECT g.name AS ТОВАР, p.value AS ЦЕНА FROM goods g
	Join quantity q ON q.goods_id = g.id
  	Join prices p ON p.goods_id = g.id
  	Join suppliers s ON s.id = g.supplier_id
  	Join manufacturer m ON m.id = s.manufacturer_id
WHERE q.value = (SELECT MIN(value) FROM quantity)
=================================================================
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
===============================================================
--Найти все товары производителей из Москвы. 
--Вывести имена товаров, их цены и имена производителей

SELECT g.name AS ТОВАР, p.value AS ЦЕНА, m.name AS ПРОИЗВОДИТЕЛЬ, m.location AS ГОРОД FROM goods g
  	Join quantity q ON q.goods_id = g.id
  	Join prices p ON p.goods_id = g.id
  	Join suppliers s ON s.id = g.supplier_id
  	Join manufacturer m ON m.id = s.manufacturer_id
WHERE m.location = 'Moscow'
==============================================================
