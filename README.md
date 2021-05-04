# Winning Jeopardy
 Guided Dataquest project

This is a guided project done on Dataquest's platform.

The premise that I want to compete and win on Jeopardy. I'll use a dataset of Jeopardy questions to figure out some patterns in the questions that could help us win.

The dataset's name is jeopardy.csv and it contains 20,000 rowstaken from the beginning of a full dataset of Jeopardy questions that can be downloaded here: https://www.reddit.com/r/datasets/comments/1uyd0t/200000_jeopardy_questions_in_a_json_file/

If we take a closer look at our dataset, we can see that each row represents a single question on a single episode of Jeopardy.

Here is the list of columns:

Show number: the Jeopardy episode number
Air Date - the date the episode aired
Round - the round of Jeopardy
Category - the category of the question
Value - the number of dollars the correct answer is worth
Question - the text of the question
Answer - the text of the answer

I started by reading the Dataframe using Pandas and printing the first 5 rows to see a sample and the columns.

Some of the column names have spaces in front so the first step was removing the spaces from each item and assigning the result back to jeopardy.columns to fix the column names in jeopardy.

Before doing analysis on the questions, I had to normalize some of the columns:
- the text columns to make sure all words are in lowercase and remove punctuation
-  the value column to remove the dollar sign and convert it to numeric 
-  and date column, from string to date format

Data analysis:

Found out the following:
- how often the answer can be used for a question
(how many times words in the answer occur in the question)
- how often questions are repeated 
(how often complex words reoccur - words with more than 6 characters)

The answer makes up for about 6% of the question. It is a small percentage, so probably, just hearing a question will not help figuring out the answer.

I only have a part of the full Jeopardy question dataset, so I can't say for sure how often new questions are repeats of older ones. 
But to answer this question I had to sort the dataset ascending on air date, split clean_questions into words and remove any word shorter than 6 characters (this way we filter out words like the/than that are commonly used, but don't say much about the question). In a set called terms_used, I added one time each word longer than 6 characters.

I then used chi-squared test to figure out which terms correspund to high-value questions.
I used the scioy.stats.chisquare function to compute the chi_squared value and p-value given the expected and observed counts.

Chi-squared results
None of the terms had a significant difference in usage between high value and low value rows. The frequencies were all lower than 5, so the chi-squared test isn't valid. It would be better to run this test with only terms that have higher frequencies.
