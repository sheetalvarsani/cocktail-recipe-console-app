# Cocktail Recipe Console App

This is a Python-based console application that allows users to search for cocktail recipes by specifying an alcohol type (e.g., vodka, rum, gin). The app utilizes the free [TheCocktailDB API](https://www.thecocktaildb.com/api.php) to fetch cocktail data and allows users to save their favorite cocktail recipes to a text file.

## Features

- Search for cocktail recipes based on the type of alcohol.
- List various cocktails that can be made with the selected alcohol.
- Retrieve detailed recipes including ingredients, measurements, and instructions.
- Save the cocktail recipe to a text file for easy access.

## Prerequisites

Before you begin, ensure you have met the following requirements:

- You have installed Python 3.x.
- You have an active internet connection (the app uses an external API to fetch cocktail data).

## Installation

1. Clone this repository
2. Make sure you're in the correct directory < cd cocktail-recipe-console-app >
3. Create and activate a virtual environment
4. Install the required Python packages (if needed) - This project uses the requests library to fetch data from the API. If you don't have it installed, you can do so by running: pip install requests
5. Open project in PyCharm or preferred IDE and run application.



<br>

```bash

git clone <repository-url>

cd cocktail-recipe-console-app

python -m venv venv
venv\Scripts\activate

pip install requests

```


## Example code:

```
Welcome to the Cocktail Maker!

Enter the alcohol you'd like to make a cocktail with (eg. vodka, rum, gin): vodka

Here are some cocktail options for you:

1. Moscow Mule
2. Bloody Mary
3. Cosmopolitan

Enter the list number of the cocktail you'd like the recipe for: 1

The recipe for Moscow Mule has been written to 'Moscow_Mule_recipe.txt'.

Do you want to try another cocktail recipe? (y/n): n

Thank you for using the Cocktail Maker, enjoy your drink!
```


## Acknowledgements

This app uses the [TheCocktailDB API](https://www.thecocktaildb.com/api.php) to fetch cocktail recipes.


