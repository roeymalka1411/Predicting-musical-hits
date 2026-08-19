# Predicting Musical Hits on Spotify 🎵

This project analyzes a dataset of Spotify songs to predict their commercial popularity. The primary goal is to build a machine learning pipeline that categorizes songs into popularity tiers, ultimately serving as a strategic decision-support tool for record labels and music investors looking to de-risk their portfolio.

## Table of Contents
- [About the Project](#about-the-project)
- [Dataset & Data Setup](#dataset--data-setup)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Methodology](#methodology)
- [Contributing](#contributing)
- [License](#license)

## About the Project
The music industry is highly volatile, and identifying hit songs is a key challenge. Instead of attempting to predict a precise, continuous popularity score (a noisy regression task), this project frames the problem as a **3-tier classification** (Flops, Average, Hits).

By isolating the "Hits" (Class 2) and optimizing for **Precision**, this approach is mathematically robust to market noise and perfectly aligns with the real-world business decision: *"Is this track a secure investment?"* The project features advanced data leakage prevention, custom Scikit-Learn transformers, and a strategic business layer with dynamic probability thresholds.

## Dataset & Data Setup
Due to file size limitations and version control best practices, the raw dataset is not hosted in this repository.

To run the notebook successfully **without modifying any code**, you need to download the data manually and place it in the correct directory.

### Data Setup Instructions:
1.  Download the original dataset from Kaggle: [30000 Spotify Songs Dataset](https://www.kaggle.com/datasets/joebeachcapital/30000-spotify-songs)
2.  Create a new folder named `Data` in the root directory of this cloned project.
3.  **Important:** The downloaded Kaggle dataset contains a `.csv` file. Because the notebook is configured to read an Excel file, please open the CSV and save/export it as an Excel Workbook.
4.  Rename the new Excel file to exactly: `spotify_songs_initial.xlsx`.
5.  Place this `.xlsx` file inside the `Data` folder.

### Key Features
*   **Target Variable:** `track_popularity` (Clustered via K-Means into 3 classes: 0 = Flop, 1 = Average, 2 = Hit)
*   **Audio Features:** `danceability`, `energy`, `loudness`, `speechiness`, `acousticness`, `instrumentalness`, `liveness`, `valence`, `tempo`.
*   **Metadata:** `playlist_genre`, `playlist_subgenre`, `track_artist`, `track_album_release_date`.
*   **Engineered Features:** `track_age`, Target Encoding for subgenres, and dynamic artist reach statistics (e.g., `artist_total_playlists`).

## Installation
To run this project, you'll need Python and the following libraries. You can install them using pip:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost
```

## Usage
All the analysis and modeling are contained within the Jupyter notebook. To run the project locally, follow these steps:

1.  Clone this repository:
    ```bash
    git clone https://github.com/roeymalka1411/Predicting-musical-hits.git
    ```

2.  Ensure you have the required libraries installed (see [Installation](#installation)).

3.  Follow the [Data Setup Instructions](#data-setup-instructions) above to ensure the dataset is in the correct location and format.

4.  Verify that your project structure looks exactly like this:
    ```
    .
    ├── Data/
    │   └── spotify_songs_initial.xlsx
    ├── predicting_musical_hits.ipynb
    └── README.md
    ```

5.  Open and run the `predicting_musical_hits.ipynb` notebook in a Jupyter environment. The notebook is structured to guide you through the entire process, from data loading and cleaning to EDA, modeling, and evaluation.

## Methodology
The project follows a comprehensive data science and business strategy workflow:

*   **Data Cleaning:** Handled duplicates, missing values, and transformed columns into usable formats (e.g., converting `duration_ms` to seconds).
*   **Feature Engineering:** Built custom Scikit-Learn Transformers to dynamically calculate subgenre target encodings and artist aggregation statistics without leaking training data into the validation/test sets.
*   **Exploratory Data Analysis (EDA):** Conducted extensive univariate and bivariate analysis to understand feature distributions and automatically prune noisy acoustic features.
*   **Outlier Detection:** Used the Isolation Forest algorithm to identify and handle multi-dimensional anomalies in the training data.
*   **Modeling & Business Optimization:** Evaluated Logistic Regression, K-Nearest Neighbors (KNN), and XGBoost. The final XGBoost pipeline was explicitly optimized for **Class 2 (Hits) Precision** using a custom scorer.
*   **The Strategic Layer:** Extracted Out-Of-Fold (OOF) probabilities to create a Precision-Recall tradeoff chart. This generated a "Business Investment Menu", allowing different corporate profiles (e.g., risk-averse indie labels vs. volume-focused streaming platforms) to set dynamic probability thresholds for signing tracks.

**Note:** For a deep dive into the statistical tests (e.g., ANOVA results), the rationale behind the regression-to-classification pivot, and the OOF threshold logic, please refer to the markdown documentation integrated directly within the Jupyter notebook.

## Contributing
Contributions are welcome! If you have suggestions for improving this project or adapting the model for new verticals (e.g., sports sponsorship discovery), please feel free to fork the repository and submit a pull request.
