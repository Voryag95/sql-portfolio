# Проект 2: Когортный анализ (Retention)

## Описание
Оценка возвращаемости клиентов после первого заказа.

## Инструменты
- SQL (MariaDB)
- DBeaver

## SQL-запрос
WITH first_orders AS (
    SELECT 
        Customer_ID,
        MIN(Order_Date) AS first_order_date
    FROM superstore
    GROUP BY Customer_ID
),
cohort_data AS (
    SELECT 
        s.Customer_ID,
        f.first_order_date,
        DATE_FORMAT(f.first_order_date, '%Y-%m') AS cohort_month,
        TIMESTAMPDIFF(MONTH, f.first_order_date, s.Order_Date) AS month_number
    FROM superstore s
    JOIN first_orders f ON s.Customer_ID = f.Customer_ID
)
SELECT 
    cohort_month,
    month_number,
    COUNT(DISTINCT Customer_ID) AS customers
FROM cohort_data
GROUP BY cohort_month, month_number
ORDER BY cohort_month, month_number;


## Результат
![Результат когортного анализа]
<img width="1920" height="1041" alt="retention_result" src="https://github.com/user-attachments/assets/21ea6500-fa4b-4607-b1cf-8cf2eae514a2" />


## Выводы
- Клиенты совершают только один заказ (в данной выборке).
- Для дальнейшего анализа нужны данные с повторными покупками.
