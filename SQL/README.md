# 🛍️📦 Brazilian E-commerce — SQL Insights

Bem-vindo(a) ao meu projeto de análise de dados do **Brazilian E-commerce Dataset** do Kaggle!  
Aqui explorei o universo de compras online no Brasil utilizando consultas **SQL** para extrair insights relevantes sobre **clientes, vendedores, pedidos e pagamentos**.  

---

## 📊 Sobre o Projeto

Este repositório tem como objetivo **explorar dados reais de e-commerce brasileiro** por meio de **consultas SQL** que revelam padrões de comportamento de clientes, desempenho de vendedores e distribuição de receita.  
O foco principal é entender **quem compra, de quem compra, quanto gasta e onde está localizado**.

---

## 🧠 Base de Dados  
📊 Kaggle Dataset: 🔗 [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) 

A base inclui informações sobre:
- 👤 Clientes  
- 🛒 Pedidos  
- 🏬 Vendedores  
- 💳 Pagamentos  

---

### ♨ Procedimento
Após baixadas as planilhas, o uso de knime foi necessário para transformar os aquivos .csv em uma base de dados. 
"O KNIME é uma plataforma de código aberto e "low-code" para análise de dados, integração e aprendizado de máquina. Seu uso de uma interface visual de arrastar e soltar (drag-and-drop) permite que usuários construam fluxos de trabalho analíticos sem escrever linhas de código, embora também ofereça a opção de integrar códigos para personalização avançada." Vale ressaltar que essa não é a melhor maneira de integrar os dados a uma base de dados, sendo necessário o uso de loops. No entanto, a distância temporal entre o meu último uso do KNIME e a atualidade é um tanto grande, tendo-me feito recorrer a métodos mais "brutos".
![brazilian_sales-knime-etl](https://github.com/user-attachments/assets/40486059-becc-4ca3-af47-9cbf535369c4)  

---

## 🔎 Consultas SQL e Insights

### 1️⃣ Count customers per seller 👥🛍️

```sql
SELECT COUNT(CLIENTE) QT, VENDEDOR 
FROM (
  SELECT CD.CUSTOMER_ID CLIENTE, ID.SELLER_ID VENDEDOR 
  FROM CUSTOMER_DATASET CD
  INNER JOIN ORDERS_DATASET OD ON (OD.CUSTOMER_ID = CD.CUSTOMER_ID)
  INNER JOIN ITEMS_DATASET ID ON (OD.ORDER_ID = ID.ORDER_ID)
)
GROUP BY VENDEDOR
ORDER BY QT DESC;
```

![count-customer-per-seller](https://github.com/user-attachments/assets/6554f6fa-50dd-4c35-a0c0-7f95b65a3d6b)

### 2️⃣ Count orders per state 📦📍

```sql
SELECT COUNT(ID_) ESTADO 
FROM (
  SELECT OD.ORDER_ID ID_, CD.CUSTOMER_STATE ESTADO 
  FROM ORDERS_DATASET OD
  INNER JOIN CUSTOMER_DATASET CD ON (OD.CUSTOMER_ID = CD.CUSTOMER_ID)
)
GROUP BY ESTADO
ORDER BY COUNT(ID_) DESC;
```

![sum-orders-per-state](https://github.com/user-attachments/assets/dfc5329c-4add-4234-a6df-13cb6aa997d4)

### 3️⃣ Sum payment per city and state 💰🌆

```sql
SELECT ESTADO, CIDADE, CAST(SUM(PAG) AS NUMERIC(15, 2))
FROM (
  SELECT PD.PAYMENT_VALUE PAG, CUSTOMER_DATASET.CUSTOMER_CITY CIDADE, CUSTOMER_DATASET.CUSTOMER_STATE ESTADO
  FROM PAYMENT_DATASET PD
  INNER JOIN ORDERS_DATASET OD ON (OD.ORDER_ID = PD.ORDER_ID)
  INNER JOIN CUSTOMER_DATASET ON (OD.CUSTOMER_ID = CUSTOMER_DATASET.CUSTOMER_ID)
)
GROUP BY 1, 2;
```

![sum-payment-city-state](https://github.com/user-attachments/assets/a0564bee-19dc-4c73-93e8-7b1fba28e5ed)

### 4️⃣ Sum per type payment 💳📊

```sql
SELECT CAST(SUM(PAG) AS NUMERIC(15, 2)), TIPO, CLIENTE, COD 
FROM (
  SELECT PD.PAYMENT_VALUE PAG, PD.PAYMENT_TYPE TIPO, CUSTOMER_DATASET.CUSTOMER_ID CLIENTE, 
         CUSTOMER_DATASET.CUSTOMER_ZIP_CODE_PREFIX COD
  FROM PAYMENT_DATASET PD
  INNER JOIN ORDERS_DATASET OD ON (OD.ORDER_ID = PD.ORDER_ID)
  INNER JOIN CUSTOMER_DATASET ON (OD.CUSTOMER_ID = CUSTOMER_DATASET.CUSTOMER_ID)
)
GROUP BY 2, 3, 4;
```
![sum-per-type-payment](https://github.com/user-attachments/assets/3ff8bcc3-9d1f-4a9b-8832-684afb603951)
![sum-per-type-payment-2](https://github.com/user-attachments/assets/4f4a0262-8b4a-497e-926f-3e91eb60d3c4)

📬 Contato

📧 E-mail: [p.paulo.pp08@gmail.com](p.paulo.pp08@gmail.com)  
💼 LinkedIn: [Pedro Andrade](https://www.linkedin.com/in/pdropaulora)  
🐙 GitHub: [pdropaulo](https://www.github.com/pdropaulo)  

🌟 Contribuição  

Fique à vontade para sugerir melhorias ou abrir issues para discussões!  

📌 Créditos  

📊 Dataset disponível no Kaggle: 🔗 [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)  
👨‍💻 Projeto desenvolvido para fins de estudo e prática em SQL.  
