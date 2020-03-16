# Databasing for & Applying Analytics to a Presidential Campaign
Code and reports about creating a database for a presidential campaign as well as performing advanced analytics on the obtained information.

# Database development README:
## NYT Archive API
### February:
  - Gets the API data for all articles published in February and saves to NYT_feb_data.txt
      - This data is in JSON format
  - Generates list of all URLs since we want articles from all of February
  - Navigates to each URL and saves html with “article” + index position

### March:
  - Gets the API data for all articles published in March and saves to NYT_march_data.txt
      - This data is in JSON format
  - Generates list of all URLs from before Super Tuesday (March 3rd)
  - Resaves the API data for all March docs before Super Tuesday to NYT_march_data_2.txt
  - Navigates to each URL and saves html with “article” + index position

## NYT Article Text
  - Reads in the html files and joins the complete article text for each article into one large paragraph
  - Adds article text for each article into a list
  - Saves list to a text file, with elements separated by a new line character
      - For February, saves into feb_article_text.txt
      - For March, saves into march_article_text.txt
  - Creates dictionary with article_id as key and article_text as value
  - Searches through each article for at least one occurrence of mentioning either Bernie Sanders or Joe Biden
      - Bernie Sanders is often referred to in many ways: Bernie, Mr. Sanders, or Senator Sanders
          - Since Sanders is a common last name, does not search for just “Sanders”. I looked at the difference between including just “Sanders” vs not and it is approximately 30 articles
      - Joe Biden is pretty much never referred to by his first name, and Biden is a much less common last name, so just “Biden” is searched for
  - Keeps only key-value pairs of articles where the article mentions one of these 2 candidates, to cut down on data storage needs
  - Saves these dictionaries to JSON file so that in order to push into MongoDB you should only need these smaller JSON files
      - For February, saves dictionary into feb_dict.json
      - For March, saves dictionary into march_dict.json

## Delegate Count Scraping
  - Navigates to New York Times article that has counts of delegate wins in each primary state for Joe Biden and Bernie Sanders
  - Gets from table state name, number of delegates that went to Biden, number of delegates that went to Sanders, and if Biden or Sanders were officially declared the “winner” of the state
  - Converts this information into a dictionary for easy input into MongoDB
  
## Campaign Contributions
  - Uses downloaded csv of all individual contributions to candidates running for 2020 Presidential candidacy from the FEC
  - Converts csv file to dictionary for easy import into MongoDB

