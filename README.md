# Car_Price_Prediction

__Polish Report__: I highly encourage you to read the full Polish report: 

__Dataset__: This project utilizes the dataset available at: 

The project description in __English__ 🇬🇧 can be found below the __Polish__ 🇵🇱 one.

# Polska Wersja

## Predykcja Cen Samochodów

Projekt ma na celu stworzenie modelu regresyjnego przewidującego ceny samochodów w oparciu o dane zbiory **web scrapingowe**. W projekcie wykorzystano metody eksploracji danych (EDA), przetwarzania wstępnego i modelowania z użyciem **XGBoost** oraz optymalizację hiperparametrów przy użyciu **Optuna**.

---

## Spis Treści
1. [Wprowadzenie](#wprowadzenie)  
2. [Dane](#dane)  
3. [Analiza Eksploracyjna Danych (EDA)](#analiza-eksploracyjna-danych-eda)  
4. [Preprocessing](#preprocessing)  
5. [Modelowanie](#modelowanie)  
6. [Wyniki](#wyniki)  
7. [Podsumowanie](#podsumowanie)  
8. [Autorzy](#autorzy)  

---

## Wprowadzenie
Konkurs Kaggle organizowany przez **DSC PJATK** miał na celu rekrutację nowych członków koła naukowego. 
- **Cel projektu**: Zbudować model regresyjny przewidujący cenę samochodu na podstawie rzeczywistych danych.  
- **Główne wyzwania**:  
  - Duża liczba zmiennych i rekordów (ponad 1,38 mln w 3 zestawach).  
  - Zrozumienie specyfiki rynku motoryzacyjnego.  
  - Wybór optymalnego modelu i odkrycie istotnych zależności między danymi.  
  - Radzenie sobie z dużą ilością wartości kategorycznych.

---

## Dane
W analizie użyto danych z pliku `sales_ads_train.csv`, zawierającego zarówno zmienne ilościowe (np. cena, rok produkcji, pojemność silnika) jak i jakościowe (np. marka, model, kolor). Przed przystąpieniem do analizy sprawdzono dane pod kątem duplikatów, braków oraz nieprawidłowych wartości.

---

## Analiza Eksploracyjna Danych (EDA)
Rozpoczęliśmy od analizy kilku macierzy korelacji na oryginalnym zbiorze danych – tylko jedna z nich okazała się wiarygodna, dlatego jej wyniki wykorzystujemy dalej.  
- Rozkład cen został przedstawiony za pomocą histogramu i boxplotu po logarytmicznej transformacji, co usprawnia zarówno wizualizację, jak i trenowanie modelu.  
- Wykresy punktowe wykazały, że wyższy przebieg naturalnie wiąże się z niższą ceną.  
- Zależność między rokiem produkcji a ceną jest wyraźna dla nowszych pojazdów, lecz dla starszych – niejednoznaczna, prawdopodobnie z powodu antyków i aut kolekcjonerskich.  
- Rozkłady mocy i pojemności silnika skupiają się wokół popularnych wartości, a ich wykres punktowy potwierdza dodatnią korelację między tymi zmiennymi.  
- Bar charty Top 20 marek i modeli ujawniają dominujące pozycje na rynku wtórnym, a dodatkowe countploty i boxploty dla kolumn kategorycznych pomagają zidentyfikować najczęściej występujące cechy oraz rozpiętość cen w obrębie kategorii.  
- Analiza wpływu wyposażenia (np. Bluetooth, czujniki parkowania) na cenę pokazuje, że obecność tych elementów może podnosić cenę.  
- Ostatecznie, mapy Polski prezentują regionalne różnice w liczbie ofert oraz średnich cenach.

---

## Preprocessing
Aby przygotować dane do modelowania, wykonano następujące kroki:
1. **Imputacja braków** – uzupełnienie brakujących danych (średnia, moda, interpolacja) przy czym uzupełnienia przeprowadzono również z wykorzystaniem pomocniczego datasetu zawierającego informacje o markach i modelach aut.  
2. **Usuwanie niekompletnych rekordów** – eliminacja obserwacji z nadmierną ilością braków.  
3. **Kodowanie zmiennych** – zastosowano Binary, One-Hot oraz Target Encoding.  
4. **Skalowanie** – przeskalowanie wybranych zmiennych ilościowych.  
5. **Feature Engineering** – tworzenie nowych cech. Przy skrajnych wartościach dodawane były nowe kolumny (np. "Duża Moc 1-0") zamiast usuwania tych wartości, ponieważ outliery występowały również w zbiorze testowym.

---

## Modelowanie
W projekcie zastosowano algorytm **XGBoost**:
- **Optymalizacja hiperparametrów** – wykorzystanie biblioteki **Optuna** (np. `n_estimators`, `max_depth`, `learning_rate`).  
- **Feature Importance** – kluczowe cechy to rok produkcji, automatyczna skrzynia biegów, LED-owe światła, Bluetooth, generacja pojazdu oraz stan techniczny.

---

## Wyniki
- **Miara oceny**: RMSE (Root Mean Squared Error).  
- **Uzyskane RMSE**: Około **19085**.  
Model wykazał dobrą jakość predykcji, pod warunkiem odpowiedniego przygotowania danych.

---

## Podsumowanie
Projekt polega na budowie modelu regresyjnego do przewidywania cen samochodów. Dzięki starannemu przygotowaniu danych, szczegółowej analizie oraz zastosowaniu zaawansowanych metod modelowania (w tym XGBoost z optymalizacją hiperparametrów), udało się uzyskać konkurencyjne wyniki. Całość stanowi praktyczny przykład wykorzystania uczenia maszynowego w analizie rynku motoryzacyjnego.

---

## Autorzy
- __Łukasz Podoba__  
- __Bartosz Paszko__

_Przygotowane w ramach projektu Data Science Club PJATK – Marzec 2025._

---

# English Version

## Car Price Prediction

The project aims to build a regression model to predict car prices based on data from **web-scraped** sources. In this project, we applied exploratory data analysis (EDA), preprocessing, and modeling techniques using **XGBoost** along with hyperparameter tuning via **Optuna**.

---

## Table of Contents
1. [Introduction](#introduction)  
2. [Data](#data)  
3. [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)  
4. [Preprocessing](#preprocessing)  
5. [Modeling](#modeling)  
6. [Results](#results)  
7. [Summary](#summary)  
8. [Authors](#authors)  

---

## Introduction
The Kaggle competition organized by **DSC PJATK** aimed to recruit new members for the scientific club.
- **Project Goal**: Build a regression model that predicts car prices using real data.  
- **Main Challenges**:  
  - A large number of variables and records (over 1.38 million across 3 datasets).  
  - Understanding the specifics of the automotive market.  
  - Selecting the optimal model and discovering key relationships within the data.  
  - Handling a high volume of categorical values.

---

## Data
The analysis used data from the `sales_ads_train.csv` file, which contains both quantitative variables (e.g., price, production year, engine capacity) and qualitative variables (e.g., make, model, color). Before analysis, the data were checked for duplicates, missing values, and invalid entries.

---

## Exploratory Data Analysis (EDA)
We began by analyzing several correlation matrices on the original dataset—only one proved reliable, so we based our further analysis on its results.  
- The price distribution was visualized using a histogram and a boxplot after a logarithmic transformation, which enhances both visualization and model training.  
- Scatter plots showed that higher mileage is naturally associated with lower prices.  
- The relationship between production year and price is clear for newer vehicles, but for older cars it is ambiguous, likely due to antiques and collector vehicles.  
- The distributions of engine power and engine capacity are centered around popular values, and their scatter plot confirms a positive correlation between these variables.  
- Bar charts displaying the Top 20 car makes and models reveal dominant positions in the secondary market, while additional count plots and boxplots for categorical variables help identify the most common features and the price ranges within each category.  
- An analysis of the impact of equipment (e.g., Bluetooth, parking sensors) on price shows that the presence of these features can increase the price.  
- Finally, maps of Poland illustrate regional differences in the number of listings and average prices.

---

## Preprocessing
To prepare the data for modeling, the following steps were taken:
1. **Imputation of Missing Values** – filling in missing data (mean, mode, interpolation), additionally utilizing an auxiliary dataset containing information about car makes and models.
2. **Removal of Incomplete Records** – eliminating observations with an excessive number of missing values.  
3. **Variable Encoding** – applying Binary, One-Hot, and Target Encoding.  
4. **Scaling** – scaling selected quantitative variables.  
5. **Feature Engineering** – creating new features. For extreme values, new columns (e.g., "High Power 1-0") were added instead of removing those values, since outliers also appeared in the test set.

---

## Modeling
The project employed the **XGBoost** algorithm:
- **Hyperparameter Tuning** – using the **Optuna** library (e.g., `n_estimators`, `max_depth`, `learning_rate`).  
- **Feature Importance** – key features include production year, automatic transmission, LED lights, Bluetooth, vehicle generation, and technical condition.

---

## Results
- **Evaluation Metric**: RMSE (Root Mean Squared Error).  
- **Achieved RMSE**: Approximately **19085**.  
The model demonstrated good predictive performance, provided that the data were properly prepared.

---

## Summary
The project involves building a regression model to predict car prices. Through meticulous data preparation, thorough analysis, and the application of advanced modeling techniques (including XGBoost with hyperparameter tuning), competitive results were achieved. The project serves as a practical example of how machine learning can be applied to analyze the automotive market.

---

## Authors
- __Łukasz Podoba__  
- __Bartosz Paszko__

_Prepared as part of the Data Science Club PJATK project – March 2025._
