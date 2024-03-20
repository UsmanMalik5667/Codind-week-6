import datetime

# Constants
TICKET_PRICES = {
    "one day": {
        "adult": 20.00,
        "child": 12.00,
        "senior": 16.00,
        "family": 60.00,
        "group": 15.00
    },
    "two days": {
        "adult": 30.00,
        "child": 18.00,
        "senior": 24.00,
        "family": 90.00,
        "group": 22.50
    }
}
EXTRA_ATTRACTIONS = {
    "lion feeding": 2.50,
    "penguin feeding": 2.00,
    "evening barbecue": 5.00
}

# Function to display ticket options and attractions
def display_options():
    print("Ticket Options:")
    for ticket_type, prices in TICKET_PRICES.items():
        print(ticket_type.capitalize(), "Tickets:")
        for ticket, price in prices.items():
            print(f"{ticket.capitalize()}: ${price:.2f}")
    print("\nExtra Attractions:")
    for attraction, price in EXTRA_ATTRACTIONS.items():
        print(f"{attraction.capitalize()}: ${price:.2f}")

# Function to get booking details and calculate total cost
def process_booking():
    print("\nPlease enter booking details:")
    ticket_type = input("Enter ticket type (one day/two days): ").lower()
    while ticket_type not in TICKET_PRICES:
        print("Invalid ticket type!")
        ticket_type = input("Enter ticket type (one day/two days): ").lower()
    
    num_adults = int(input("Enter number of adults: "))
    num_children = int(input("Enter number of children: "))
    num_seniors = int(input("Enter number of seniors: "))
    num_days = 1 if ticket_type == "one day" else 2
    
    # Calculate base ticket cost
    total_cost = num_adults * TICKET_PRICES[ticket_type]["adult"] + \
                 num_children * TICKET_PRICES[ticket_type]["child"] + \
                 num_seniors * TICKET_PRICES[ticket_type]["senior"]
    
    # Check for family ticket
    if num_adults + num_seniors == 2 and num_children <= 3:
        total_cost = min(total_cost, TICKET_PRICES[ticket_type]["family"])
    
    # Check for group ticket
    num_people = num_adults + num_children + num_seniors
    if num_people >= 6:
        total_cost = min(total_cost, num_people * TICKET_PRICES[ticket_type]["group"])
    
    # Get extra attractions
    attractions = []
    while True:
        attraction = input("Enter extra attraction (leave blank to finish): ").lower()
        if not attraction:
            break
        while attraction not in EXTRA_ATTRACTIONS:
            print("Invalid attraction!")
            attraction = input("Enter extra attraction (leave blank to finish): ").lower()
        attractions.append(attraction)
    
    # Calculate extra attractions cost
    extra_cost = sum(EXTRA_ATTRACTIONS[attraction] for attraction in attractions)
    
    # Display booking details
    print("\nBooking Details:")
    booking_number = datetime.datetime.now().strftime("%Y%m%d%H%M%S")
    print(f"Booking Number: {booking_number}")
    print(f"Total Cost: ${total_cost + extra_cost:.2f}")
    print("Extra Attractions:", ', '.join(attractions))

# Function to run the program
def run_program():
    while True:
        print("\nWelcome to the Wildlife Park Ticket Booking System!")
        print("1. Display ticket options and attractions")
        print("2. Make a booking")
        print("3. Exit")
        choice = input("Enter your choice: ")
        
        if choice == "1":
            display_options()
        elif choice == "2":
            process_booking()
        elif choice == "3":
            print("Thank you for using the Wildlife Park Ticket Booking System. Goodbye!")
            break
        else:
            print("Invalid choice! Please enter 1, 2, or 3.")

# Run the program
if __name__ == "__main__":
    run_program()


OUTPUT:

<img width="396" alt="image" src="https://github.com/UsmanMalik5667/Codind-week-6/assets/130907787/db717b5e-9822-4e90-a079-013c52fe03d4">
<img width="590" alt="image" src="https://github.com/UsmanMalik5667/Codind-week-6/assets/130907787/1915a750-abdc-48e9-8c81-c237f9dc1d9c">




