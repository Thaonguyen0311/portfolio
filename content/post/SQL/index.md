---
title: "SQL"
description: "my random SQL queries"
date: 2024-02-19T20:22:27Z
image: 
math: 
license: 
hidden: false
comments: true
draft: true
---
```sql
SELECT 
DATE_TRUNC(DATE(_DATE_PARTITION,"+7"),MONTH) AS MONTH_ACTIVE
,COUNT(DISTINCT ID) AS TTAL_TRANS
,COUNT(DISTINCT USER_PAYMENT) AS TTAL_USER
,SUM(AMOUNT) AS TTAL_TPV
,COUNT(DISTINCT CASE WHEN AMOUNT >= 10000 AND AMOUNT < 20000 THEN ID ELSE NULL END) AS TRANS_10_20K
,COUNT(DISTINCT CASE WHEN AMOUNT >= 10000 AND AMOUNT < 20000 THEN USER_PAYMENT ELSE NULL END) AS USER_10_20K_
,SUM(CASE WHEN AMOUNT >= 10000 AND AMOUNT < 20000 THEN AMOUNT ELSE 0 END) AS TPV_10_20K
FROM `momovn-prod.BITEAM_EXP.CORE_TRANS_202*` T1
LEFT JOIN `momovn-prod.BITEAM_EXP.D_SERVICE_LIST` T2 ON T1.SERVICE_CODE  = T2.SERVICE_CODE 
WHERE STATUSID = 2
AND T2.NEWVERTICAL_Merchant ='Cashout Bank'
GROUP BY 1
```