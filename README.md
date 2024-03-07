What You're Creating
This new assignment consists of two technical products. You will submit the following deliverables:

Deliverable 1: Scrape titles and preview text from Mars news articles.

Deliverable 2: Scrape and analyze Mars weather data, which exists in a table.


Code source:

# Loop through the text elements .ChatGPT (personal communication, March 5, 2024).
for title, preview in zip(titles, preview):
    dictionary = {'title': title.text.strip(), 'preview': preview.text.strip()}
    list.append(dictionary)



#get headings th. ChatGPT (personal communication, March 5, 2024).
headings = ['id', 'terrestrial_date', 'sol', 'ls', 'month', 'min_temp', 'pressure']

# Loop through the scraped data to create a list of rows. . ChatGPT (personal communication, March 5, 2024)
for table in data:
    # Loop through each table row and extract data
    rows = table.find_all('tr')[1:]  # Start from index 1 to skip the header row
    for row in rows:
        # Extracting data from each row
        row_data = [td.text.strip() for td in row.find_all('td')]
        # Ensure row_data is not empty
        if row_data:
            # Creating a dictionary where keys are the headings and values are the row data
            row_dict = dict(zip(headings, row_data))
            # Adding the row dictionary to the data list
            row_list.append(row_dict)
        else:
            print("Skipping empty row:", row)



# ChatGPT (personal communication, March 6, 2024)
import numpy as np

# Sample DataFrame creation
# Replace this with your actual DataFrame
earthly_date = {'terrestrial_date': pd.date_range(start='2012-08-16', end='2018-02-27', periods=1850),
        'min_temp': np.random.randint(-90, -59, size=1850)}
df = pd.DataFrame(earthly_date)

# Calculate the number of Earth days since the start
df['earth_days'] = (df['terrestrial_date'] - df['terrestrial_date'].min()).dt.days

# Plotting
plt.figure(figsize=(10, 6))
plt.plot(df['earth_days'], df['min_temp'], color='blue')
plt.xlabel("Terrestrial Days")
plt.ylabel("Minimum Temperature (°C)")

# Draw vertical lines at 1000 and 1600 Earth days
plt.axvline(x=1000, color='red', linestyle='--', label='Peak 1 (Day 1000)')
plt.axvline(x=1600, color='green', linestyle='--', label='Peak 2 (Day 1600)')

plt.show()
