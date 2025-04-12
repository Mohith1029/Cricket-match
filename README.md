# Cricket-match
# Import required libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load datasets
matches = pd.read_csv('matches.csv')
deliveries = pd.read_csv('deliveries.csv')

# 1. Overview of matches
print("Total Seasons:", matches['season'].nunique())
print("Total Matches:", matches.shape[0])
print(matches.head())

# 2. Most successful teams
most_wins = matches['winner'].value_counts().head(5)
most_wins.plot(kind='bar', color='teal', figsize=(8, 5))
plt.title("Top 5 Most Successful IPL Teams")
plt.xlabel("Team")
plt.ylabel("Wins")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 3. Toss decision analysis
toss_decisions = matches['toss_decision'].value_counts()
toss_decisions.plot(kind='pie', autopct='%1.1f%%', startangle=90, shadow=True, colors=['orange', 'cyan'])
plt.title("Toss Decision Distribution")
plt.ylabel('')
plt.tight_layout()
plt.show()

# 4. Top run scorers
top_batsmen = deliveries.groupby('batsman')['batsman_runs'].sum().sort_values(ascending=False).head(10)
top_batsmen.plot(kind='bar', color='purple', figsize=(8, 5))
plt.title("Top 10 Run Scorers in IPL")
plt.xlabel("Batsman")
plt.ylabel("Total Runs")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 5. Most wicket-taking bowlers
wickets = deliveries[deliveries['dismissal_kind'].isin(['bowled', 'caught', 'lbw', 'stumped', 'caught and bowled'])]
top_bowlers = wickets['bowler'].value_counts().head(10)
top_bowlers.plot(kind='bar', color='darkred', figsize=(8, 5))
plt.title("Top 10 Wicket-Taking Bowlers")
plt.xlabel("Bowler")
plt.ylabel("Wickets")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 6. Winning by runs
plt.hist(matches['win_by_runs'][matches['win_by_runs'] > 0], bins=30, color='green')
plt.title("Distribution of Win by Runs")
plt.xlabel("Run Margin")
plt.ylabel("Number of Matches")
plt.tight_layout()
plt.show()

# 7. Winning by wickets
plt.hist(matches['win_by_wickets'][matches['win_by_wickets'] > 0], bins=9, color='blue')
plt.title("Distribution of Win by Wickets")
plt.xlabel("Wicket Margin")
plt.ylabel("Number of Matches")
plt.tight_layout()
plt.show()
