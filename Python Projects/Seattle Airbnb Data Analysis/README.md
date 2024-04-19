# Introduction
The purpose of this report is to provide stakeholders with a comprehensive analysis of Airbnb activity in Seattle, leveraging a dataset encompassing listing information, reviews, time data, pricing details, and neighborhood characteristics. By delving into this dataset, I want to provide valuable insights that enable stakeholders to gain a deeper understanding of the Airbnb market dynamics in Seattle and make informed decisions. <br> <br>
In recent years, the sharing economy has significantly transformed the way people travel and seek accommodation. Airbnb, as a prominent player in this space, has emerged as a popular choice for travelers seeking unique and personalized lodging experiences. Seattle, renowned for its vibrant culture, scenic landscapes, and thriving tech industry, serves as an attractive destination for both leisure and business travelers alike. <br> <br>
Understanding the nuances of Airbnb activity in Seattle is crucial for various stakeholders, including hosts looking to optimize their listings, potential guests seeking the ideal accommodation, and policymakers interested in regulating the short-term rental market. By analyzing the provided dataset, we aim to uncover key trends, patterns, and insights that shed light on various aspects of Airbnb activity in Seattle. <br> <br>
Specifically, this report will focus on several key objectives: <br>
**1. Identifying Popular Areas:** I will analyze the distribution of Airbnb listings across different neighborhoods in Seattle to identify the most popular areas for short-term rentals. Understanding the spatial distribution of listings can help stakeholders make informed decisions regarding property investment, pricing strategies, and marketing efforts. <br>
**2. Temporal Booking Trends:** By examining temporal patterns in booking activity, I aim to identify the peak seasons and times when people are most likely to book Airbnb accommodations in Seattle. This insight can assist hosts in optimizing their availability and pricing strategies to maximize occupancy rates and revenue. <br>
**3. Price Dynamics:** Pricing plays a crucial role in the competitiveness of Airbnb listings. I will analyze the distribution of listing prices, explore factors influencing pricing decisions, and identify any temporal or spatial variations in pricing across different neighborhoods and listing types. <br>
**4. Sentimental Review Analysis:** In addition to quantitative metrics, I will delve into the qualitative aspect of guest experiences by analyzing sentiment from reviews. By identifying recurring themes, positive sentiments, and areas for improvement, stakeholders can gain valuable insights into guest preferences and expectations, enhancing their ability to provide exceptional experiences. <br> <br>
By addressing these objectives, this report seeks to empower stakeholders with actionable insights that facilitate better decision-making in the realm of Airbnb hosting, booking, and regulation in Seattle. From identifying lucrative investment opportunities to optimizing marketing strategies, the findings presented herein aim to provide tangible value to stakeholders navigating the dynamic landscape of short-term rentals in Seattle.
# Data Description
The dataset comprises three files: listings, calendar, and reviews, each offering unique insights into the Airbnb activity in Seattle. <br> <br>

**1. Listings:**
This file includes detailed information about individual listings available on Airbnb in Seattle.
Key attributes include:
id: Unique identifier for each listing.
listing_url: URL link to the listing on the Airbnb platform.
scrape_id: Identifier for the scraping process.
last_scraped: Date when the listing was last scraped from the Airbnb website.
name: Title or name of the listing.
summary: Brief summary description of the listing.
space: Detailed description of the space offered in the listing.
description: Comprehensive description of the listing.
experiences_offered: Information about experiences offered by the host.
neighborhood_over: Overview of the neighborhood where the listing is located. <br>
**2. Calendar:**
This file provides information about the availability and pricing of listings on specific dates.
Key attributes include:
listing_id: Unique identifier for each listing.
date: Date for which availability and pricing information is provided.
available: Binary indicator (True/False) denoting whether the listing is available on the specified date.
price: Price of the listing for the specified date, if available. <br>
**3. Reviews:**
This file contains reviews provided by guests who have stayed at Airbnb listings in Seattle.
Key attributes include:
listing_id: Unique identifier for the listing associated with the review.
id: Unique identifier for each review.
date: Date when the review was submitted.
reviewer_id: Unique identifier for the reviewer.
reviewer_name: Name of the reviewer.
comments: Textual comments or review provided by the guest. <br> <br>
These datasets collectively offer a comprehensive view of the Airbnb ecosystem in Seattle, allowing for in-depth analysis of listing characteristics, availability patterns, pricing dynamics, and guest experiences. Through the exploration and analysis of these datasets, stakeholders can gain valuable insights into the factors driving Airbnb activity in Seattle and make informed decisions regarding hosting, booking, and investment opportunities in the region.
# Data Preprocessing
Before I analyze the data, I preprocess the data to ensure its quality and consistency. The following steps were undertaken to prepare the Airbnb Seattle dataset for analysis: <br> <br>
**1. Removing NA Values:** I removed rows with missing values in the 'price' column using the dropna() method. This ensures that the analysis isn't influenced by incomplete data. It's essential to handle missing values appropriately, and in this case, dropping rows with missing prices ensures the integrity of the pricing analysis. <br> 
**2. Removing $ Sign from Price:** I removed the dollar sign ('$') from the 'price' column using the replace() method with a regular expression. This is a common preprocessing step for numeric columns containing currency symbols. By replacing the '$' sign with an empty string, the price values into a numeric format suitable for analysis. <br>
**3. Converting Price to Numeric:** After removing the '$' sign, I converted the 'price' column to numeric data type using pd.to_numeric(). This ensures that the 'price' values are treated as numerical values rather than strings, enabling mathematical operations and analysis.
# Data Analysis
## Pricing Trends Over Time
To understand the temporal dynamics of Airbnb pricing in Seattle, I conducted an analysis of the average price per night over the course of the year. The following steps were undertaken: <br> <br> 
**1. Converting Date to DateTime Format:** The 'date' column in the 'calendar' dataset was converted to datetime format using the pd.to_datetime() function, enabling easy manipulation and extraction of date components. <br>
**2. Extracting Month and Year:** Month and year components were extracted from the 'date' column using the dt.month and dt.year attributes, respectively. This facilitated grouping and aggregation of data based on monthly or yearly intervals. <br>
**3. Calculating Average Price per Month:** The average price per night for each month was computed by grouping the data by 'year' and 'month' and then calculating the mean of the 'price' column. This allowed us to discern trends in Airbnb pricing over the course of the year. <br>
**4. Plotting the Data:** The average price per night over the months was visualized using a line plot. This plot effectively illustrates the seasonal variations in Airbnb pricing, highlighting periods of high and low prices throughout the year. <br> <br> 
The analysis revealed that the highest average prices were observed in July, while the lowest average prices were recorded in January. This temporal analysis provides valuable insights for stakeholders, enabling them to anticipate seasonal fluctuations in pricing and adjust their strategies accordingly. The corresponding plot is presented below: <br> 
![image](https://github.com/lleavuong/Data-Analysis-Portfolio/assets/93018471/1b9a69f1-a477-408f-bff1-96880b7954ab) <br>
The plot illustrates the fluctuation of average prices per night over the course of the year, with peaks observed in July and troughs in January. These insights can inform pricing strategies for hosts and help potential guests plan their visits to Seattle more effectively. <br>

## Popular Neighborhoods
To identify the popular neighborhoods for Airbnb listings in Seattle, we employed a method that involved parsing the neighborhood information embedded within the longer description in the "neighborhood" column. As the neighborhood information was not consistently positioned within the description and varied in each row, we devised a strategy utilizing a predefined list of known neighborhoods. <br> <br>
**1. List of Known Neighborhoods:** I compiled a list of popular neighborhoods in Seattle, including 'Queen Anne', 'Capitol Hill', 'Ballard', 'Fremont', 'West Seattle', 'Downtown', 'Beacon Hill', 'Central District', 'Belltown', 'Montlake', 'Mount Baker', 'Wallingford', 'Green Lake', 'Madrona', 'Madison', 'University District', 'South Lake', and 'Eastlake'. <br>
**2. Finding Neighborhoods in Descriptions:** I developed a function, find_neighborhood(), to search for known neighborhoods within the description of each listing. This function iterates over the list of known neighborhoods and checks for their presence in the description. If a match is found (ignoring case), the respective neighborhood is assigned to a new 'Neighborhood' column. <br>
**3. Counting Listings in Each Neighborhood:** The number of listings in each neighborhood was then calculated using the newly created 'Neighborhood' column. This allowed us to quantify the popularity of each neighborhood based on the number of Airbnb listings. <br> <br> 
![image](https://github.com/lleavuong/Data-Analysis-Portfolio/assets/93018471/ff9851ea-b4ac-4925-81c5-b984d72b1dde)
The bar plot illustrates the distribution of Airbnb listings across popular neighborhoods in Seattle. Capitol Hill emerges as the most popular neighborhood, followed by Queen Anne and Ballard. This information can guide stakeholders in making informed decisions regarding property investment, pricing strategies, and marketing efforts targeted at specific neighborhoods. <br>


## Sentiment Analysis of Reviews
To gain insights into the sentiment expressed in Airbnb reviews for listings in Seattle, I conducted sentiment analysis on the textual comments provided by guests. The following steps outline our approach: <br> <br>

**1. Converting Comments to Strings:**  I converted the 'comments' column to strings to handle any NaN values and ensure consistency in data type.
Sentiment Polarity Calculation: I developed a function, get_sentiment(), using the TextBlob library, to calculate the sentiment polarity of each comment. Sentiment polarity quantifies the positivity or negativity of a text on a scale from -1 (negative) to 1 (positive), with values closer to 0 indicating neutrality. <br> 
**2. Applying Sentiment Analysis:** The sentiment function was applied to each comment in the 'comments' column, generating sentiment polarity scores for all reviews. <br>
**3. Categorizing Sentiments:**  To simplify interpretation, I categorized the sentiment polarity scores into three categories: 'Positive', 'Negative', and 'Neutral'. Comments with a polarity score greater than 0 were classified as positive, those with a score less than 0 were classified as negative, and comments with a polarity score of 0 were classified as neutral. <br> <br>
![image](https://github.com/lleavuong/Data-Analysis-Portfolio/assets/93018471/28d2cccf-18f5-4724-81d5-09efa2445df0)
The countplot illustrates the distribution of sentiments in Airbnb reviews, with the majority of reviews categorized as positive (68.39%), followed by neutral (23.48%) and negative (8.13%). This analysis provides valuable insights into the overall sentiment expressed by guests in their reviews, which can inform hosts and potential guests alike in assessing the quality and satisfaction levels associated with Airbnb listings in Seattle.


# Recommendations
Based on the insights derived from our analysis of Airbnb data in Seattle, I offer the following recommendations for stakeholders: <br> <br> 

**Pricing Strategy Optimization:**
As a host, consider utilizing the temporal pricing trends identified in our analysis to adjust your pricing strategies throughout the year. Implement dynamic pricing models that account for seasonal fluctuations in demand to maximize revenue potential during peak periods while remaining competitive during off-peak times. <br>
**Neighborhood Targeting:**
Focus your marketing efforts and investment strategies on popular neighborhoods identified in our analysis, such as Capitol Hill, Queen Anne, and Ballard. Tailor your listing descriptions and amenities to appeal to the preferences of travelers seeking accommodations in these high-demand areas. <br>
**Enhanced Guest Experience:**
Leverage insights from our sentiment analysis to improve the guest experience and satisfaction levels. Pay close attention to negative reviews and address any recurring issues or concerns raised by guests promptly. Implement measures to enhance communication, cleanliness, and overall hospitality to foster positive guest experiences. <br>
**Investment and Expansion Opportunities:**
Consider investment opportunities in emerging neighborhoods or areas with untapped potential based on our analysis of neighborhood popularity and pricing trends. Evaluate the feasibility of expanding your Airbnb offerings to cater to niche markets or address underserved segments of the traveler demographic.
<br> <br>
By implementing these recommendations, you can optimize your Airbnb hosting experience, enhance guest satisfaction, and capitalize on opportunities for growth and success in the dynamic Seattle Airbnb market. Effective implementation of these strategies will position you for long-term sustainability and success in the sharing economy landscape.

# Conclusion
In conclusion, my analysis of Airbnb data in Seattle has provided valuable insights into pricing trends, neighborhood popularity, and guest sentiments. By identifying seasonal fluctuations in pricing and the popularity of certain neighborhoods, I have equipped hosts with the knowledge needed to optimize their pricing strategies and target high-demand areas. Additionally, sentiment analysis of guest reviews has highlighted opportunities for enhancing the guest experience and improving overall satisfaction. Moving forward, I recommend hosts leverage these insights to make data-driven decisions that drive success in the competitive Seattle Airbnb market.
