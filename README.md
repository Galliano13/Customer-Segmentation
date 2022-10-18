# Customer-Segmentation
Applied K Means Clustering algorithm to create customer segmentation. By creating customer segmentation, we can identified the behavior of customers and create marketing campaign based on each segmentation

# Understanding the Problem Statement and Business Case

Marketing is crucial for the growth and sustainability of any business. Marketers can help build the company's brand, engage customers, grow revenue, and increase sales.One of the key pain points for marketers is to know their customers and identify their needs. By understanding the customer, marketers can launch a targeted marketing campaign that is tailored for specific needs.

In this project, we are going to perform customer segmentation based on data of the customers. By performing customer segmentation, we can identify customer needs and behaviours. In this way, we can create effective marketing campaign for customers.

# Importing Datasets

We used customer personality analysis from kaggle that contains the information of 2240 customers. The following is the first two rows of the dataset :

| ID  | Year_Birth | Education | Marital_Status | Income | Kidhome | Teenhome | Dt_Customer | Recency | MntWines | ... | NumWebVisitsMonth | AcceptedCmp3 | AcceptedCmp4 | AcceptedCmp5 | AcceptedCmp1 | AcceptedCmp2| Complain | Z_CostContact | Z_Revenue | Response |
| ------------- | ------------- | ------------ | ------------- |------------- |-------------  |------------- | ------------- |------------- |------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------ |
| 5524 | 1957 | Graduation | Single | 58138.0 | 0 | 0 | 2012-04-09 | 58 | 635 | ... | 7 | 0 | 0 | 0 | 0 | 0 | 0 | 3 | 11 | 1 |
| 2174 | 1954 | Graduation | Single | 46344.0 | 1 | 1 | 2012-08-03 | 38 | 11 | ... | 5 | 0 | 0 | 0 | 0 | 0 | 0 | 3 | 11 | 0 |

Attributes

People

- ```ID```: Customer's unique identifier

- ```Year_Birth```: Customer's birth year

- ```Education```: Customer's education level

- ```Marital_Status```: Customer's marital status

- ```Income```: Customer's yearly household income

- ```Kidhome```: Number of children in customer's household

- ```Teenhome```: Number of teenagers in customer's household

- ```Dt_Customer```: Date of customer's enrollment with the company

- ```Recency```: Number of days since customer's last purchase

- ```Complain```: 1 if the customer complained in the last 2 years, 0 otherwise
Products

- ```MntWines```: Amount spent on wine in last 2 years

- ```MntFruits```: Amount spent on fruits in last 2 years

- ```MntMeatProducts```: Amount spent on meat in last 2 years

- ```MntFishProducts```: Amount spent on fish in last 2 years

- ```MntSweetProducts```: Amount spent on sweets in last 2 years

- ```MntGoldProds```: Amount spent on gold in last 2 years

Promotion

- ```NumDealsPurchases```: Number of purchases made with a discount

- ```AcceptedCmp1```: 1 if customer accepted the offer in the 1st campaign, 0 otherwise

- ```AcceptedCmp2```: 1 if customer accepted the offer in the 2nd campaign, 0 otherwise

- ```AcceptedCmp3```: 1 if customer accepted the offer in the 3rd campaign, 0 otherwise

- ```AcceptedCmp4```: 1 if customer accepted the offer in the 4th campaign, 0 otherwise

- ```AcceptedCmp5```: 1 if customer accepted the offer in the 5th campaign, 0 otherwise

- ```Response```: 1 if customer accepted the offer in the last campaign, 0 otherwise

Place

- ```NumWebPurchases```: Number of purchases made through the company’s website

- ```NumCatalogPurchases```: Number of purchases made using a catalogue

- ```NumStorePurchases```: Number of purchases made directly in stores

- ```NumWebVisitsMonth```: Number of visits to company’s website in the last month

After importing our dataset, we should take a look for missing values in our dataset. We have 24 missing values on ```Income``` column, lets fill them up with average values on ```income``` column.

Before we do visualization of customers profile, lets make new column that contain age of the customers. The following is new dataset with age column :

| ID  | Year_Birth | Education | Marital_Status | Income | Kidhome | Teenhome | Dt_Customer | Recency | MntWines | ... | NumWebVisitsMonth | AcceptedCmp3 | AcceptedCmp4 | AcceptedCmp5 | AcceptedCmp1 | AcceptedCmp2| Complain | Z_CostContact | Z_Revenue | Response | Age |
| ------------- | ------------- | ------------ | ------------- |------------- |-------------  |------------- | ------------- |------------- |------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------ | ------------ |
| 5524 | 1957 | Graduation | Single | 58138.0 | 0 | 0 | 2012-04-09 | 58 | 635 | ... | 7 | 0 | 0 | 0 | 0 | 0 | 0 | 3 | 11 | 1 | 65 |
| 2174 | 1954 | Graduation | Single | 46344.0 | 1 | 1 | 2012-08-03 | 38 | 11 | ... | 5 | 0 | 0 | 0 | 0 | 0 | 0 | 3 | 11 | 0 | 68 |

# Customers Profile

**Customers Age**

![Age Vis 1](https://user-images.githubusercontent.com/107464383/196362335-75f1c4eb-6a39-46b5-af41-4f7e575fa08f.PNG)

![Age Vis 2](https://user-images.githubusercontent.com/107464383/196362467-91564f24-b5e0-4de2-89e2-34cdcfe544fb.PNG)

Boxplot above shows that there are huge outlier on age boxplot, we should drop it later. 

We can divide age of customer into 4 category : Young, Adult, Mature, and Senior category

![Age Vis 3](https://user-images.githubusercontent.com/107464383/196362762-a2ebdeae-a8ce-4c4f-b56c-73387dd22781.PNG)

Now we know that all of the customer is consist by 54.1% of customers falls into mature category, 25.8% of customers falls into adult category, 18.8% of customers falls into senior category, 1.25% of customers falls into young category.

**Customers Education**

![Edu Vis 1](https://user-images.githubusercontent.com/107464383/196370925-0f7cc5d3-f22d-457c-8443-8757abd66d36.PNG)

Based on chart above, the majority of customer is graduation or bachelor deegre followed by master and PhD deegre. We can divide the education of customer for our model into two categories, undergraduate and postgraduate

![Edu Vis 2](https://user-images.githubusercontent.com/107464383/196371134-60a7c201-4610-4f05-adfb-34ff1dbd20dd.PNG)

Now we know that all of the customer is consist by 88.5% of customer have postgraduate education and 11.5% of customer have undergraduate education

**Customers Marital Status**

![MS Vis 1](https://user-images.githubusercontent.com/107464383/196371482-882dd511-ca57-4927-b08e-5a09d977a054.PNG)

Based on chart above, we know that there are many marital status with absurd and YOLO being one of the marital status of the customers. Lets divide it into two categories, single and in-relationship.

![MS Vis 2](https://user-images.githubusercontent.com/107464383/196371656-9cf3ebb9-7212-420a-a871-c36d9a61ceef.PNG)

After we divide the marital status into two categories, now we know that all of the customer is consist by 64.5% of customer in relationship and 35.5% of customer are single.

**Customers Income**

![Income Vis 1](https://user-images.githubusercontent.com/107464383/196372466-8d2f95fc-0542-43d2-a4a7-9872c57c74d9.PNG)

![Income Vis 2](https://user-images.githubusercontent.com/107464383/196372514-273a1a6c-5937-41cf-a924-ea798decf536.PNG)

The plot above shows there are huge outlier in income boxplot with income on 666.666k ,we should remove it later.

We can divide the income of each customers into 4 category : low income, low to medium income, medium to high income, and high income.

![Income Vis 3](https://user-images.githubusercontent.com/107464383/196372755-b2349319-ec10-4fce-b823-75a8f31ffec0.PNG)

**Distribution of Customers by Children in Their Home**

![Kids vis](https://user-images.githubusercontent.com/107464383/196373966-0517533e-cd34-4d43-a68a-22ca33daafb8.PNG)

![Teen Vis 1](https://user-images.githubusercontent.com/107464383/196374001-800da12e-bdb9-46db-b7f8-8ed2a27febba.PNG)

Now lets combine Kidhome and Teenhome into one column. We call it 'Number of Child' column, this column contain info of the child in customer household.

![Children Vis](https://user-images.githubusercontent.com/107464383/196374224-848173f2-2f94-40d3-bfdd-9adcb6d7ff0c.PNG)

Now we know that majority of the customers have 1 children followed by 0 children and 2 children.

**Customers complain**

![Complain Vis 1](https://user-images.githubusercontent.com/107464383/196374524-de3186bc-5383-4a53-9b4b-ac08913d0692.PNG)

Pie chart above shows that 99.1% of customers never filed a complain while 0.938% of customers have filed a complain

We already take a look into our customer profile, now lets create new columns that contain information of total monthly spend,total number of campaign accepted, and total purchases

# Data Pre-processing

We drop ```Dt_Customer```, ```Kidhome```, ```Teenhome```, ```Recency```, ```ID```, ```Year_Birth```, ```Income```, ```Age```, ```Z_CostContact```, ```Z_Revenue``` columns because its unnecesary for our cluster

# Data Encoding

There are categorical data on model data, we will do ordinal encoding to give label for these columns with categorical data :
- ```Age_group``` = {'Young': 1, 'Adult': 2 , 'Mature': 3, 'Senior': 4}
- ```Education``` = {'Undergraduate': 1, 'Postgraduate': 2}
- ```Marital_Status``` = {'Single': 1, 'In-Relationship': 2}
- ```Income_group``` = {'Low income': 1, 'Low to medium income': 2, 'Medium to high income': 3, 'High income': 4}

# Data Normalization

Before we put the data into our model, we should normalize the data first.Normalization gives equal weights/importance to each variable so that no single variable steers model performance in one direction just because they are bigger numbers. We use Power Transformer to normalize the data

Before Normalization :

![Norm 1](https://user-images.githubusercontent.com/107464383/196377942-f4cd26bb-d9fb-41ca-ab07-f5359d164777.PNG)

After Normalization :

![Norm 2](https://user-images.githubusercontent.com/107464383/196378064-ed4b1e58-b292-433c-9e83-dad40d9c6dae.PNG)

# Clustering

Before we cluster our data, we should find out ideal cluster for us using Elbow Method and silhouette score for validation.

## Elbow Method

![Elbow Score](https://user-images.githubusercontent.com/107464383/196379249-059fb075-c695-4f05-bc4e-b6bf8a17d53f.PNG)

In cluster analysis, the elbow method is a heuristic used in determining the number of clusters in a data set. The vertical lines of the graph above shows that ideal cluster for our cluster is 4

## Silhouette Score

Silhouette Coefficient or silhouette score is a metric used to calculate the goodness of a clustering technique. Its value ranges from -1 to 1, each clusters are well apart from each other and clearly distinguished if silhouette score is towards 1.

![Silhouette Score](https://user-images.githubusercontent.com/107464383/196380300-0707d894-b853-42fc-92c2-12583a0fbe25.PNG)

We have bad silhouette score because our silhouette score is towards 0.

To optimize it, we can apply principal component analysis (PCA) for our cluster

# Principal Component Analysis

PCA is an unsupervised machine learning algorithm. PCA performs dimensionality reductions while attempting at keeping the original information unchanged.

![PCA 1](https://user-images.githubusercontent.com/107464383/196382496-c3ac4e49-8fcf-43ea-a67b-296281e9659b.PNG)

![PCA 2](https://user-images.githubusercontent.com/107464383/196382498-45b57c4a-5550-4ddb-b551-068986e04631.PNG)

![PCA 3](https://user-images.githubusercontent.com/107464383/196382499-81ab8a38-0866-4326-a382-447cbe9719ad.PNG)

![PCA 4](https://user-images.githubusercontent.com/107464383/196382504-1b291bec-f216-4960-b5b1-e7dbd453c81c.PNG)

![PCA 5](https://user-images.githubusercontent.com/107464383/196382507-61d1b9b9-6fbd-4608-a783-1256c23ab6d0.PNG)

![PCA 6](https://user-images.githubusercontent.com/107464383/196382512-301dfed7-75a2-48fb-9968-65b67373d044.PNG)

![PCA 7](https://user-images.githubusercontent.com/107464383/196382514-da82a792-c8a4-4d38-a71a-e256220bcdfd.PNG)

![PCA 8](https://user-images.githubusercontent.com/107464383/196382485-d5e10f97-82e7-4f26-be2f-6b113920d6ed.PNG)

We will fit PCA algorithm into our cluster and visualize it for customer segmentation

# Customer Segmentation

![Segmen 1](https://user-images.githubusercontent.com/107464383/196385495-d539ddc9-01eb-4621-afec-b1b8e54b5e2a.PNG)

![Segmen 2](https://user-images.githubusercontent.com/107464383/196385501-390bad10-5546-4729-819e-407fd37c23bc.PNG)

![Segmen 3](https://user-images.githubusercontent.com/107464383/196385505-34eac525-4b01-4eed-9cfe-dbb3e2552024.PNG)

![Segmen 4](https://user-images.githubusercontent.com/107464383/196385507-dec536f9-720b-49a2-88a8-d9595cf93afc.PNG)

![Segmen 5](https://user-images.githubusercontent.com/107464383/196385510-bb860952-9e1d-45ea-9271-ae3c80159b46.PNG)

![Segmen 6](https://user-images.githubusercontent.com/107464383/196385516-2cf8f124-a739-4805-9004-30e1a73b5a5c.PNG)

![Segmen 7](https://user-images.githubusercontent.com/107464383/196385522-24f6ad7c-3dc0-44ec-8b0b-5d003777ac5d.PNG)

![Segmen 8](https://user-images.githubusercontent.com/107464383/196385524-e988a319-7cb0-4127-8501-6568c01869c4.PNG)

![Segmen 9](https://user-images.githubusercontent.com/107464383/196385528-b72aab58-37be-4f72-8690-8eb475d6c80e.PNG)

![Segmen 10](https://user-images.githubusercontent.com/107464383/196385465-1ac16b9e-bae1-44a5-b569-fb6557cd0d1b.PNG)

![Segmen 11](https://user-images.githubusercontent.com/107464383/196385470-aa11795a-3ff6-4cc8-8bf0-fa7808c5d938.PNG)

![Segmen 12](https://user-images.githubusercontent.com/107464383/196385473-fc6ff243-612a-47cb-a832-74a602a78559.PNG)

![Segmen 13](https://user-images.githubusercontent.com/107464383/196385477-fbf481f7-70e5-4fbd-912f-cc6e4065e1e5.PNG)

![Segmen 14](https://user-images.githubusercontent.com/107464383/196385480-49950f33-bf87-484f-b003-ad0903eec212.PNG)

![Segmen 15](https://user-images.githubusercontent.com/107464383/196385482-16a9fb36-a91e-435f-a697-32052ee0e343.PNG)

![Segmen 16](https://user-images.githubusercontent.com/107464383/196385488-091642f8-7b50-4080-ae62-9887fdacde3d.PNG)

![Segmen 17](https://user-images.githubusercontent.com/107464383/196385491-92c0a0b4-a29c-4b70-84c5-204b543875a5.PNG)

# Summary

Based on visualization of customer clusters, we can tell the characteristic of each clusters

## Cluster 0

- Majority of customers belong to this cluster
- Have low to medium - low income
- Majority have 1 - 2 children at home
- Spend less money on products
- Buy less products
- Complains a lot
- Don't like to buy product via catalog
- Gives negatives responses on marketing campaign

## Cluster 1

- Have medium-high to high income
- Have 0-1 children at home
- Cluster with second highest amount of total purchases
- Spent more money on fruits and fish products
- Gives negative responses on marketing campaign
- Likes to buy product via store
- Likes discount

## Cluster 2

- Have low-medium to medium-high income
- Consist of customers in adult to senior age group
- Have 1-2 children at home
- Spent more money on wine and gold
- Really likes discount
- Gives positives responses on marketing campaign

## Cluster 3

- Cluster with least number of customers on it
- Have high income
- Majority are child-free
- Cluster with highest amount of total purchases
- Spent more money on all kinds of products
- Less likely to complain
- likes to buy product via catalog
- Don't likes discount
- Gives positive responses on marketing campaign

# Conclusions

After we perform clustering to create customer segmentation, we have 4 segmentation for our customers. We can tell that cluster 3 is our best cluster because they are spent more money on all kinds of products, less likely to complain, don't likes discount, and gives positive responses on marketing campaign. Cluster 0 is our worst cluster because thay are spend less money on products, buy less products, complains a lot, and gives negative responses on marketing campaign

For next campaign, we can create marketing campaign towards cluster 2 and cluster 3 because they are giving positive responses on marketing campaign. For cluster 3, we can use catalog as media for our campaign because they likes to buy product via catalog. For cluster 2, we can gives discount with minimum spend on wines and gold products because they likes discount and spend more money on gold and wines product






















