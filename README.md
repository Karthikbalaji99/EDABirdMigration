# 🐦 Bird Migration Exploratory Data Analysis

A comprehensive, step-by-step analysis of a synthetic bird migration dataset (10,000 records, 40+ features) to uncover flight behaviors, environmental influences, seasonal rhythms, and migratory success patterns. This project demonstrates advanced EDA techniques—data cleaning, statistical plots, geospatial mapping, dimensionality reduction, clustering, and focused deep dives.

---

## 📖 Project Overview

**Objective:**  
Uncover core migratory strategies and environmental dependencies in a global, synthetic bird tracking dataset. We explore:

- Flight metrics (distance, duration, speed, altitude)  
- Environmental factors (weather, temperature, humidity)  
- Temporal patterns (spring vs. fall migrations)  
- Outcomes (success vs. interruption)  
- Behavioral clusters (distinct migration strategies)

**Why Synthetic Data?**  
Privacy-safe, fully-synthetic yet realistic records allow unrestricted exploration and portfolio showcase without ethical constraints.

---

## 🗂️ Dataset Description

- **Records:** 10,000 individual bird migrations  
- **Features (40+):**  
  - **Numeric:** Flight_Distance_km, Flight_Duration_hours, Average_Speed_kmph, Max_Altitude_m, Min_Altitude_m, Temperature_C, Wind_Speed_kmph, Humidity_%, Pressure_hPa, Visibility_km, Rest_Stops, Predator_Sightings, Flock_Size, Tag_Weight_g, Recovery_Time_days, Observation_Counts  
  - **Categorical:** Bird_ID, Species, Region, Habitat, Weather_Condition, Migration_Reason, Migration_Start_Month, Migration_End_Month, Tag_Type, Migrated_in_Flock, Tracking_Quality, Migration_Interrupted, Interrupted_Reason, Migration_Success, Recovery_Location_Known  
  - **Derived “Origin”**: Combined start latitude/longitude  




---

## 🚀 Analysis Workflow & Inferences

### 1️⃣ Data Preparation & Cleaning  
- **Load & Inspect:** Examined `df.info()`, missing values, data types.  
- **Handle Missing “Interrupted_Reason”:** ~10% NaNs → filled with `"Unknown"` to preserve all records.  
- **Convert Columns:** Month fields to ordered categories, key fields to `category` dtype.  
- **Inference:** After cleaning, the dataset is fully populated and correctly typed, enabling robust downstream analysis.

---

### 2️⃣ Univariate & Bivariate Exploration  
- **Univariate:**  
  - **Species Counts:** No single dominating species—“Other” category comprises 71%.  
  - **Flight Distance & Duration:** Right-skewed distributions; most flights cluster around 2,000–3,000 km and 40–60 h.  
  - **Weather Conditions:** “Foggy” and “Stormy” dominate (each ~20%).  

- **Bivariate:**  
  - **Distance vs. Speed (Scatter):** Weak positive correlation—longer trips tend to be slightly faster on average.  
  - **Distance by Region (Boxplot):** North/South America flights slightly longer median than Europe/Africa.  
  - **Altitude by Weather (Boxplot):** Clear conditions permit highest altitudes; storms force lower ceilings.  
  - **Nesting Success by Habitat:** Wetlands & grasslands show marginally higher success rates.  

- **Inference:** Basic distributions align with ecological expectations: adverse weather constrains altitude; habitat influences nesting success; flight characteristics vary modestly by region.

---

### 3️⃣ Geospatial Mapping  
- **Plotly Routes:** Sampled 500 birds; thick, semi-opaque lines on light-gray land highlight colorful species-coded tracks.  
- **Folium Interactive Map:** Overlay of 200 trajectories with hoverable start/end markers.  

- **Inference:** Migration corridors are global—transpolar flights in spring, intercontinental return paths in fall. Visual clarity accentuates species ranges and migration breadth.

---

### 4️⃣ PCA & Clustering  
- **Standardization:** Scaled 16 numeric features.  
- **PCA:**  
  - **PC1 (6.5% variance):** Dominated by flight duration (0.39) and distance (0.33).  
  - **PC2 (6.4% variance):** Driven by temperature (0.34), min altitude (0.34), visibility (0.32), with negative loadings on max altitude and rest stops.  
- **K-Means (k=4):** Identified four migration strategy clusters:  
  1. **Cluster 0:** Long, high-altitude flights with moderate stops  
  2. **Cluster 1:** Longest distances + heavy rest-stop behavior  
  3. **Cluster 2:** Shortest, fastest, large-flock migrations  
  4. **Cluster 3:** Mid-range opportunistic flyers  

- **Inference:** The low variance explained by first two PCs indicates a need for multiple components to capture complexity; clustering in PCA space revealed coherent behavioral types.

---

### 5️⃣ Seasonal & Time-Based Patterns  
- **Migration Counts by Month:**  
  - Bi-modal peaks: **spring** (Jan–May, peak in Mar–Apr) and **fall** (Sep–Nov, peak in Oct).  
  - Virtually no migrations in June–Aug or December.  
  - **Cluster nuances:** Cluster 0 peaks earlier in spring; Cluster 2 maintains a robust autumn presence.  

- **Flight Duration & Distance by Month & Cluster:**  
  - **Duration:** Cluster 0 highest (55–62 h), Cluster 1 next (52–60 h), Cluster 3 mid (45–54 h), Cluster 2 lowest (45–50 h). Spring variability > Fall consistency.  
  - **Distance:** Cluster 1 longest (2,700–2,800 km), Cluster 0 (2,500–2,650 km), Cluster 3 (2,300–2,450 km), Cluster 2 shortest (2,200–2,350 km).  

- **Inference:** Behavioral clusters maintain signature flight profiles regardless of exact start month; spring migrations exhibit greater variation, while fall returns are more uniform.

---

### 6️⃣ Categorical Cross-Tabs & Heatmaps  
- **Success by Habitat:**  
  - **Wetlands** highest success (52.3%), **coastal** (~51.8%), **grassland** (~51.7%).  
  - **Mountains** lowest (~48% success).  
- **Interruption by Weather:**  
  - **Windy** most interruptive (50.5%), followed by storms/fog (~50.3%).  
  - **Rainy** slightly less disruptive (50.2%).  

- **Inference:** Routes through wetlands/coasts favor successful completion; mountainous terrain poses challenges. High winds slightly increase interruption risk more than storms or fog.

---

### 7️⃣ Cluster 2 Deep-Dive  
- **Habitat Mix:** Urban (~17%), Wetland (~17%), Grassland (~17%), Mountain (~16%), Coastal (~16%), Forest (~17%)  
- **Weather Mix:** Foggy (~21%), Windy (~21%), Clear/Stormy (~20%), Rainy (~18%)  
- **Success Rate:** 51.1% successful vs. 48.9% failed  

- **Inference:** Cluster 2’s fast-flock strategy operates under diverse environments and weather but achieves only average success—flocking speeds flight but doesn’t markedly improve outcomes.

---

## ✨ Conclusion

This notebook demonstrates how layered EDA—combining cleaning, statistical plots, geospatial visualization, PCA, clustering, seasonal analysis, and cross-tab heatmaps—can reveal intricate patterns in complex ecological data. The derived insights into migratory strategies, habitat resilience, and weather impacts form a rich narrative suitable for ecological modeling, BI dashboards, or ML pipelines.

---


Feel free to explore, extend, and adapt this analysis for real-world tracking studies or interactive dashboards!
