# 🏀 NCAA Tournament Prediction & Simulation

## Project Overview
This project predicts and simulates the **NCAA Men’s and Women’s Basketball Tournament** using **Elo ratings and machine learning (XGBoost)**. The final outputs include:

✅ **Predicted probabilities for tournament matchups**  
✅ **Simulated tournament brackets** (Men's & Women's)  
✅ **Visualized NCAA bracket progressions**  

---

## Step 1: Data Preparation
To build a predictive model, we used the following datasets:  
- `MTeams.csv / WTeams.csv` → Team information (ID, names, etc.).  
- `MRegularSeasonCompactResults.csv / WRegularSeasonCompactResults.csv` → Regular season results.  
- `MNCAATourneyCompactResults.csv / WNCAATourneyCompactResults.csv` → NCAA tournament results.  
- `MNCAATourneySeeds.csv / WNCAATourneySeeds.csv` → Tournament seeding data.  

### Actions Taken:
1. **Loaded and cleaned data** (handled missing values, merged relevant tables).  
2. **Mapped Team IDs to Team Names** (so visualizations are readable).  
3. **Prepared structured datasets** for Elo rating calculations and ML modeling.  

---

## Step 2: Calculating Elo Ratings for Teams
Elo ratings provide a **dynamic ranking system** to measure team strength over time.  

### Elo Calculation Steps:
1. **Set a baseline rating (1500) for all teams.**  
2. **Updated ratings after every game** using:  
   - **Win Probability Formula:**  
     ```
     P(A) = 1 / (1 + 10^((Elo_B - Elo_A) / 400))
     ```
   - **Elo Update Formula:**  
     ```
     Elo_new = Elo_old + K * (Actual - Expected)
     ```
3. **Stored final Elo ratings per team** to use as ML features.  

---

## Step 3: Training the Machine Learning Model (XGBoost)
We trained an **XGBoost model** to predict the probability of a team winning a matchup.  

### Features Used:
- **Elo ratings** (Team A & Team B)  
- **Elo rating difference**  
- **Tournament seeding differences**  

### Training Steps:
1. **Created labeled matchups** from tournament results.  
2. **Split data into training & validation sets.**  
3. **Used RandomizedSearchCV for hyperparameter tuning.**  
4. **Trained an XGBoost model** on past NCAA games.  
5. **Evaluated performance using log-loss and accuracy.**  

---

## Step 4: Generating Predictions for Submission
Once the model was trained, we generated **predictions for upcoming matchups**.  

### Steps Taken:
1. **Extracted matchups from submission files (`SampleSubmissionStage1` & `Stage2`).**  
2. **Retrieved Elo ratings & team features for each matchup.**  
3. **Used the trained XGBoost model to predict probabilities.**  
4. **Saved results into submission files:**  
   - `NCAA_FinalPredictions_MenStage1.csv`  
   - `NCAA_FinalPredictions_MenStage2.csv`  
   - `NCAA_FinalPredictions_WomenStage1.csv`  
   - `NCAA_FinalPredictions_WomenStage2.csv`  
   - `NCAA_FinalPredictions_ConcatMenWomen.csv`  

---

## Step 5: Enhancing Predictions with Additional Features
To improve prediction accuracy, we experimented with:  
**Regular season win-loss percentages**  
**Head-to-head results between teams**  
**Advanced metrics like margin of victory & strength of schedule**  

These were incorporated into the **final model features**, boosting performance.

---

## Step 6: Hyperparameter Optimization & Model Selection
To **improve model accuracy**, we:  
**Used RandomizedSearchCV** to fine-tune `max_depth`, `n_estimators`, `learning_rate`, and regularization parameters.  
**Implemented early stopping** to prevent overfitting.  
**Balanced training data** (to account for upsets).  

---

## Step 7: Simulating the NCAA Tournament
Once probabilities were generated, we simulated the tournament **round-by-round**.

### Simulation Process:
1. **Started with all teams from the first round.**  
2. **At each round, used probabilities to "simulate" who advances.**  
3. **Eliminated losing teams until a final champion was determined.**  
4. **Stored all round winners for bracket visualization.**  

---

## Step 8: Visualizing the NCAA Tournament Bracket
We used **Matplotlib** to create a **clear bracket-style visualization** of the tournament results.

### Features of the Visualization:
**Displays round-by-round progression**  
**Connects teams with lines showing how they advance**  
**Readable and structured bracket layout**  

---

## Key Takeaways & Results
🏆 **We successfully built a predictive model for the NCAA tournament.**  
🏆 **We simulated the full tournament and visualized the bracket.**  
🏆 **The final model uses Elo ratings + ML to predict matchups accurately.**  

---

## Future Improvements to Enhance the Project
While the current model performs well, **several enhancements** could further improve accuracy and insights:  

### 1. Incorporate Player-Level Data  
- **Use individual player statistics** (e.g., points per game, rebounds, assists).  
- **Factor in injuries & lineup changes** to adjust team strength dynamically.  
- **Track player form trends** to weigh recent performance more heavily.  

### 2️. Improve Strength of Schedule & Opponent Adjustments  
- **Enhance Elo calculations** by incorporating each team's **strength of schedule (SOS)**.  
- Adjust Elo updates based on **how strong the opponent was**, not just win/loss.  
- Consider **home vs. away performance** (home-court advantage).  

### 3️. Use Advanced Machine Learning Models  
- Experiment with **deep learning (neural networks)** for predictive modeling.  
- Try **ensemble models** (combine XGBoost with Random Forests, Neural Networks).  
- Implement **Bayesian modeling** to capture uncertainty in predictions.  

### 4️. Optimize Simulation Logic for Tournament Bracket  
- **Improve bracket visualization** (clearer team matchups, color-coded win probabilities).  
- **Allow multiple simulations** (run 10,000 tournament simulations & show probability of each team winning).  
- Introduce **live-updating simulation** (adjust predictions as real games happen).  

### 5️. Leverage More Data Sources  
- **Use historical betting odds** to improve prediction accuracy.  
- Incorporate **team chemistry & coaching effects** as additional features.  
- Gather **real-time Twitter sentiment analysis** to factor in external hype/momentum.  

---

Generate by Engracia Batista
Chrysalytics
March 2025
