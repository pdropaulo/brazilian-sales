# 🛍️📦 Brazilian E-commerce — SQL Insights

Bem-vindo(a) ao meu projeto de análise de dados do **Brazilian E-commerce Dataset** do Kaggle!  
Aqui explorei o universo de compras online no Brasil utilizando consultas **SQL** para extrair insights relevantes sobre **clientes, vendedores, pedidos e pagamentos**.  

---

## 📊 Sobre o Projeto

Este repositório tem como objetivo **explorar dados reais de e-commerce brasileiro** por meio de **consultas SQL** que revelam padrões de comportamento de clientes, desempenho de vendedores e distribuição de receita.  
O foco principal é entender **quem compra, de quem compra, quanto gasta e onde está localizado**.

📁 Estrutura do projeto:
- 📂 `SQL/` – Pasta com todas as consultas utilizadas no projeto.  
- 📄 `README.md` – Este arquivo que explica a estrutura e propósito da análise.  

---

## 🧠 Base de Dados  
📊 Kaggle Dataset: [🔗 Inserir link aqui](COLOQUE_AQUI_O_LINK_DO_DATASET)  

A base inclui informações sobre:
- 👤 Clientes  
- 🛒 Pedidos  
- 🏬 Vendedores  
- 💳 Pagamentos  

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

![sum-payment-city-state](https://github.com/user-attachments/assets/a0564bee-19dc-4c73-93e8-7b1fba28e5ed)
