# Movies

Below is my code for Deliverable 3
For some reason this jupyter notebook files did not add to the git hub repo. I had problems with this challenge and module from the start. The directions were very difficult to follow and there was so much information that I had a hard time keeping names of data sets, dfs, etc. straight. I copied things right from the module and was still unable to get them to run. I feel this is one of the most important of all the skills in the course, but there was just way too much to absorb in this module. I know this challenge is imcomplete and incorrect, but I got help from tutors, office hours and learning assistants in the process. In the end, I just have to cut my losses and move on to Module 9. Please give me feedback that will help me get on track and I will revisit this in the coming weeks when I have time. 

I could not include the data sets in a resources file as the CSV file included is much too large and will not upload. I was told by TAs and instructors that graders have the files and it is not a problem, however, it did create a problem with my repo. 

Thank you. 


import json
import pandas as pd
import numpy as np

import re

from sqlalchemy import create_engine
import psycopg2

# from config import db_password

import time
  Add the clean movie function that takes in the argument, "movie".
def clean_movie(movie):

    
    
    
# 1 Add the function that takes in three arguments;
# Wikipedia data, Kaggle metadata, and MovieLens rating data (from Kaggle)

def  1. Create a function that takes in three arguments;
# Wikipedia data, Kaggle metadata, and MovieLens rating data (from Kaggle)

def  extract_transform_load(Wikipedia_data, kaggle_metadata, movieLens_rating_data):
    #Read in the kaggle metadata and MovieLens ratings CSV files as Pandas DataFrames.
    kaggle_metadata = pd.read_csv(kaggle_metadata, low_memory=False)
    ratings = pd.read_csv(movieLens_rating_data)

    #Open the read the Wikipedia data JSON file.
    with open(Wikipedia_data, mode='r') as file:
        # Read in the raw wiki movie data as a Pandas DataFrame.
        wiki_movies_df = json.load(file) 
        wiki_movies_df = pd.DataFrame(wiki_movies_df)
        
    # Return the three DataFrames
    return wiki_movies_df, kaggle_metadata, ratings

# Create the path to your file directory and variables for the three files. 
file_dir = file_dir = "Resources/"
# Wikipedia data
wiki_file = f'{file_dir}wikipedia-movies.json'
# Kaggle metadata
kaggle_file = f'{file_dir}movies_metadata.csv'
# MovieLens rating data.
ratings_file = f'{file_dir}ratings.csv'

#Set the three variables in Step 6 equal to the function created in Step 1.
wiki_file, kaggle_file, ratings_file = extract_transform_load(wiki_file, kaggle_file, ratings_file)
    # Write a list comprehension to filter out TV shows.
     wiki_movies = [movie for movie in wiki_movies_raw
               if 'No. of episodes' not in movie]
    # Write a list comprehension to iterate through the cleaned wiki movies list
    # and call the clean_movie function on each movie.
     clean_movies = [clean_movie(movie) for movie in wiki_movies]
    

    # Read in the cleaned movies list from Step 4 as a DataFrame.
     wiki_movies_df = pd.DataFrame(clean_movies)

    # Write a try-except block to catch errors while extracting the IMDb ID using a regular expression string and
    #  dropping any imdb_id duplicates. If there is an error, capture and print the exception.
#     try:
        
#     except 

    #  Write a list comprehension to keep the columns that don't have null values from the wiki_movies_df DataFrame.
        wiki_columns_to_keep = [column for column in wiki_movies_df.columns if wiki_movies_df[column].isnull().sum() < len(wiki_movies_df) * 0.9]
        wiki_movies_df = wiki_movies_df[wiki_columns_to_keep]

    # Create a variable that will hold the non-null values from the “Box office” column.
        box_office = wiki_movies_df['Box office'].dropna()
    
    # Convert the box office data created in Step 8 to string values using the lambda and join functions.
         box_office[box_office.map(lambda x: type(x) != str)]

    # Write a regular expression to match the six elements of "form_one" of the box office data.
        form_one = r'\$\d+\.?\d*\s*[mb]illion'
        # Write a regular expression to match the three elements of "form_two" of the box office data.
        form_two = r'\$\d{1,3}(?:,\d{3})+'

    # Add the parse_dollars function.
        form_two = r'\$\d{1,3}(?:,\d{3})+'

    # if input is of the form $###.# billion
        elif re.match(r'\$\s*\d+\.?\d*\s*billi?on', s, flags=re.IGNORECASE):

        # remove dollar sign and " billion"
        s = re.sub('\$|\s|[a-zA-Z]','', s)

        # convert to float and multiply by a billion
        value = float(s) * 10**9

        # return value
        return value
     # if input is of the form $###,###,###
        elif re.match(r'\$\s*\d{1,3}(?:[,\.]\d{3})+(?!\s[mb]illion)', s, flags=re.IGNORECASE):

        # remove dollar sign and commas
        s = re.sub('\$|,','', s)

        # convert to float
        value = float(s)

        # return value
        return value
    
    # otherwise, return NaN
        else:
        return np.nan
        
    # Clean the box office column in the wiki_movies_df DataFrame.
    wiki_movies_df['box_office'] = box_office.str.extract(f'({form_one}|{form_two})', flags=re.IGNORECASE)[0].apply(parse_dollars)
    
    # Clean the budget column in the wiki_movies_df DataFrame.
    budget = wiki_movies_df['Budget'].dropna()
    budget = budget.map(lambda x: ' '.join(x) if type(x) == list else x)
    budget = budget.str.replace(r'\$.*[-—–](?![a-z])', '$', regex=True)
    matches_form_one = budget.str.contains(form_one, flags=re.IGNORECASE, na=False)
    matches_form_two = budget.str.contains(form_two, flags=re.IGNORECASE, na=False)
    budget[~matches_form_one & ~matches_form_two]

    # Clean the release date column in the wiki_movies_df DataFrame.
    release_date = wiki_movies_df['Release date'].dropna().apply(lambda x: ' '.join(x) if type(x) == list else x)
    wiki_movies_df['release_date'] = pd.to_datetime(release_date.str.extract(f'({date_form_one}|{date_form_two}|{date_form_three}|{date_form_four})')[0], infer_datetime_format=True)

    # Clean the running time column in the wiki_movies_df DataFrame.
    running_time = wiki_movies_df['Running time'].dropna().apply(lambda x: ' '.join(x) if type(x) == list else x)
    running_time.str.contains(r'^\d*\s*m', flags=re.IGNORECASE, na=False).sum()
     
    # 2. Clean the Kaggle metadata.
    kaggle_metadata[~kaggle_metadata['adult'].isin(['True','False'])]
    kaggle_metadata['video'] = kaggle_metadata['video'] == 'True'
    kaggle_metadata['budget'] = kaggle_metadata['budget'].astype(int)
    kaggle_metadata['id'] = pd.to_numeric(kaggle_metadata['id'], errors='raise')
    kaggle_metadata['popularity'] = pd.to_numeric(kaggle_metadata['popularity'], errors='raise')
    kaggle_metadata['release_date'] = pd.to_datetime(kaggle_metadata['release_date'])
    ratings['timestamp'] = pd.to_datetime(ratings['timestamp'], unit='s')

    # 3. Merged the two DataFrames into the movies DataFrame.
   movies_df = pd.merge(wiki_movies_df, kaggle_metadata, on='imdb_id', suffixes=['_wiki','_kaggle']) 


    # 4. Drop unnecessary columns from the merged DataFrame.
    movies_df.drop(columns=['title_wiki','release_date_wiki','Language','Production company(s)'], inplace=True)

    # 5. Add in the function to fill in the missing Kaggle data.
    def fill_missing_kaggle_data(df, kaggle_column, wiki_column):
    df[kaggle_column] = df.apply(
        lambda row: row[wiki_column] if row[kaggle_column] == 0 else row[kaggle_column]
        , axis=1)
    df.drop(columns=wiki_column, inplace=True)

    # 6. Call the function in Step 5 with the DataFrame and columns as the arguments.
    fill_missing_kaggle_data(movies_df, 'runtime', 'running_time')
    fill_missing_kaggle_data(movies_df, 'budget_kaggle', 'budget_wiki')
    fill_missing_kaggle_data(movies_df, 'revenue', 'box_office')
    movies_df

    # 7. Filter the movies DataFrame for specific columns.
    


    # 8. Rename the columns in the movies DataFrame.
    movies_df = movies_df.loc[:, ['imdb_id','id','title_kaggle','original_title','tagline','belongs_to_collection','url','imdb_link',
                       'runtime','budget_kaggle','revenue','release_date_kaggle','popularity','vote_average','vote_count',
                       'genres','original_language','overview','spoken_languages','Country',
                       'production_companies','production_countries','Distributor',
                       'Producer(s)','Director','Starring','Cinematography','Editor(s)','Writer(s)','Composer(s)','Based on'
                      ]]


    # 9. Transform and merge the ratings DataFrame.
    
    return wiki_movies_df, movies_with_ratings_df, movies_df
# 10. Create the path to your file directory and variables for the three files.
file_dir = '../Resources'
# The Wikipedia data
wiki_file = f'{file_dir}/wikipedia_movies.json'
# The Kaggle metadata
kaggle_file = f'{file_dir}/movies_metadata.csv'
# The MovieLens rating data.
ratings_file = f'{file_dir}/ratings.csv'
# 11. Set the three variables equal to the function created in D1.
wiki_file, kaggle_file, ratings_file = extract_transform_load()

# 12. Set the DataFrames from the return statement equal to the file names in Step 11. 
wiki_movies_df = wiki_file
movies_with_ratings_df = kaggle_file
movies_df = ratings_file

# 13. Check the wiki_movies_df DataFrame. 
wiki_movies_df.head()
# 14. Check the movies_with_ratings_df DataFrame.
movies_with_ratings_df.head()

# 15. Check the movies_df DataFrame. 
movies_df.head()


