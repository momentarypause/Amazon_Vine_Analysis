# Amazon_Vine_Analysis
ETL process on Amazon Vine data, connecting to an AWS RDS instance, and loading transformed data into pgAdmin. Analysis on review bias from Vine members.

## Overview
The following is an analysis of Lawn and Garden reviews made by members of Amazon Vine, a program where companies pay a fee to Amazon and send products to members who then are required to publish a review.

The ETL process and PySpark was used to extract the dataset, transform it, connect to an AWS RDS instance, and load the transformed data into pgAdmin.

PySpark was then used to determine if there is a bias toward favorable reviews made by Amazon Vine members.

### Technologies Used
	- Google Colab
	- PySpark
	- AWS RDS
	- Postgres/pgAdmin

### Extract
Pyspark was used to pull the dataset from Amazon and load it into a Spark DataFrame.
![extract](https://user-images.githubusercontent.com/102555125/192887608-470bb41a-6d57-4aae-a203-983ec310b9b3.png)


### Transform
Null values were dropped from the whole dataset.  Then, 4 dataframes were created using various grouping and filtering functions to match the schema of tables created in pgAdmin.

### Load
These tables were then loaded to pgAdmin using an AWS RDS instance.
![load](https://user-images.githubusercontent.com/102555125/192887646-c11c3bec-94c2-4b38-b9c9-9fe0fedace06.png)

The resulting tables are below:
![pgAdmin_snapshots](https://user-images.githubusercontent.com/102555125/192887700-cc81a6bd-c36a-49eb-bcad-52867f5837fe.png)

## Results
- How many Vine reviews and non-Vine reviews were there?

![totalreviews](https://user-images.githubusercontent.com/102555125/192887762-15b4bc28-bb39-4ec8-98aa-721215e055e2.png)

There were 386 reviews from Vine subscribers and 48,702 reviews from non-subscribers for a total of 49,088 reviews of Lawn and Garden items.
<br></br>
- How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?

![fivestar](https://user-images.githubusercontent.com/102555125/192887980-c851383d-36e5-4ee7-9f96-4cc0a6fc2355.png)

Vine subscribers gave 176 items 5-star reviews and non-subscribers gave 24,016 items 5-star reviews for a total of 24,192 5-star reviews.
<br></br>
- What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?

![starpercent](https://user-images.githubusercontent.com/102555125/192888038-5878457c-f924-4cae-bd5e-1827decd619b.png)

The 5-star reviews of Vine subscribers made up 45.6% of their total reviews.  The 5-star reviews of non-subscribers made up 49.3% of their total reviews.
<br></br>
## Summary
In Lawn and Garden items, Vine subscribers do not appear to have a positivity bias for reviews, in fact, non-subscribers had a higher percentage of 5-star reviews than subscribers.  However, given that Vine reviews make up less than 1% of the total reviews, this may not be a fair comparison as smaller fluctuations can sway data more drastically in smaller datasets.

Since this is the size of dataset we have, there isn't much that can be done on a product-specific level.  However, if all of the products were analyzed together in this manner, there would be more evidence of positivity bias or lack thereof in Vine subscribers.

I would also like to see the other end of the spectrum to see if there is a lack of negative reviews (1 or 2 in the star ratings).  If Vine subscribers have a significantly lower percentage of 1 or 2 star votes than non-subscribers, that may indicate sway toward positive.

The most telling analysis, though, would be to take the top 10 products in terms of number of helpful reviews, and to compare the star ratings for members and non-members.  If there is a significant difference in the same product between the 2 groups (for example: if Vine members had overwhelming positive reviews on a certain pair of gardening gloves and non-vine members scored it much lower), this may indicate bias. 
