import pandas as pd
import numpy as np

# Here we read the file using pd.read_csv
auto = (r'D:\excel\automobile_data.csv')
df = pd.read_csv(auto)

# for printing the first 15 rows we need to use the first 15 rows
# for printing the last 15 rows we need to use the last 15 rows
print(" first 15 rows: ")
print(df.head(15))

print("last 15 rows: ")
print(df.tail(15))

# replace ? with value and n.a with Nan
new_value = df.replace("?",2)
print(new_value)

# old_value = df.replace("n.a" "Nan")
# print(old_value)

# convert price to numeric errors= 'coerce to handle non numeric values
#errors = coerce means it replaces all the null values with Nan
# idxmax is used to locate the max index of the database
df['price'] = pd.to_numeric(df['price'],errors="coerce")
max_price = df.loc[df['price'].idxmax()]
print(f"Company name:{max_price['make']}\nprice:{max_price['price']}")

# Calculate maximum horsepowers for each company.(df.groupby())
# pd.to_numeric is a function that converts the data to numeric format
# df.groupby is used to group the data of specific columns or rows together

df['horsepower'] = pd.to_numeric(df['horsepower'], errors="coerce")
max_horsepower = df.groupby('make')['horsepower'].max()
print(max_horsepower)

# calculate min wheel base per fuel type
df['wheel-base'] = pd.to_numeric(df['wheel-base'], errors="coerce")
min_wheel_base = df.groupby('fuel-type')['wheel-base'].min()
print(min_wheel_base)

 # Create a new column for the updated price. This updated price will be calculated on top of the given price -
#  if the engine is in front, price will be same else if the engine is in rear, price will be doubled.

df['price'] = pd.to_numeric(df['price'], errors="coerce")
df['updated_price'] = np.where(df['engine-location'] == "rear",df['price'] * 2, df['price'])
print(df[['make', 'engine-location', 'price','updated_price']])

# Sort the cars by price columns(sort_values(by=))
# here we have sorted the price column in descending order by using sort_values
sorted_price = df.sort_values(by="price",ascending=False)
print(sorted_price[["make","price"]])

# Print the total number of cars manufactured by each company.value_counts()
# We have counted the total number of cars each company has produced
total_cars = df['make'].value_counts()
print(total_cars)


