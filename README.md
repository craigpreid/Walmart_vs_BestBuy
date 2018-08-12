# Best Buy -- Walmart Comparison
##### Team Members

Thanu Thavasi Perumal
Sangeetha Kamalakkannan
Phil Sohn
David Cruz
Khaled Karman
Craig Reid

##### Project Description/Outline

Objective : We will use Vendor’s API to access product and review data.  We will clean the raw data into workable dataframes and will examine the scope of data provide and attempt to answer commercially relevant questions about the online businesses we are investigating.

Limitations and challenges: We acknowledge that, while we have some access to product data, we do not have access to marketing and sales information.  This prevents us from answering the most salient questions such as, "What drives sales."  To overcome this limitation, we will look for proxy data or substitute comparisons between data sets which demonstrate the ability to answer more important questions if our team had access to the data.

##### Hypotheses

- We can use publicly available information to infer commercial success
- We can develop insights into brick and mortar v. online businesses
- Walmart & Best Buy prices will converge when each sells the same product online
- We will recognize a pattern, either higher or lower between price and number of reviews
- There will be a correlation between number of review and quality of reviews for each product

##### Research Questions to Answer

- Comparison of product offerings in common categories

- Size and scope of datasets
- Price comparison and geographical location of stores
- Analysis of reviews
- Differences/commonalities in assessment of common products
- Look at price and store locations and determine which of those variables might be more significant for the survival of the companies
- We anticipate modify the scope of research once we have more familiarity with the data

##### Data Sets to be Used

Walmart API
Best Buy API

##### Code Overview (description by file)

**0.1a Walmart_Search_Attempt1**.ipynb

- Uses Walmart API to do execute a search for product by keyword
- Walmart has over 20,000 laptops, for example, because it also has a marketplace like Amazon
- There is a limitation of 1000 items using Walmarts paginated search
- We got around this by using a loop that starts pricing at the lowest price item and stops at the highest price
- Appends each page of results to a json file
- We abandoned this method because we could not consistently get a json file that we can read

**0.1b_BestBuy_Search_Attempt1**.ipynb

- This uses the product category code from Best Buy to do a product lookup
- You must obtain the product category code manually from the the developer portal
- This returns effective search results as the json is structured and can be appended and read easily
- json from Best Buy is appended to a dictionary.
- Output is a single csv file build from dataframe and appended json**** 

**1_Product_Search.ipynb**

- This code base combines product search from Walmart and Best Buy. Early versions were developed separately.


**Purpose of Code:**

- Search product buy keyword (e.g. laptop) at Best Buy and Walmart
- Allow programmer to select the product parameters to store
- Return a complete list of all products within the query
- Rename the product parameters to a common columns names
- Run a regular expression loop to pull out screensize and store in a column
- Write results to a csv file (or json in earlier iterations of the code)
- Saves search results to the following folders:
  - Walmart_datasets
  - BestBuy_datasets

**Problems Solved:**

- Best Buy allows you to download and store entire product database. Walmart does not
- Complete Product Inventory for Walmart.
  - Walmart has a much larger product inventory per category in several areas.
  - For example, 20,000 laptops with a limit of 1000 for paginated search
  - We got around this by running a loop to search the entire price range and append results to a file
- Walmart json not formated properly
  - When you append successive searches in Walmart, the json is not structured properly to read back into a dataframe
  - This method overcomes that issue by saving each search in a separate csv file, then combining
- Product information missing, for example screen size of TVs
  - This method contains regular expression to capture screen size



**2_Product_Comparison.ipynb**

The purpose of this section is to determine whether we can find a proxy for commercial activity.  In this case we will use reviews. First, we compare common products within product categories, like laptops, TVs, etc.  Then we look at all of the product categories and in order to understand the data within each category as whole and try to understand the commercial activity within each category.

Since we do not have sales data, we will use number of review to represent an indicator of commercial activity

***Hypotheses***

1. Greater number of reviews will mean systematically lower prices If true, our thought is that this is because the company is using some sort of promotion (which this app cannot see). Lower price would be part of the promotion
2. For similar reason, we do not expect to see many both companies have a high number of reviews for products with less brand power such as laptops. Best Buy and Walmart will be selling different products in similar catoegories
3. Conversely, when we inspect products with greater brand power such as the iPhone we do expect to see high numbers of reviews for both retailers

##### Operations

- Open csv files form Walmart_datasets and BestBuy_datasets into dataframes
- Creates a single dataframe with a center join on UPC.  This shows only the upc codes found in both sites, i.e. both sites are selling these products
- Plots the following for common products:
  - Number of common products
  - Number of reviews per product category
  - Quality of reviews per product category
  - Avg. price per product category
  - Scatterplot: reviews v. price difference
  - Scatterplot: quality of reviews v. price difference
  - Scatterplot: review avg. v. number of reviews

##### 3_Location_Analysis.ipynb

- Pull latitude, longitude of all Walmart Best Buy stores, supercenters, etc. in California
- Plot location of Walmart and Best Buy locations using Google Maps
- Find the number of stores per metro area in the Bay Area for Walmart and Best Buy
- Compare number of stores to median income (from US Census) by metro area