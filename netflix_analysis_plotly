import pandas as pd
import plotly.express as px
from collections import Counter

# Load dataset
df = pd.read_csv("/Users/apple/Downloads/netflix_titles.csv")

# Clean data
df['country'].fillna("Unknown", inplace=True)
df.dropna(subset=["director", "cast"], inplace=True)

# 1. Content Type Distribution
type_counts = df['type'].value_counts().reset_index()
type_counts.columns = ['Type', 'Count']
fig1 = px.bar(type_counts, x='Type', y='Count', color='Type', title='Content Types on Netflix', text='Count')
fig1.show()

# 2. Top 10 Countries
country_counts = df['country'].value_counts().head(10).reset_index()
country_counts.columns = ['Country', 'Count']
fig2 = px.bar(country_counts, x='Country', y='Count', color='Country', title='Top 10 Countries with Most Content', text='Count')
fig2.show()

# 3. Year-wise Content Release Trend
df['date_added'] = pd.to_datetime(df['date_added'], errors='coerce')
df['year_added'] = df['date_added'].dt.year
yearly_counts = df['year_added'].value_counts().sort_index().reset_index()
yearly_counts.columns = ['Year', 'Count']
fig3 = px.line(yearly_counts, x='Year', y='Count', markers=True, title='Content Added Over the Years')
fig3.show()

# 4. Top 10 Genres
genre_series = df['listed_in'].dropna().str.split(', ')
genres = Counter([genre for sublist in genre_series for genre in sublist])
top_genres = pd.DataFrame(genres.most_common(10), columns=['Genre', 'Count'])
fig4 = px.bar(top_genres, x='Genre', y='Count', color='Genre', title='Top 10 Genres on Netflix', text='Count')
fig4.show()

# 5. Top 10 Directors
top_directors = df['director'].value_counts().head(10).reset_index()
top_directors.columns = ['Director', 'Count']
fig5 = px.bar(top_directors, x='Director', y='Count', color='Director', title='Top 10 Directors', text='Count')
fig5.show()

# 6. Most Frequent Actors
cast_series = df['cast'].dropna().str.split(', ')
actors = Counter([actor.strip() for sublist in cast_series for actor in sublist])
top_actors = pd.DataFrame(actors.most_common(10), columns=['Actor', 'Count'])
fig6 = px.bar(top_actors, x='Actor', y='Count', color='Actor', title='Most Frequent Actors on Netflix', text='Count')
fig6.show()
