import pandas as pd
from sqlalchemy import create_engine

# Database connection details
username = 'your_username'
password = 'your_password'
host = 'your_host'
database = 'your_database'

# Create a connection to the database
engine = create_engine(f'mysql+pymysql://{username}:{password}@{host}/{database}')

# SQL query to fetch the data
sql_query = """
SELECT 
    Name, 
    Surname, 
    Currency, 
    Amount, 
    `Value Date`, 
    Region, 
    Country
FROM 
    your_table_name
"""

# Execute the query and load the data into a pandas DataFrame
df = pd.read_sql(sql_query, engine)

# Path to save the Excel file
excel_path = 'your_data.xlsx'

# Write the DataFrame to an Excel file
with pd.ExcelWriter(excel_path, engine='openpyxl') as writer: # or engine='xlsxwriter'
    df.to_excel(writer, index=False)

print("Data exported to Excel successfully.")
