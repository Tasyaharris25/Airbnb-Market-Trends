# Airbnb-Market-Trends
Data Source : Kaggle

**Introduction**

Airbnb is property management company that manages rental listings across the world. This dataset captured data of property listing in Airbnb in multiple cities in United States. By analyzing this dataset, Airbnb can optimize their property listings and maximize revenue by understanding key market trends, pricing strategies, and customer preferences.

**Objective**

The goal of this project is to analyze rental property data to:

1. Identify factors influencing pricing
2. Evaluate customer preferences for room types and property types. 
3. Determine if the cancellation policy affects the rental rate.
4. Assess whether cleaning fees affect the rental rate.
5. Examine the impact of instant bookable on the rental rate.
6. Provide recommendations to improve listing performance

**Data Preparation**

- Check if there are duplicate data
  ```
  duplicates = df.duplicated()
  print("Number of duplicate rows:", duplicates.sum())
  ```
  <img width="197" alt="image" src="https://github.com/user-attachments/assets/810b09d7-1812-47e0-8e3d-4e1aa3b511db" />

  no duplicate data
    
- Data cleaning
  ```
  null_values = df.isnull().sum()
  print(null_values)
  ```
  There are no null values in the important fields being analyzed, so missing data can be ignored without affecting the integrity of the analysis.
    

**Analysis**

- Convert Log Prices to Actual Prices
```
df['price'] = np.exp(df['log_price'])

print(df['price'].describe())
```
1. Pricing Analysis 
    - average price by room type
      
       <img width="154" alt="image" src="https://github.com/user-attachments/assets/a3853c62-c7f3-43d6-8095-8bb655c915e6" />

        - Entire home/apartment has the highest average price among room types, indicating guests are willing to pay a premium for complete privacy and exclusive access.
        - Private rooms and shared rooms have significantly lower prices than entire homes/apartments, suggesting that shared spaces or limited amenities reduce their value.
          
    - average price by property type
  
      <img width="170" alt="image" src="https://github.com/user-attachments/assets/a1a64bc8-1db9-4dd6-a6ac-053ebeb90705" />

        - Luxury property types such as Villas and Earth Houses command the highest prices due to their unique and upscale experiences.
        - Standard property types like Apartments and Houses fall in the mid-price range, offering traditional lodging with modern amenities.
        - Budget-friendly options like Dorms and Hostels are the most affordable, targeting travelers on tight budgets.
        - Niche experiences like Castles and Treehouses can charge a premium for their uniqueness.
          
    - average price by number of bedrooms
      
      <img width="262" alt="image" src="https://github.com/user-attachments/assets/28b1a89d-6598-4d80-83f5-ecf0a0578209" />
      
        - Rental prices increase as the number of bedrooms increases, reflecting the added spaces and accommodation capacity.
        - Properties with 6-10 bedrooms have significantly higher prices, targeting large groups or luxury markets.
        - Prices slightly fluctuate after 7 bedrooms, possible due to fewer listing.
        - Property with 0 bedrooms have a relatively higher average price, suggesting these might include premium locations or modern studio apartments.
          
2. Customer Preference
    - Average Review Scores by Room Type
   
      <img width="214" alt="image" src="https://github.com/user-attachments/assets/4bb9a351-86b2-4af3-ad8a-9ca30fdc2608" />

        - Entire home/apt has the highest average review score, indicating guests generally prefer and rate exclusive accommodations highly.
        - The difference in average review scores is minimal, implying that guests value their experiences in all room types. However, entire homes/apartments slightly edge out in guest satisfaction.

    - Popularity Room Types

      <img width="143" alt="image" src="https://github.com/user-attachments/assets/d174811f-9be4-4ce2-94c5-afe6ffde2004" />

        - Entire home/apt is the most popular room types, with the largest number of listings, reflects high demand for accommodations offering privacy and exclusivity.
        - Private rooms are the second most popular, while shared rooms are the least popular, indicating lower demand. Despite this, shared rooms still maintain reasonable review scores, satisfying their niche audience.
   
3. Does cancellation policy affect rental rate?
    - Distribution of Rentals by Cancellation Policy
      
      <img width="134" alt="image" src="https://github.com/user-attachments/assets/357ecf75-c0e5-4007-b416-7c6267a38c5a" />
      

      The majority of listings have a **strict cancellation policy**, followed by **flexible** and **moderate**.  **Super Strict 30** and **Super Strict 60** policies are much less common, with only 112 and 17 rentals, respectively. This indicates that these policies are rare and likely not preferred by hosts or guests.
          
    - ANOVA Test Results
        - ANOVA is a statistical tool used to compare the means of multiple groups to determine if there are significant differences between them.

  
          <img width="187" alt="image" src="https://github.com/user-attachments/assets/dd66e897-883c-40f1-9216-7f3e4445df4f" />
          

        - Based on the results, the high F-statistic indicates a significant difference in rental rates across different cancellation policies. The p-value is less than 0.05, confirming that **cancellation policy has a significant effect on rental rates**.
        
4. Does Property with Cleaning Fee Affect Rental Rate?
    - Rental Count by Cleaning Fee
    
      <img width="119" alt="image" src="https://github.com/user-attachments/assets/20f9d891-8886-4f22-bd0d-e35dc893232b" />

      Based on the listings, the majority of properties include a cleaning fee, indicating hosts likely consider cleaning fees a standard practice to cover additional maintenance costs.
          
    - T-Test Result

      <img width="260" alt="image" src="https://github.com/user-attachments/assets/199cc25c-c099-4a56-9a6f-0fa6b8e3c868" />

       - A t-test is a statistical tool used to compare the means of two groups or the difference between one group's mean and a standard value. T-tests             are used to determine if differences are statistically significant, or if they occurred by chance.
       - T-statistic (7.0523): This value indicates a substantial difference in the average rental rates between properties with and without cleaning                fees. A higher absolute value of the t-statistic generally implies a stronger relationship.
       - p-value (0.0000): The extremely low p-value (essentially zero) is highly significant. This means there's an extremely low probability that the             observed difference in rental rates between the two groups (with and without cleaning fees) occurred by chance.
       - Properties with cleaning fees generally have higher rental rates. Hosts likely use cleaning fees to cover maintenance costs and may factor this             into their overall pricing strategy
        
6. Does Property with Instant Bookable Affect Rental Rate?
    - Rental Record by Instant Bookable System


       <img width="140" alt="image" src="https://github.com/user-attachments/assets/e2e02672-0085-4c89-ac97-db6a0e31e8a1" />



       The properties without instant booking has significantly more rentals than properties with instant booking, suggesting that hosts prefer a manual           approval process to manage bookings more selectively.
   
    - T-Test Result:
   
       <img width="266" alt="image" src="https://github.com/user-attachments/assets/a06dabb4-e928-4129-8ed6-6f667c1844e4" />



        The t-test confirms that the presence of an instant booking system significantly affects rental rates. The negative T-statistic indicates that              properties with instant booking have, on average, lower rental rates compared to those without instant booking.
    
    **Recommendations and Insights**
    
    1. **Optimize Pricing Strategies:**
        - Increase rental rates for luxury and niche property types to maximize revenue from premium audiences.
        - *Consider offering competitive pricing for instant booking properties to attract more travelers while ensuring profitability.*
    2. **Leverage Cleaning Fees:**
        - Highlight the inclusion of cleaning fees as a value-added service to maintain guest satisfaction while covering operational costs.
        - Educate hosts on setting cleaning fees to optimize total rental income.
    3. ***Improve Instant Bookable Systems:***
        - *Encourage more hosts to adopt instant booking to cater to travelers seeking convenience. However, maintain competitive pricing to balance demand and revenue.*
    4. **Cancellation Policies:**
        - Promote flexible and moderate cancellation policies to attract more bookings, as stricter policies may deter potential guests.
    5. **Target Marketing:**
        - Market entire homes/apartments as the most preferred room type, focusing on privacy and exclusivity.
        - Highlight the affordability and practicality of private and shared rooms to appeal to budget travelers.
    
    By addressing these factors, Airbnb can enhance its property listings, align offerings with market demand, and increase overall profitability.
