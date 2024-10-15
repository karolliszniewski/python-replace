```py
import os
import re

# Define the path to the di.xml file
file_path = 'app/etc/di.xml'

# Check if the file exists
if os.path.exists(file_path):
    # Read the content of the file
    with open(file_path, 'r') as file:
        content = file.read()

    # Define the pattern to search for and the replacement
    pattern = r'<item name="MySQL-8" xsi:type="string">^8\.0\.</item>'
    replacement = '<item name="MySQL-8" xsi:type="string">^8\.*\.</item>'

    # Replace the pattern in the content
    new_content = re.sub(pattern, replacement, content)

    # Write the modified content back to the file
    with open(file_path, 'w') as file:
        file.write(new_content)

    print(f"Updated '{file_path}' successfully.")
else:
    print(f"File '{file_path}' does not exist.")

```


```
pip install mysql-connector-python
```

```py
import mysql.connector
from mysql.connector import Error

def update_core_config_data():
    # Database connection parameters
    db_config = {
        'host': 'localhost',
        'user': 'your_username',  # Replace with your database username
        'password': 'your_password',  # Replace with your database password
        'database': 'your_database'  # Replace with your database name
    }

    try:
        # Connect to the database
        connection = mysql.connector.connect(**db_config)

        if connection.is_connected():
            print("Connected to the database.")

            # Create a cursor object
            cursor = connection.cursor()

            # SQL update query
            sql_update_query = """
            UPDATE core_config_data
            SET value = 'https://test.com'
            WHERE value LIKE 'https%'
            """

            # Execute the update query
            cursor.execute(sql_update_query)

            # Commit the changes
            connection.commit()

            print(f"Updated {cursor.rowcount} rows successfully.")

    except Error as e:
        print(f"Error: {e}")

    finally:
        # Close the cursor and connection
        if (connection.is_connected()):
            cursor.close()
            connection.close()
            print("Database connection closed.")

if __name__ == "__main__":
    update_core_config_data()

```
