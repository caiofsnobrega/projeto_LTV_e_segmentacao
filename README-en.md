# Customer Segmentation and Lifetime Value (LTV) Prediction in E-commerce

🌐 *[Veja a versão em Português aqui](README.md)*

This project was developed to solve a classic e-commerce challenge: understanding customer behavior and predicting how much they will spend in the future. With this information, a company can stop spending money on generic marketing campaigns and focus on the right customers.

The solution was split into two main parts:
1. **Clustering:** Identifying current customer profiles.
2. **Regression:** Predicting each customer's revenue for the next 3 months.

---

## 🛠️ Project Methodology

The project was built step-by-step following a logical data science pipeline:

Note: As an integral part of the EBAC Data Science course, this project received tutoring and artificial intelligence support at certain stages.

### 1. Data Cleaning and Preparation
The raw data contained transactions from a UK-based e-commerce. In this stage:
* Records missing customer identification were removed.
* Returns and cancellations were handled carefully so they wouldn't distort the true historical revenue.

### 2. Feature Engineering (RFM Model)
To understand customer behavior, thousands of invoice lines were transformed into 3 key metrics for each individual:
* **Recency (R):** Days since the last purchase.
* **Frequency (F):** Total number of purchases made.
* **Monetary (M):** Total amount of money spent.

### 3. Customer Clustering (K-Means)
Using the K-Means algorithm, the customer base was divided into groups with similar purchasing habits. To find the optimal number of groups, the **Elbow Method** was used, which enabled the analysis of the distribution of centroids (the typical profile of each cluster).

### 4. LTV Prediction (Machine Learning with XGBoost)
To test if it would be possible to predict future spend over the next 3 months, a time-based split was set up. The model was trained on a historical period and validated on a subsequent period, preventing any data leakage.

Two major real-world challenges came about: a large number of customers didn't buy anything in the future period (leading to an excess of zeros), and a few customers spent extremely high amounts. Traditional regression models failed, so the final solution was to implement an **XGBoost Regressor with Tweedie Loss**, a specialized industry technique tailored for this type of zero-inflated, highly skewed data.

---

## 📊 Key Insights and Results

### The 3 Identified Customer Profiles:
* **Top Group:** High spenders, frequent shoppers, with highly recent activity. They should receive exclusive loyalty perks.
* **Intermediate Group:** Occasional shoppers. They need targeted recommendations and incentives to become Tops.
* **Inactive Group:** Low spenders who haven't bought anything in a long time. Aggressive win-back campaigns could be applied here.

### Prediction Model Performance:
The final model successfully brought the $R^2$ into positive territory at **0.0554**. While human purchasing behavior in non-contractual settings is highly chaotic, the model successfully captured genuine business intelligence. The feature importance analysis proved that a customer's historical **Monetary** value is the strongest predictor of their future spend.

## Visualizations Produced throughout the Project:

### Clusters:

![Clusters Visualization](images/grafico_pairplot.png)

![centroids Plot](images/grafico_centroides.png)

![Elbow Method](images/grafico_cotovelo.png)

### Distributions:

![Distributions without treatment plot](images/grafico_distribuicoes.png)

![Normalized Features](images/grafico_normalizadas.png)

### Feature Importances:

![Features Importances](images/grafico_importancias.png)
---

## 🧠 Conclusion and Takeaways

This project demonstrated that real-world data is messy and rarely fits textbook assumptions. The biggest achievement was diagnosing why the baseline models failed and applying an advanced technical solution (Tweedie Loss) to mitigate the distortions caused by extreme outliers and a zero-inflated target variable.

As next steps to improve performance, engineering contextual features — such as top product categories purchased — would be highly recommended.

---

## 📁 Repository Structure

* `images/`: Charts and visualizations generated during the analysis.
* `projeto_ltv_ecommerce.ipynb`: Jupyter notebook containing the full Python pipeline.
* `requirements.txt`: List of dependencies required to run the project.
