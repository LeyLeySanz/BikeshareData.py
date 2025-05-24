# I am doing the Udacity course for Introduction to Python and this is the final project. I've already submitted it, but it's giving me some identation errors.
# Can someone explain where I possibly went wrong and how to fix it. I'm not sure I understand the identation error.


import time
import pandas as pd
import numpy as np

CITY_DATA = { 'chicago': 'chicago.csv',
              'new york city': 'new_york_city.csv',
              'washington': 'washington.csv' }

def get_filters():
    """
    Asks user to specify a city, month, and day to analyze.

    Returns:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    """
    print('Hello! Let\'s explore some US bikeshare data!')
    # TO DO: get user input for city (chicago, new york city, washington). HINT: Use a while loop to handle invalid inputs
while True:
    city=input("Which city would you like to explore?('Chicago', 'New York', 'Washington'): ").strip().lower()
    if city in CITY_DATA:
        break
    else:
        print("Invalid input. Please select or enter one of the listed cities.")

    # TO DO: get user input for month (all, january, february, ... , june) 
months = ['all', 'january', 'february', 'march', 'april', 'may', 'june']
    while True:
        month = input("Which month? (January to June, or 'all'): ").strip().lower()
        if month in months:
            break
        else:
            print("Invalid month. Please enter from January to June or 'all'.")
    if month in months:
                 break
    else:
                 print("Invalid input. Please enter a month or select 'all'. ")
                   
    # TO DO: get user input for day of week (all, monday, tuesday, ... sunday)
days = ['all', 'monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday', 'sunday']
    while True:
        day = input("Which day? (Monday to Sunday, or 'all'): ").strip().lower()
        if day in days:
            break
        else:
            print("Invalid day. Please choose a valid weekday or 'all'.")

    print('-'*40)
    return city, month, day


def load_data(city, month, day):
    """
    Loads data for the specified city and filters by month and day if applicable.

    Args:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    Returns:
        df - Pandas DataFrame containing city data filtered by month and day
    """
df = pd.read_cvs(CITY_DATA[city])

df['Start Time']=pd.to_datetime(df['Start Time']
df['month']=df['Start Time'].dt.month_name().str.lower()
df['day_of_week']=df['Start Time'].dt.day_name().str.lower()
df['hour']=df['Start Time'].dt.hour
                                
if month != 'all':
      df=df[df['month']==month'
if day != 'all':
      df=df[df['day_of_week']==day]

    return df


def time_stats(df):
    """Displays statistics on the most frequent times of travel."""

    print('\nCalculating The Most Frequent Times of Travel...\n')
    start_time = time.time()

    # TO DO: display the most common month
common_month= df['month'].mode()[0]
print(f"Most Common Month: {common_month.title()}")

    # TO DO: display the most common day of week
common_day= df['day_of_week'].mode()[0]
print(f'Most Common Day of Week:{common_day.title()}")

    # TO DO: display the most common start hour
common_hour= df['hour'].mode()[0]
print(f"Most Common Start Hour: {common_hour}")

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def station_stats(df):
    """Displays statistics on the most popular stations and trip."""

    print('\nCalculating The Most Popular Stations and Trip...\n')
    start_time = time.time()

    # TO DO: display most commonly used start station
start_station=df['Start Station'].mode()[0]
      print("Most Common Start Station: {start_station}")

    # TO DO: display most commonly used end station
end_station=df['End Station'].mode()[0]
      print("Most Common End Station: {end_station}")

    # TO DO: display most frequent combination of start station and end station trip
df['Start_End_Combo'] = df['Start Station'] + 'to' + df['End Station']
      most_common_trip=df['Start to End Combo'].mode()[0]
print("Most Frequent Trip: {most_common_trip}")

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def trip_duration_stats(df):
    """Displays statistics on the total and average trip duration."""

    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # TO DO: display total travel time
total_duration=df['Trip Duration'].sum()
print("Total Travel Time:{total_duration} seconds")

    # TO DO: display mean travel time
average_duration=df['Trip Duration'].mean()
print("Average Travel Time: {average_duration:.2} seconds")

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def user_stats(df):
    """Displays statistics on bikeshare users."""

    print('\nCalculating User Stats...\n')
    start_time = time.time()

    # TO DO: Display counts of user types
user_types=df['User Types'].value_counts()
      print("User Types:")
      print(df['User Types'].value_counts().to_str())
      print()
else:
      print("Gender data not available for this city.")

    # TO DO: Display counts of gender
if 'Gender' in df.columns:
      print('Gender Counts:'_
      print(df['Gender'].value_counts().to_str())
      print()
else:
      print("Gender data not available for this city.")

    # TO DO: Display earliest, most recent, and most common year of birth
earliest=int(df['Birth Year'].min())
latest=int(df['Birth Year'].max())
most_common=int(df['Birth Year'].mode()[0])
      print(f"Earliest Birth Year:{earliest}")
      print(f"Most Recent Birth Year: {latest}")
      print(f"Most Common Birth Year: {most_common}")
else:
      print("Birth year data not available for this city.")

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def main():
    while True:
        city, month, day = get_filters()
        df = load_data(city, month, day)

        time_stats(df)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df)

        restart = input('\nWould you like to restart? Enter yes or no.\n')
        if restart.lower() != 'yes':
            break


if __name__ == "__main__":
	main()
