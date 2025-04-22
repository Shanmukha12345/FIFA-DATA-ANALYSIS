# FIFA-DATA-ANALYSIS
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
df = pd.read_csv("E:\\python program\\dataset-rankings-1966-2018.csv")

# Add average goals scored per match
df["avgGoalsScored"] = df["goalsScored"] / df["matchs"]

# Points Over Seasons (Line Plot)
top_teams = ["JUVENTUS", "ROMA", "NAPOLI"]
df_top_teams = df[df["team"].isin(top_teams)]

plt.figure(figsize=(12, 6))
for team in top_teams:
    team_data = df_top_teams[df_top_teams["team"] == team]
    plt.plot(team_data["season"], team_data["points"], marker='o', label=team)

plt.xticks(rotation=90)
plt.title("Points Over Seasons - Top Teams")
plt.xlabel("Season")
plt.ylabel("Points")
plt.legend()
plt.tight_layout()
plt.grid(True)
plt.show()

# Correlation Heatmap
correlation_matrix = df.corr(numeric_only=True)

plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True, cmap="coolwarm", fmt=".2f")
plt.title("Correlation Heatmap of Metrics")
plt.show()
