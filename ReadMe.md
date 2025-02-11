# **Best Selling Video Games Project:**
![alt text](Figs/Icon.png)
## **1. Introduction:**
This project analyzes the best-selling video games of all time, providing insights into the trends and titles that have dominated the gaming industry.  Using Python, data on the top 50 best-selling video games, spanning from 1984 to 2023, will be extracted from Wikipedia.  This data, representing global sales figures, will then be loaded into Power BI Desktop.  Within Power BI, the Extract, Transform, Load (ETL) process will be employed to clean, prepare, and structure the data, creating a robust foundation for analysis and reporting.  The resulting visualizations will offer a comprehensive overview of the best-selling games landscape, highlighting key performance indicators and potential patterns within this dynamic market.

You can see the full Dashboard from [here](Power_BI_Dashboard).

## **2. Tools I Used:**
To thoroughly explore insights and trends of the best-selling video games dataset I utilized the capabilities of a range of essential tools:

**1. Python:** for extract the tables of the dataset from the Wikipedia website.

**2. Power BI Desktop:** for Extract, Transform, Load (ETL) process and create interactive dashboards.

**3. Git & GitHub:** for sharing my analysis and dashboard.

## **3. Extract Tables From Web _Wikipedia_ (List of best-selling video games):**
Using Python Pandas library to extract tables from the Wikipedia website from link: https://en.wikipedia.org/wiki/List_of_best-selling_video_games

```py
import pandas as pd

url = "https://en.wikipedia.org/wiki/List_of_best-selling_video_games"

tables = pd.read_html(url)

print(f"The Number Of Tables = {len(tables)}")

for index, table in enumerate(tables):
    print(f"Saving Table_{index + 1}")
    file_name = f"table_{index + 1}.xlsx"
    table.to_excel(
        file_name,
        index=False,
    )
```
## **4. Upload Extracted Tables To Power BI Desktop:**

**4.1. Get data from Power BI using folder and choose _Excel_Files_Extraction_ folder:**

![alt text](Figs/P1.PNG)

**4.2. Transform tables unto power query for cleaning and preparing structure the data:**
![alt text](Figs/P2.PNG)

## **5. Claening And Preparing The Data In Power Query:**

**5.1. Use first row as headers.**

**5.2. Change type of column (sales) to fixced decimal number as it is currency column.**

**5.3. Remove duplicates if exists from remove rows.**

Replace null values in series column into (No Series).
Replace ([c]) from initial relase date column to avoid errors when converting the column type from text to date.
Cahange the type of column initial relase date column from text to date data type.
Remove column (Ref.) references from the original site.
Change title column name into Game.
Change initial relase date column name into Release_Date.
Change Developer(s)[b]column name into Developer(s).
Change Publisher(s)[b]column name into Publisher(s).
Close and apply.
Create games count measure:
Games_Count = DISTINCTCOUNT(Best_Selling_Video_Games[Game])

Create platform count measure:
Platforms_Count = DISTINCTCOUNT(Best_Selling_Video_Games[Platform(s)])

Create publisher count measure:
Publishers_Count = DISTINCTCOUNT(Best_Selling_Video_Games[Publisher(s)])

Create developers count measure:
Developers_Count = DISTINCTCOUNT(Best_Selling_Video_Games[Developer(s)])

Create series count measure:
Series_Count = DISTINCTCOUNT((Best_Selling_Video_Games[Series]))
Create total sales measure:
Total_Sales = SUM(Best_Selling_Video_Games[Sales])
