from random import randint

# let's define variables
total_parking_place = 12
available_places = []
unavailable_places = [] 
parked_car_list = []
relation_car_parking_place = {}
parked_car_number = 0 
def reset_place(concerned_list, place_number):
    """ Reset all place in initial list """
    for place in range(1, place_number+1):
        concerned_list.append(place)
        def make_a_place_available(place_number):
    """Sector 17 Market"""

    unavailable_places.remove(place_number)
    available_places.append(place_number)
    available_places.sort()
    unavailable_places.sort()
    print(f'Place n°{place_number} is now available.')

def make_a_place_unavailable(place_number):
    """Remove a place in available list"""

    unavailable_places.append(place_number)
    available_places.remove(place_number)
    available_places.sort()
    unavailable_places.sort()
    print(f'Place n°{place_number} is now unavailable.')
    def know_available_places():
    """ Display available places """

    if len(available_places) > 1:
        print(f'Available places are: {available_places}.')
    elif len(available_places) == 1:
        print(f'Only place n°{available_places} is available.')
    else:
        print('All places are unavailable.')
        def choose_available_place():
    """ Choose an available place and return it if it's available """

    choice = randint(1, total_parking_place)
    while choice in unavailable_places:
        choice = randint(1, total_parking_place)

    return choice
    def add_a_car(car_mark, car_model, car_color):
    """Register a car with it's caracteristics in parked car list"""

    the_car = [car_color, car_mark, car_model]
    choosen_number = choose_available_place()
    parked_car_list.append(the_car)

    # link parked car to place where driver parked
    relation_car_parking_place[choosen_number] = the_car

    print(f'{car_color} {car_mark} {car_model} added to parking at place n°{choosen_number}')
    make_a_place_unavailable(choosen_number)
    print('******************************')
print('Welcome to "BLACK BEAST" market.\n')

continue_game = True # initialize a boolean which indicate if application continue or stop
while continue_game:
    # program interact with parking guard and display choices

    correct_choice = False
    user_choice = ''
    while not correct_choice:
        user_choice = input('What do you want to do?\n\
Choose wright number:\n\
    1- give a ticket to a driver (add a car)\n\
    2- make a place available (remove a car)\n\
    3- print availables places list\n\
    ')
        # Let's be sure that user choose a integer, and his choice is in [1:3]
        try:
            user_choice = int(user_choice)
            correct_choice = True

            if user_choice < 1 or user_choice > 3:
                correct_choice = False
                print('Make sure that you choose a number between 1 and 3')
            else:
                correct_choice = True

        except ValueError:
            print('Sorry, you must choose a number')
            correct_choice = False

    if user_choice == 1: # option 1: add a car

        # Ask car carasteristics to user
        car_ma = input('Enter the car mark: ')
        car_mo = input('Enter the car model: ')
        car_c = input('Enter the car color: ')

        # Avoid that user inputs not contain car caracteristics
        while len(car_ma) <= 0 or len(car_mo) <= 0 or len(car_c) <= 0:

            print('\nMake sure to fill in all the fields.')
            car_ma = input('Enter the car mark: ')
            car_mo = input('Enter the car model: ')
            car_c = input('Enter the car color: ')

        # If all is good admit car to parking and count it
        add_a_car(car_ma, car_mo, car_c)
        parked_car_number += 1
        correct_choice = False

    elif user_choice == 2: # option 2: remove a car
        print('List of parked cars:')
        # Display parked cars list
        for place, car in relation_car_parking_place.items():
            print(f'place n°{place}: {car}')

        '''here, we can add a try...except statement to 
        be sure that user enter correct answer
        '''
        place_wanted = int(input('Choose place you want to remove: '))

        place_of_removed_car = 0
        if place_wanted in unavailable_places:
            for place, car in relation_car_parking_place.items():
                if place == place_wanted:
                    parked_car_list.remove(car)
                    place_of_removed_car = place
                    esthetic_phrase = ' '.join(car) # Transform list in string
                    print(f'{esthetic_phrase} go out.')
            del(relation_car_parking_place[place_of_removed_car])
            make_a_place_available(place_wanted)

        else: # tell user that place number he choose is already available
            print(f'Sorry, {place_wanted} is already available.')

    else: # option 3: display available places
        know_available_places()

    # Ask if parking guard want exit the program
    exit_question = input('Do you want exit program? (Y/n)')

    if exit_question.lower() == 'y':
        continue_game = False

print('Bye bye! See you next time!')

if parked_car_number == 0:
    print(f'You didn\'t parked a car.')
elif parked_car_number == 1:
    print(f'You\'ve parked only {parked_car_number} car.')
else:
    print(f'You\'ve parked {parked_car_number} cars')
