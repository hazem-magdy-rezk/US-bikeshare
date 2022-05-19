import time
import pandas as pd
import numpy as np
CITY_DATA = {'chicago': 'chicago.csv',
              'new_york_city': 'new_york_city.csv',
              'washington': 'washington.csv' }

def get_filters():
    print('Hello! Let\'s explore some US bikeshare data!')
    error_message=" sorry we didn't get a right answer, try one more time "
    while True:
        city_input =input(" which city would you like to explore. chicago, new york or washington ? (please write new york seperated by space)  " )
        if city_input.lower() == "chicago":
            city='chicago'
            print(" thank you we are glad to show you chicago's bikeshare data")
            break
        elif city_input.lower()=="new york":
            city='new_york_city'
            print(" thank you we are glad to show you new york's bikeshare data")
            break
        elif city_input.lower()=="washington":
            city='washington'
            print(" thank you we are glad to show you  washingtons's bikeshare data")
            break
        else:
            print( error_message )
            continue
    valid_months=["january","february","march","april","may","june","july","august","septemper","october","november","december","all"]
    while True:
        month = input(" would you like to explore a specific month or all ? type month full name or all for no month filter ")
        if month.lower() in valid_months:
            break
        else :
            print(error_message)
            continue
    valid_days=["saturday","sunday","monday","tuesday","wednesday","thursday","friday","all"]
    while True:
        day = input(" do you want to choose a specific day to explore data from ? type a day full name or all for no days filter ")
        if day.lower() in valid_days:
            break
        else:
            print(error_message)
            continue
    print('-'*40)
    print(" we will make sure to filter data exactly as you prefer  ")
    print( " please wait untill we prepare data ... ")
    return city,month,day
def load_data(city, month, day):
    df=pd.read_csv(CITY_DATA[city])
    df['Start Time'] = pd.to_datetime(df['Start Time'])
    df['month'] = df['Start Time'].dt.month
    df['day_of_week'] = df['Start Time'].dt.day_name()
    if month != 'all':
        months = ['january', 'february', 'march', 'april', 'may', 'june','july','august','septemper','october','november','december']
        month = months.index(month) + 1
        df = df[df['month'] == month]
    if day != 'all':
        # filter by day of week to create the new dataframe
        df = df[df['day_of_week'] == day.title()]
    return df
def time_stats(df):

    print('\nCalculating The Most Frequent Times of Travel...\n')
    start_time = time.time()

    df['Start Time']=pd.to_datetime(df['Start Time'])
    df['month']=df['Start Time'].dt.month_name()
    popular_month = df['month'].mode()[0]
    print(' Most Popular month is  :', popular_month)

    # display the most common day of week

    df['Start Time'] = pd.to_datetime(df['Start Time'])
    df['day'] = df['Start Time'].dt.day_name()
    popular_day = df['day'].mode()[0]
    print('\n Most Popular day is  :', popular_day)

    # display the most common start hour

    df['Start Time'] = pd.to_datetime(df['Start Time'])
    df['hour'] = df['Start Time'].dt.hour
    popular_hour = df['hour'].mode()[0]
    print('\n Most Popular Start Hour:', popular_hour)

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)

def station_stats(df):

    print('\nCalculating The Most Popular Stations and Trip...\n')
    start_time = time.time()

    # display most commonly used start station
    popular_start_station=df['Start Station'].mode()[0]
    print(" the most popular start station is : " , popular_start_station)

    # display most commonly used end station
    popular_end_station = df['End Station'].mode()[0]
    print("\n the most popular end station is : ", popular_end_station)

    # display most frequent combination of start station and end station trip
    common_trip = df.groupby(['Start Station'])['End Station'].value_counts().nlargest(1)
    print( "\n the most frequent combination is : " , common_trip)
    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)

def trip_duration_stats(df):

    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # display total travel time
    total_travel_time = df['Trip Duration'].sum()
    print("\n total travel time is :  ", total_travel_time)
    # display mean travel time
    avarage_travel_time = df['Trip Duration'].mean()
    print("\n avarage travel time is :  ", avarage_travel_time)

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)

def user_stats(df):

    print('\nCalculating User Stats...\n')
    start_time = time.time()

    user_types = df['User Type'].value_counts()
    print(user_types)
    # Display counts of gender
    try:
        user_gender = df['Gender'].value_counts()
        print(user_gender)
    except KeyError:
        print("\n washington has no gender data")

    # Display earliest, most recent, and most common year of birth
    try:
        earliest_birth_year = df['Birth Year'].min()
        print("\n the earliest birth year is : ", earliest_birth_year )
        latest_birth_year = df['Birth Year'].max()
        print("\n the latest birth year is : ", latest_birth_year)
        popular_birth_year = df['Birth Year'].mode()[0]
        print("\n the popular birth year is : ", popular_birth_year)
    except KeyError:
        print(" washington has no birth year data")

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)
def raw_data(df):
    x=0
    y=5
    while True:
        raws=input( " would you like to view more 5 raws of data from selected city ? \n'yes' or 'no' : ")
        if raws.lower()=='yes':
            print(df.iloc[x:y])
            x += 5
            y += 5
            continue
        else:
            break
def main():
    while True:
        city, month, day = get_filters()
        df = load_data(city, month, day)
        time_stats(df)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df)
        raw_data(df)
        restart = input('\nWould you like to restart? Enter yes or no.\n')
        if restart.lower() != 'yes':
            break

if __name__ == "__main__":
    main()
