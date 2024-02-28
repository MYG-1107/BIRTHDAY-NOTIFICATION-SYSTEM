# Author: Mallarapu Yaswanth   
# GMAIL ID : 23641a66d3@vaagdevi.edu.in  OR mallarapuyaswanth05@gmail.com
# MOBILE NUMBER : 8639975852
# Student of Vaagdevi College of Engineering
# Date: 2024-02-28
# Import the datetime module to work with dates and times
from datetime import datetime

# User data containing personal information and visibility settings
user_data = {
    "name": "Mallarapu Yaswanth",
    "date_of_birth": "2005-07-11",  # Placeholder for the birth date 
    "visible_to": ["Friend1", "Family Group"]  # List of contacts who can view the birth date
}

# Function to manage visibility settings
def manage_visibility():
    # Display current visibility settings
    print("Current visibility settings:")
    print("People who can see your date of birth:", ", ".join(user_data['visible_to']))

    # Prompt the user for action choice
    choice = input("Do you want to\n1. Add contacts\n2. Remove contacts\n3. Cancel\n")

    # Add contacts
    if choice == "1":
        new_contact = input("Enter the name of the contact to add: ")
        user_data["visible_to"].append(new_contact)
        print(f"Added {new_contact} to the list.")
    # Remove contacts
    elif choice == "2":
        contact_to_remove = input("Enter the name of the contact to remove: ")
        if contact_to_remove in user_data["visible_to"]:
            user_data["visible_to"].remove(contact_to_remove)
            print(f"Removed {contact_to_remove} from the list.")
        else:
            print("Contact not found.")
    # Cancel operation
    else:
        print("Cancelled.")

# Function to notify upcoming birthdays
def notify_birthdays():
    # Get today's date
    today = datetime.now().date()

    # Convert the birth date string to a datetime object
    dob = datetime.strptime(user_data["date_of_birth"], "%Y-%m-%d").date()

    # List to store upcoming birthdays
    upcoming_birthdays = []

    # Iterate through each contact to check for upcoming birthdays
    for contact in user_data["visible_to"]:
        # Calculate the next birthday for the contact
        contact_dob = dob.replace(year=today.year)
        if contact_dob < today:
            contact_dob = contact_dob.replace(year=today.year + 1)
        days_until_birthday = (contact_dob - today).days

        # Check if the birthday is today, tomorrow, or later
        if days_until_birthday == 0:
            print(f"Today is {contact}'s birthday!")
        elif days_until_birthday == 1:
            print(f"Tomorrow is {contact}'s birthday!")
        else:
            upcoming_birthdays.append((contact, days_until_birthday))

    # Display upcoming birthdays
    for contact, days_until_birthday in upcoming_birthdays:
        print(f"{contact}'s birthday is in {days_until_birthday} days.")

# Main function to run the program
def main():
    # Loop to display the menu and handle user input
    while True:
        print("\nWelcome to Birthday Notification System")
        print("1. Manage Visibility Settings")
        print("2. Notify Birthdays")
        print("3. Exit")
        
        # Prompt the user for their choice
        choice = input("Enter your choice: ")
        
        # Execute corresponding functions based on the user's choice
        if choice == "1":
            manage_visibility()
        elif choice == "2":
            notify_birthdays()
        elif choice == "3":
            print("Exiting...")
            break
        else:
            print("Invalid choice. Please enter a valid option.")

# Entry point of the program
if __name__ == "__main__":
    main()
