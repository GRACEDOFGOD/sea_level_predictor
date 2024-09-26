# sea_level_predictor
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress

def draw_line_plot():
    # Load the data
    df = pd.read_csv('epa-sea-level.csv')

    # Create scatter plot
    plt.figure(figsize=(10, 5))
    plt.scatter(df['Year'], df['CSIRO Adjusted Sea Level'], color='blue', label='Observed Data')

    # Create first line of best fit (from the entire dataset)
    slope, intercept, r_value, p_value, std_err = linregress(df['Year'], df['CSIRO Adjusted Sea Level'])
    
    # Create x values for the line of best fit
    x_fit = pd.Series(range(1880, 2051))  # From 1880 to 2050
    y_fit = slope * x_fit + intercept

    # Plot the line of best fit
    plt.plot(x_fit, y_fit, color='red', label='Best Fit Line (All Data)')

    # Create second line of best fit (from the year 2000 onwards)
    df_recent = df[df['Year'] >= 2000]
    slope_recent, intercept_recent, r_value_recent, p_value_recent, std_err_recent = linregress(df_recent['Year'], df_recent['CSIRO Adjusted Sea Level'])
    
    # Create x values for the second line of best fit
    x_fit_recent = pd.Series(range(2000, 2051))  # From 2000 to 2050
    y_fit_recent = slope_recent * x_fit_recent + intercept_recent

    # Plot the second line of best fit
    plt.plot(x_fit_recent, y_fit_recent, color='green', label='Best Fit Line (2000 Onwards)')

    # Labeling the plot
    plt.title('Rise in Sea Level')
    plt.xlabel('Year')
    plt.ylabel('Sea Level (inches)')
    plt.legend()
    plt.grid()

    # Save the figure
    plt.savefig('sea_level_plot.png')
    plt.show()

# Uncomment to run the function
# draw_line_plot()
