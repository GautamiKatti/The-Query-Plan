# 01: Intra-Row Identity Filtering
`LeetCode 1148` | `Article Views I` | `Logic: Predicate Comparison`

---

### 🔎 The Problem Logic
We need to identify records where the **subject** (author) and **object** (viewer) are the same entity. Because the source table lacks a Primary Key and contains duplicate entries, the solution must enforce set uniqueness.

---

### 🛠️ Implementation

```sql
SELECT 
    author_id AS id
FROM 
    Views
WHERE 
    author_id = viewer_id
GROUP BY 
    author_id
ORDER BY 
    id ASC;
```
---

### 📑 Technical Breakdown
* **Predicate Filtering:** WHERE author_id = viewer_id isolates self-referential rows at the record level.
* **Cardinality Reduction:** GROUP BY author_id (or DISTINCT) is mandatory to handle the "no primary key" constraint, ensuring each author is only reported once regardless of view count.
* **Deterministic Sorting:** ORDER BY author_id ASC is applied to meet the specific requirements of the result schema.

---

### ⚡ Engineering Insight
**Execution Plan:** In high-volume logging environments, a query like this should ideally trigger an Index-Only Scan. By placing a composite index on (author_id, viewer_id), the database engine can evaluate the equality predicate and the grouping without fetching the full row from the heap.

---

### 🔗 Next Steps
* **Next Problem:** [02: Boolean Conjunction Filtering](https://github.com/GautamiKatti/The-Query-Plan/tree/main/02-Recyclable-and-Low-Fat-Products)
* **Series Index:** [The Query Plan](https://github.com/GautamiKatti/The-Query-Plan)
