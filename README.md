# AI-Traffic-Prediction-and-Smart-Routing-System
This is an AI ML project that that uses python and prolog to make an AI Traffic Prediction and Smart Routing System. 


*Hybrid AI Traffic Routing System*


This project combines Machine Learning and Logic Programming to predict traffic conditions and suggest optimal routes across a small road network of 5 junctions (A–E).
A Random Forest classifier is trained on a synthetic dataset of 300 samples, learning to classify traffic as High, Medium, or Low based on the hour of day and vehicle count. It achieves ~97% accuracy.
The predicted traffic level is then passed to a Prolog knowledge base, which applies rule-based logic to recommend the best route — avoiding congested edges (A↔B, B↔C) during peak hours and falling back to mid-junction routing when needed.
The system runs in two modes — a batch mode that tests 4 preset scenarios (morning rush, midday, night, evening rush), and an interactive mode where the user inputs their own junction, hour, and vehicle count to get a real-time prediction and route suggestion.
Tech used: Python, scikit-learn, pandas, SWI-Prolog, PySwip.
