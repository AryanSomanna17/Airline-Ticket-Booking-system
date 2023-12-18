#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_PASSENGERS 10

// Struct to store passenger information
typedef struct {
    char name[50];
    int age;
    int isVIP;
    int isBooked;
    int isFlyingWithKid;
    int hasDisability;
} Passenger;

Passenger passengers[MAX_PASSENGERS];
int numPassengers = 0;

// Function to add a new passenger
void addPassenger() {
    if (numPassengers < MAX_PASSENGERS) {
        Passenger newPassenger;
printf("Enter passenger name: ");
scanf("%s", newPassenger.name);
printf("Enter passenger age: ");
scanf("%d", &newPassenger.age);

        if (newPassenger.age< 18) {
printf("Sorry, passengers under the age of 18 are not allowed to book.\n");
            return;  // Exit the function without adding the passenger
        }

printf("Is the passenger flying with a kid (1 for yes, 0 for no): ");
scanf("%d", &newPassenger.isFlyingWithKid);
printf("Is the passenger a VIP (1 for yes, 0 for no): ");
scanf("%d", &newPassenger.isVIP);
printf("Does the passenger have a disability (1 for yes, 0 for no): "); // New input
scanf("%d", &newPassenger.hasDisability); // New field

newPassenger.isBooked = 0;
        passengers[numPassengers] = newPassenger;
        numPassengers++;
printf("Passenger added successfully.\n");
    } 
else {
printf("Sorry, the passenger list is full.\n");
    }
}

// Function to display the passenger list
void displayPassengerList() {
printf("\nPassenger List:\n");
    for (int i = 0; i < numPassengers; i++) {
printf("Name: %s, Age: %d, VIP: %s, Flying with Kid: %s, Disability: %s, Status: %s\n",
               passengers[i].name, passengers[i].age,
               passengers[i].isVIP ? "Yes" : "No",
               passengers[i].isFlyingWithKid ? "Yes" : "No",
               passengers[i].hasDisability ? "Yes" : "No", // Display disability status
               passengers[i].isBooked ? "Booked" : "Not Booked");
    }
printf("\n");
}

// Function to book passengers based on priority and age
void bookPassengers() {

    // Book VIP pwd
    for (int i = 0; i < numPassengers; i++) {
        if (!passengers[i].isBooked&& passengers[i].hasDisability&& passengers[i].isVIP) 
        {
            passengers[i].isBooked = 1;
printf("Passenger %s has been booked (PWD, VIP).\n", passengers[i].name);
        }
    }

    // Book Non VIPpwd
    for (int i = 0; i < numPassengers; i++) {
        if (!passengers[i].isBooked&& passengers[i].hasDisability&& !passengers[i].isVIP) 
        {
            passengers[i].isBooked = 1;
printf("Passenger %s has been booked (PWD, Non-VIP).\n", passengers[i].name);
        }
    }   

    // Book VIP passengers above 60
    for (int i = 0; i < numPassengers; i++) {
        if (!passengers[i].isBooked&& passengers[i].age > 60 && passengers[i].isVIP)
        {
            passengers[i].isBooked = 1;
printf("Passenger %s has been booked (Above 60, VIP).\n", passengers[i].name);

        }
    }

    // Book Non VIP passengers above 60
    for (int i = 0; i < numPassengers; i++) {
        if (!passengers[i].isBooked&& passengers[i].age > 60 && !passengers[i].isVIP)
        {
            passengers[i].isBooked = 1;
printf("Passenger %s has been booked (Above 60, Non-VIP).\n", passengers[i].name);

        }
    }

    // Book VIP passengers flying with kids
    for (int i = 0; i < numPassengers; i++) {
        if (!passengers[i].isBooked&& passengers[i].isFlyingWithKid&& passengers[i].isVIP) 
        {
            passengers[i].isBooked = 1;
printf("Passenger %s has been booked (Flying with Kid, VIP).\n", passengers[i].name);

        }
    }

    // Book Non VIP passengers flying with kids
   for (int i = 0; i < numPassengers; i++) {
        if (!passengers[i].isBooked&& passengers[i].isFlyingWithKid&& !passengers[i].isVIP) 
        {
            passengers[i].isBooked = 1;
printf("Passenger %s has been booked (Flying with Kid, Non-VIP).\n", passengers[i].name);
        }
    }   
    // Book regular VIP passengers
    for (int i = 0; i < numPassengers; i++) {
        if (passengers[i].isVIP&& !passengers[i].isBooked) 
        {
            passengers[i].isBooked = 1;
printf("Passenger %s has been booked (Regular VIP).\n", passengers[i].name);

        }
    }
    // Book regular non-VIP passengers
    for (int i = 0; i < numPassengers; i++) {
        if (!passengers[i].isVIP&& !passengers[i].isBooked) 
        {
            passengers[i].isBooked = 1;
printf("Passenger %s has been booked (Regular Non-VIP).\n", passengers[i].name);
        }
    }
}




int main() {
    int choice;
    do {
printf("\n\nAirline Ticket Reservation System\n");
printf("1. Add Passenger\n");
printf("2. Display Passenger List\n");
printf("3. Book Passengers\n");
printf("4. Quit\n");
printf("Enter your choice: ");
scanf("%d", &choice);
        switch (choice) {
            case 1:
                addPassenger();
                break;
            case 2:
                displayPassengerList();
                break;
            case 3:
                bookPassengers();
                break;
            case 4:
printf("Exiting the program. Goodbye!\n");
                break;
            default:
printf("Invalid choice. Please try again.\n");
        }
    } while (choice != 4);
    return 0;

