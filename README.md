# WokBites - AI-Powered Recipe Recommendation System

An intelligent recipe recommendation platform that leverages multiple collaborative filtering techniques to deliver personalized recipe suggestions based on user preferences and taste profiles.

## 🎯 Overview

WokBites is a machine learning-powered web application built with Flask that provides personalized recipe recommendations using hybrid recommendation algorithms. The system analyzes user preferences through an interactive quiz interface and delivers tailored recipe suggestions using collaborative filtering, content-based filtering, and matrix factorization techniques.

## ✨ Key Features

### Multi-Algorithm Recommendation Engine
- **User-Based Collaborative Filtering**: Finds users with similar taste profiles and recommends recipes they enjoyed
- **Item-Based Collaborative Filtering**: Suggests recipes similar to ones you've liked using cosine similarity
- **Matrix Factorization (SVD)**: Employs Truncated SVD for latent factor analysis to uncover hidden patterns in user preferences
- **Hybrid Recommendations**: Combines multiple algorithms to provide diverse, high-quality suggestions
- **Category-Based Discovery**: Browse recipes within specific cuisine categories

### Interactive User Experience
- **Personalized Quiz**: Interactive interface to capture user taste preferences
- **Popular Recipes**: Curated selection of trending and highly-rated recipes
- **Tastebreaker Mode**: Discover recipes outside your comfort zone with opposite recommendations
- **Visual Recipe Cards**: Recipe images fetched and displayed for enhanced browsing experience

### Smart Filtering
- Excludes already-tried recipes from recommendations
- Rating threshold filtering (default: 4+ stars)
- Duplicate removal across recommendation sources
- Random sampling for variety in each session

## 🛠️ Technical Architecture

### Backend Stack
- **Framework**: Flask 1.0.2
- **Data Processing**: Pandas, NumPy
- **Machine Learning**: Scikit-learn 0.21.0, SciPy 1.2.1
- **Algorithms**: 
  - K-Nearest Neighbors for user-user similarity
  - Cosine similarity for item-item recommendations
  - Truncated SVD for dimensionality reduction and matrix factorization

### Data Pipeline
- **Web Scraping**: BeautifulSoup4 for recipe data collection from AllRecipes.com
- **Data Storage**: CSV-based storage for recipes, users, ratings, and photo URLs
- **Preprocessing**: Pickled sparse matrices and similarity matrices for fast inference

### Frontend
- **HTML/CSS/JavaScript**: Responsive web interface
- **Template Engine**: Jinja2 (Flask templates)
- **Styling**: Custom CSS with pretty-checkbox library

## 📊 Dataset

The application uses scraped recipe data including:
- **Recipes**: 50,000+ recipes with titles, categories, ingredients, nutritional info
- **User Ratings**: Collaborative filtering dataset with ratings (1-5 scale)
- **Photo URLs**: Recipe images for visual presentation
- **Categories**: Multi-label classification with cuisine types, meal types, and ingredients

## 🚀 Getting Started

### Prerequisites
```bash
Python 3.6+
pip
```

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/Recipie-Recommender-main.git
cd Recipie-Recommender-main
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the application:
```bash
python app.py
```

4. Access the web interface:
```
http://localhost:5000
```

### Deployment

The application is configured for deployment on Heroku:
- `Procfile` included for web dyno configuration
- `runtime.txt` specifies Python version
- Gunicorn WSGI server for production

## 🧮 Recommendation Algorithms

### 1. User-User Collaborative Filtering
```python
recommenders.user_user_recommender(top_N=30, user_id=user_id, threshold=4)
```
- Computes cosine similarity between users based on rating patterns
- Identifies top-N most similar users
- Recommends highly-rated recipes from similar users' profiles

### 2. Item-Item Collaborative Filtering
```python
recommenders.item_item_recommender(title="Recipe Name", top_N=10)
```
- Pre-computed cosine similarity matrix between recipes based on categories
- Returns recipes with highest similarity scores
- Supports "opposite mode" for discovery of contrasting recipes

### 3. SVD Matrix Factorization
```python
recommenders.svd_recommender(user_id=user_id, threshold=3)
```
- Decomposes user-item rating matrix into lower-dimensional latent factors
- 100-component truncated SVD for dimensionality reduction
- Predicts ratings for unseen recipes and ranks them

### 4. Hybrid Approach
Combines outputs from multiple algorithms, removes duplicates, filters out tried recipes, and samples top recommendations for diversity.

## 📈 Model Performance

The system includes evaluation metrics:
- **RMSE**: Root Mean Square Error for rating prediction accuracy
- **Precision@K**: Fraction of recommended items the user consumed
- **Recall@K**: Fraction of consumed items that were recommended
- Baseline comparison against naive model

## 🗂️ Project Structure

```
Recipie-Recommender-main/
├── app.py                  # Flask application and routing
├── model.py               # Recommendation algorithms and utilities
├── web_scraper.py         # Data collection scripts
├── requirements.txt       # Python dependencies
├── Procfile              # Heroku deployment config
├── runtime.txt           # Python version specification
├── data/
│   ├── recipes/          # Recipe metadata CSV
│   ├── users/            # User ratings CSV
│   └── photo_url/        # Recipe image URLs
├── pickle/
│   ├── cosine_sim.pkl    # Pre-computed similarity matrix
│   └── users3.pkl        # Filtered user data
├── templates/            # HTML templates
│   ├── quiz.html         # Landing page with quiz
│   ├── result.html       # Recommendation results
│   ├── signup.html       # User registration
│   └── about.html        # About page
└── static/
    ├── images/           # Static image assets
    └── stylesheets/      # CSS styling
```

## 🔍 Features Deep Dive

### New User Handling
Creates temporary user profile (ID: 8888888) based on quiz responses:
- All selected recipes rated as 5/5
- Integrated into collaborative filtering without database persistence
- Enables immediate personalized recommendations

### Category Exploration
Multi-label category system allows:
- Browsing by cuisine type (Italian, Chinese, Mexican, etc.)
- Meal type filtering (Breakfast, Lunch, Dinner, Dessert)
- Ingredient-based discovery (Chicken, Vegetarian, Seafood)

### Tastebreaker Recommendations
Uses inverse similarity scoring to:
- Identify recipes least similar to user preferences
- Encourage culinary exploration
- Expand user taste profiles

## 🤝 Contributing

Contributions are welcome! Areas for improvement:
- Real-time learning from user feedback
- Deep learning models (Neural Collaborative Filtering)
- Recipe nutritional analysis and filtering
- Personalized dietary restriction handling
- Enhanced UI/UX with React or Vue.js
- GraphQL API for mobile applications

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Recipe data sourced from AllRecipes.com
- Inspiration from Netflix and Spotify recommendation systems
- Research papers on collaborative filtering and matrix factorization techniques

## 📧 Contact

For questions, suggestions, or collaboration opportunities, please open an issue or submit a pull request.

---

**Note**: This project was developed as a demonstration of recommendation system techniques and machine learning application in real-world scenarios. The data collection and usage comply with web scraping best practices and terms of service.
