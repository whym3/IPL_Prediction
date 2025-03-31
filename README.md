# IPL Match Prediction System

This repository contains a Python-based system for predicting the outcome of Indian Premier League (IPL) matches using historical data stored in an SQLite database and leveraging statistical analysis. The system extracts detailed team-level and player-level features from IPL match data and uses them to generate predictions. Optionally, it integrates with an LLM (e.g., OpenAI's GPT-4o) to provide detailed reasoning and verdicts based on the extracted features.

## Features

- **Database Creation**: Processes IPL match data from JSON files into an SQLite database (`ipl_data.db`) with tables for matches, players, and ball-by-ball statistics.
- **Team Name Normalization**: Updates team names (e.g., "Delhi Daredevils" to "Delhi Capitals") to reflect current IPL franchises.
- **Feature Extraction**: Calculates comprehensive statistics including:
  - Team-level: win rates, recent form, average runs, wickets taken, venue performance, chasing success, powerplay, and death over runs.
  - Player-level: total runs, strike rates, wickets taken, and economy rates for current roster players.
- **Prediction**: Provides a framework for match outcome prediction, with an optional LLM integration for detailed analysis.
- **User Interaction**: Allows users to select teams and view predictions via a command-line interface.

## Prerequisites

- **Python 3.6+**
- **Required Libraries**:
  - `sqlite3` (built-in)
  - `json` (built-in)
  - `os` (built-in)
  - `datetime` (built-in)
  - `openai` (optional, for LLM integration; install via `pip install openai`)

## Setup

1. **Clone the Repository**:
   ```bash
   cd ipl-match-prediction
   ```

2. **Install Dependencies**:
   If using the LLM integration, install the `openai` library:
   ```bash
   pip install openai
   ```

3. **Prepare IPL Data**:
   - Place your IPL JSON data files in a folder named `ipl_json` within the project directory. These files should contain match details in the format expected by the code (e.g., `info`, `innings`, etc.).
   - Run the initial script to create the SQLite database:
     ```bash
     python create_database.py
     ```
     Replace `create_database.py` with the actual filename if you split the notebook into separate scripts.

4. **Set Up OpenAI API (Optional)**:
   - If using LLM predictions, set your OpenAI API key as an environment variable:
     ```bash
     export OPENAI_API_KEY='your-api-key-here'
     ```
     Alternatively, replace `os.getenv("OPENAI_API_KEY")` in the code with your key directly.

## Usage

1. **Run the Prediction System**:
   Execute the main script (e.g., `predict_match.py` if you save it as a separate file):
   ```bash
   python predict_match.py
   ```

2. **Select Teams**:
   - The system lists available teams with numbers (e.g., 1. Chennai Super Kings).
   - Enter the numbers corresponding to the two teams you want to analyze.

3. **View Output**:
   - The system extracts features and displays them in a formatted prompt.
   - If LLM integration is enabled, it provides a detailed prediction with reasoning. Otherwise, it shows a placeholder prediction.

### Example Output
```
Available Teams:
1. Chennai Super Kings
2. Delhi Capitals
...

Select Team 1 (number): 1
Select Team 2 (number): 2

Prompt sent to LLM:
Match between Chennai Super Kings and Delhi Capitals:
team1: Chennai Super Kings
team2: Delhi Capitals
...

Prediction:
Based on the data, Chennai Super Kings have a higher win rate and better head-to-head performance...
Final Verdict: Chennai Super Kings are predicted to win.
```

## Project Structure

- **`ipl_json/`**: Directory containing IPL match JSON files (not included in the repo; add your own).
- **`ipl_data.db`**: SQLite database generated from JSON data.
- **`create_database.py`**: Script to create and populate the database (extract from notebook cell 1-4).
- **`predict_match.py`**: Main script for feature extraction and prediction (extract from notebook cell 5-7).
- **`README.md`**: This file.

## Data Schema

- **matches**: Stores match-level data (e.g., `match_id`, `date`, `team1`, `team2`, `winner`).
- **players**: Links players to teams and matches (e.g., `player_id`, `name`, `team`, `match_id`).
- **ball_by_ball**: Detailed ball-by-ball records (e.g., `match_id`, `batter`, `bowler`, `runs_total`, `wicket`).

## Customization

- **Add More Features**: Modify `extract_features()` to include additional statistics (e.g., player form, weather conditions).
- **Change LLM Model**: Update `get_prediction_from_llm()` to use a different model or provider.
- **Team Rosters**: Update `ipl_teams_2025` dictionary with the latest player lists.

## Limitations

- Requires IPL JSON data, which is not provided in this repo.
- Player-level stats are limited to the 2025 roster defined in the code.
- Predictions without LLM are placeholders; full predictive modeling requires additional implementation (e.g., machine learning).
- Assumes consistent JSON data structure; variations may cause errors.

## Contributing

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -m 'Add your feature'`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Data processing inspired by IPL historical records.
- LLM integration powered by OpenAI's GPT-4o model.
