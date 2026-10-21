# Supply Chain Distribution Network Optimization

An end-to-end Linear Programming (LP) case study demonstrating cost minimization for a multi-source, multi-destination supply chain network across India.

---

## 📌 Project Overview

This project models and solves a classical **Transportation Optimization Problem** using Python, Pyomo, and the COIN-OR Branch and Cut (CBC) solver.

The goal is to determine the most cost-effective distribution plan to transport products from **4 manufacturing plants** to **10 key market regions** across India while ensuring:
1. Plant supply capacity is not exceeded.
2. Market demand is fully satisfied.
3. Total transportation cost is minimized.

---

## 🏭 Network Structure & Data

### **Nodes Overview**
* **4 Manufacturing Plants (Sources):** Chandigarh, Raipur, Dharwad, Howrah
* **10 Regional Markets (Destinations):** Delhi, Mumbai, Bengaluru, Nagpur, Hyderabad, Chennai, Kolkata, Patna, Lucknow, Ahmedabad

---

### 📊 Cost, Supply, and Demand Matrix

| Plant / Market | Delhi | Mumbai | Bengaluru | Nagpur | Hyderabad | Chennai | Kolkata | Patna | Lucknow | Ahmedabad | **Supply Capacity** |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Chandigarh** | 10 | 15 | 25 | 20 | 22 | 28 | 30 | 18 | 12 | 8 | **500** |
| **Raipur** | 18 | 12 | 20 | 10 | 15 | 22 | 14 | 16 | 20 | 16 | **600** |
| **Dharwad** | 25 | 18 | 10 | 15 | 12 | 18 | 25 | 30 | 22 | 14 | **400** |
| **Howrah** | 30 | 25 | 28 | 22 | 20 | 15 | 10 | 12 | 18 | 25 | **700** |
| **Market Demand** | **200** | **300** | **250** | **150** | **200** | **200** | **300** | **100** | **150** | **200** | **Total Supply: 2200** <br> **Total Demand: 2050** |

---

## 📐 Mathematical Model Formulation

### **Sets & Indices**
* $i \in I = \{\text{Chandigarh, Raipur, Dharwad, Howrah}\}$ (Set of Plants)
* $j \in J = \{\text{Delhi, Mumbai, Bengaluru, Nagpur, Hyderabad, Chennai, Kolkata, Patna, Lucknow, Ahmedabad}\}$ (Set of Markets)

### **Parameters**
* $C_{i,j}$: Cost of shipping one unit from plant $i$ to market $j$
* $S_i$: Maximum supply available at plant $i$
* $D_j$: Minimum demand required at market $j$

### **Decision Variables**
* $X_{i,j} \ge 0$: Quantity of goods shipped from plant $i$ to market $j$

---

### **Mathematical Formulation**

#### **1. Objective Function**
Minimize total supply chain transportation cost:
$$\text{Minimize } Z = \sum_{i \in I} \sum_{j \in J} C_{i,j} \cdot X_{i,j}$$

#### **2. Supply Constraints**
Total shipments from plant $i$ cannot exceed its supply capacity:
$$\sum_{j \in J} X_{i,j} \le S_i \quad \forall i \in I$$

#### **3. Demand Constraints**
Total shipments received by market $j$ must satisfy its demand:
$$\sum_{i \in I} X_{i,j} \ge D_j \quad \forall j \in J$$

#### **4. Non-Negativity Constraints**
$$X_{i,j} \ge 0 \quad \forall i \in I, \forall j \in J$$

---

## 🎯 Optimal Solution Summary

* **Optimal Minimum Cost:** **₹23,050**
* **Status:** Optimal Solution Found (CBC Solver - 12 Iterations)

### **Optimal Shipping Allocation Matrix**

| Plant | Market Destination | Units Shipped | Unit Cost | Total Route Cost |
| :--- | :--- | :---: | :---: | :---: |
| **Chandigarh** | Ahmedabad | 200 | 8 | 1,600 |
| | Delhi | 200 | 10 | 2,000 |
| | Lucknow | 100 | 12 | 1,200 |
| **Dharwad** | Bengaluru | 250 | 10 | 2,500 |
| | Hyderabad | 150 | 12 | 1,800 |
| **Howrah** | Kolkata | 300 | 10 | 3,000 |
| | Patna | 100 | 12 | 1,200 |
| | Chennai | 200 | 15 | 3,000 |
| | Lucknow | 50 | 18 | 900 |
| **Raipur** | Nagpur | 150 | 10 | 1,500 |
| | Mumbai | 300 | 12 | 3,600 |
| | Hyderabad | 50 | 15 | 750 |
| **Total Cost** | | | | **₹23,050** |

---

## 🛠️ Installation & Setup

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/your-username/supply-chain-network-optimization.git
   cd supply-chain-network-optimization
   ```

2. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Install CBC Solver (if running locally without pre-bundled solver):**
   * **Windows/Linux/Mac via Conda:**
     ```bash
     conda install -c conda-forge coincbc
     ```

4. **Run the Notebook:**
   ```bash
   jupyter notebook
   ```

---

## 💻 Tech Stack
* **Language:** Python
* **Optimization Modeling:** Pyomo
* **Solver:** COIN-OR CBC (Branch and Cut)
* **Environment:** Jupyter Notebook / Anaconda