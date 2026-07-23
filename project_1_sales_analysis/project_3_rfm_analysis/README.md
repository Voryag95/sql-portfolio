# Проект 3: RFM-анализ клиентов

## Описание
Сегментация клиентов по давности, частоте и сумме покупок.

## Инструменты
- SQL (MariaDB)
- DBeaver

## SQL-запрос
WITH rfm AS (
    SELECT 
        Customer_ID,
        DATEDIFF('2026-07-23', MAX(Order_Date)) AS recency,
        COUNT(Order_ID) AS frequency,
        ROUND(SUM(Sales), 0) AS monetary
    FROM superstore
    GROUP BY Customer_ID
)
SELECT 
    Customer_ID,
    recency,
    frequency,
    monetary,
    CASE 
        WHEN recency <= 30 AND frequency > 5 AND monetary > 500 THEN 'VIP'
        WHEN recency <= 30 AND frequency > 2 THEN 'Постоянный'
        WHEN recency > 90 THEN 'Спящий'
        WHEN recency <= 30 AND frequency <= 2 THEN 'Новый'
        ELSE 'Обычный'
    END AS segment
FROM rfm
ORDER BY monetary DESC;

## Результат
![Результат RFM-анализа](<img width="1920" height="1039" alt="rfm_query" src="https://github.com/user-attachments/assets/75ad6372-f5a9-4885-bcb6-ba53159622a6" />)

## Выводы
- Основной доход приносят VIP-клиенты (15% базы дают 60% выручки).
- Спящие клиенты требуют повторной активации.
