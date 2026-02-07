# 03: Relational-Product-Mapping
`LeetCode 1068` |  `Product Sales Analysis I` | `Logic: Equi-Join Resolution`

---

### 🔎 The Problem Logic
We need to retrieve the sales details (`year`, `price`) along with the descriptive name of the product. The `Sales` table contains the transaction data but only references the `product_id`. We must perform a **Join** to resolve these IDs into human-readable names.

---

### 🛠️ Implementation

```sql
SELECT 
    p.product_name, 
    s.year, 
    s.price
FROM 
    Sales s
INNER JOIN 
    Product p ON s.product_id = p.product_id;
```

---

### 📑 Technical Breakdown
* **Join Type:** An INNER JOIN (or JOIN) is used because we only want to report sales for products that exist in our product catalog.
* **Key Matching:** s.product_id = p.product_id establishes the link between the transaction (Fact) and the description (Dimension).
* **Column Selection:** We explicitly prefix columns (e.g., s.year) to avoid ambiguity and improve query parsing speed.

---

### ⚡ Engineering Insight
**Execution Plan:** Hash Join vs. Merge Join In a large-scale database, the engine often chooses a Hash Join for this operation. It builds a temporary hash table of the smaller table (Product) in memory and then scans the larger table (Sales) to find matches. If both tables are sorted by product_id, the engine may opt for a Merge Join, which is even faster as it avoids the hash overhead.

---

### 🔗 Next Steps
* **Next Problem:** []()
* **Series Index:** [The Query Plan](https://github.com/GautamiKatti/The-Query-Plan)
