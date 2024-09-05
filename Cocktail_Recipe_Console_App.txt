"""
For this console app, I am using an API called The Cocktail DB which is free to use at its basic level:
(https://www.thecocktaildb.com/api.php)

It is a database of cocktails, which I am accessing by alcohol to get cocktail recipes for the chosen alcohol.

"""

import requests


# Function to get cocktail suggestions for chosen alcohol:
def get_cocktails(alcohol):
    url = "https://www.thecocktaildb.com/api/json/v1/1/filter.php?i={}".format(alcohol)
    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()
        return data['drinks']
    else:
        print("Error: Could not fetch cocktail data.")
        return None


# Function to get cocktail recipe by ID:
def get_cocktail_recipe(cocktail_id):
    url = "https://www.thecocktaildb.com/api/json/v1/1/lookup.php?i={}".format(cocktail_id)
    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()
        return data['drinks'][0]
    else:
        print("Error: Could not fetch cocktail details.")
        return None


# Function to write cocktail details to text file:
def write_cocktail_details(cocktail, file_name):
    with open(file_name, 'w') as file:
        file.write("Cocktail Name: {}\n".format(cocktail['strDrink']))
        file.write("Glass Type: {}\n".format(cocktail['strGlass']))
        file.write("\nIngredients:\n")

        # Show ingredients and measurements
        for i in range(1, 16):
            ingredient = cocktail['strIngredient{}'.format(i)]
            if ingredient:
                measurement = cocktail['strMeasure{}'.format(i)]
                file.write("{} {}\n".format(measurement, ingredient))

        file.write("\nInstructions:\n")
        file.write(cocktail['strInstructions'] + "\n\n")


# Main app function:
def main():
    print("\nWelcome to the Cocktail Maker!")

    while True:
        alcohol_choice = (input("\nEnter the alcohol you'd like to make a cocktail with (eg. vodka, rum, gin): ")
                          .strip().lower())

        cocktails = get_cocktails(alcohol_choice)

        # Lists cocktail options available with that alcohol:
        if cocktails:
            print("\nHere are some cocktail options for you:\n")
            for index, cocktail in enumerate(cocktails, start=1):
                print("{}. {}".format(index, cocktail['strDrink']))

            selection = input("\nEnter the list number of the cocktail you'd like the recipe for: ").strip().lower()

            # Writes the recipe for the chosen cocktail to a text file:
            try:
                selected_cocktail = get_cocktail_recipe(cocktails[int(selection) - 1]['idDrink'])
                cocktail_name = selected_cocktail['strDrink'].replace(' ', '_')
                write_cocktail_details(selected_cocktail, '{}_recipe.txt'.format(cocktail_name))
                print("\nThe recipe for {} has been written to '{}_recipe.txt'".format(selected_cocktail['strDrink'],
                                                                                       cocktail_name))

                # End the app or try again:
                choice = input("\nDo you want to try another cocktail recipe? (y/n): ").strip().lower()
                if choice != 'y':
                    print("\nThank you for using the Cocktail Maker, enjoy your drink!")
                    break

            except (ValueError, IndexError):
                print("Invalid selection. Please enter a valid number.")
        else:
            print("No cocktails found with {}. Please try another alcohol.".format(alcohol_choice))


if __name__ == "__main__":
    main()
