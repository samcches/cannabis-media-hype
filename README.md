# Cannabis Stock Prices and Media Hype
## Deep Learning Projecting Utilizing NLTK and Time Series Analysis

This project focuses on four major cannabis stocks: Tilray, Inc. (TLRY), Canopy Growth Corporation (CGC), Aurora Cannabis, Inc (ACB), and Cronos Group (CRON), and the effects media hype has had on their stock price fluctuations.

### Introduction 
Cannabis stocks have for a few years now been hyped up as the new "tech stocks", promising to be to current investors what Apple and Microsoft were decades ago. With marijuana fully legalized in Canada, and fully legal status or reduced decriminalization in thirty-seven of the United States, many investors jumped onboard in 2018 when major cannabis companies, some believing in the product, others believing in the profit.
As the demand for the stocks increased, certain stocks saw near-exponential growth, to the wonder and admiration of investors and analysts alike. But how much of that growth was a natural reflection on the product and how much was artificially inflated hype?

### Step 1: Source Data from NASDAQ + Preprocessing
The first step was to source the historical data from NASDAQ. Luckily, the information is stored in a csv file and requires minimal preprocessing. The only cleaning required was a removal of extra spaces in the name and a reordering of the prices with the oldest date first.

### Step 2: Time Series Analysis
Our next step was to convert the date columns for each stock to datetime format and set it as the index column. Then we needed to strip the dollar sign from the price and convert the prices to numeric type rather than string. Each stock was then graphed as a candlestick plot, then converted to pandas Series to be tested for stationarity and seasonality.

Each stock was next decomposed so that the seasonality, residuals and trend were removed from the original, and decomposed stationarity viewed. Cronos Group (CRON) lacked enough data to be of any practical use, and was henceforth dropped from the study. Aurora Cannabis (ACB) and Canopy Growth Corporation (CGC) showed a good level of stationarity, while Tilry, Inc. (TLRY) showed some initial irregularities.

Each of the three stocks were then tested for both autocorrelation and partial autocorrelation. While ACB and CGC both showed high autocorrelation, indicating that past prices were good indicators of future growth, TLRY did not.

SARIMAX modeling further indicated that both ACB and CGC showed regular fluctuations and growth, while TLRY showed inconsistencies. For these reasons, TLRY alone was chosen as an ideal candidate for analysis of artificial price fluctuations due to media hype.

### Step 3: Scraping Data From News Articles
Ideally, we'd like to use an API, like News API, for this sort of bulk scraping. However, News API's free version does not allow scraping further back than a month and we're looking for a specific date-range: the first three months of TLRY's launch on the New York Stock Exchange, and the month before. As this is scraping these dates is impossible using the API, we used requests and Google News search results to scrape articles, which were then parsed using BeautifulSoup.

The adjectives were then isolated from each article using nltk.corpus, and used and classified as either having a positive sentiment or negative sentiment usiing nltk.opinion_lexicon. 

### Step 4: Putting It All Together
Each article was then graphed as a specific color based on percentage of positivity. This underlaid an excerpt of the trend line from our previous decomposition that matched the date-range of the articles we scraped. Prior to TLRY's launch on the NYSE, the sentiment around it was overwhelmingly positive. Even after TLRY's growth slowed and began to fall, sentiment remained high with only a few voices speaking negatively of the stock.

### Conclusion
Although we cannot be certain whether the sentiment caused the decline by influencing share-holders, August's growth was certainly met by positive write-ups. The lesson here for investors and financial writers alike, is not to fall victim to growth driven solely by animal spirits. Such growth is artificial and extremely tricky to short-sell profitably.

### Further Research
- Extending the sentiment analysis to the life of all four stocks included in the first half of the project (TLRY, ACB, CGC, CRON)
- Expand the sentiment analysis to adverbs and verb as well as adjectives.
- Predict future prices and use sentiment analysis classifier to predict the weight of influence or how long the influence lasts after initial stock launch