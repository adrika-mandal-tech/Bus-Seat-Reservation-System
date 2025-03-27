# Bus-Seat-Reservation-System
/*                                Project 1 - BUS SEAT RESERVATION SYSTEM
This is a simple and clear project that displays the implementation of class alongside the object of C++Programminglanguage. 
You are to create this project in a way to make users be able to install bus information, reserve bus seat, 
display reservation information, and receive information about buses that are available.
Write functions to:
1. Create a bus route with
• Bus number
• Driver name 
• Departure time & Arrival time
• From & To
2. Take in reservations with:
• Bus number
• Seat number
• Passenger name
3. Display the seats in a bus for given number
• Show all 32 seats with seat number and passenger name if booked
4. Show available busses
• Print bus details in a table format
5. Exit      */
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

#include <iostream>
#include <string>
#include <vector> // Standard Template Library --->> Dynamic Size
using namespace std;
// Class to represent a bus
class Bus {
public:
    int busNumber;
    string driverName;
    string arrivalTime;
    string departureTime;
    string from;
    string to;
    vector<string> passengers; // To store passenger names for each seat
// Constructor
    Bus(int busNumber, string driverName, string arrivalTime, string departureTime, string from, string to) {
        this->busNumber = busNumber;
        this->driverName = driverName;
        this->arrivalTime = arrivalTime;
        this->departureTime = departureTime;
        this->from = from;
        this->to = to;
        this->passengers = vector<string>(32, ""); } // Initialize all seats as empty    
// Function to check if a seat is available
    bool isSeatAvailable(int seatNumber) const {
        return passengers[seatNumber - 1] == "";    }
// Function to reserve a seat
    void reserveSeat(int seatNumber, string passengerName) {
        if (seatNumber < 1 || seatNumber > 32) {
            cout << "Invalid seat number. Please enter a seat number between 1 and 32." << endl;
        } else if (isSeatAvailable(seatNumber)) {
            passengers[seatNumber - 1] = passengerName;
            cout << "Seat " << seatNumber << " reserved for " << passengerName << endl;
        } else {
            cout << "Seat " << seatNumber << " is already booked." << endl;    } }
// Function to display seat information (marked as const)
    void displaySeats() const {
        cout << "Bus Number: " << busNumber << endl;
        for (int i = 0; i < 32; i++) {
            cout << "Seat " << i + 1 << ": ";
            if (passengers[i] != "") {
                cout << passengers[i] << endl;
            } else {
                cout << "Available" << endl;    }    }    }     };
// Function to create a new bus route
Bus createBusRoute() {
    int busNumber;
    string driverName, arrivalTime, departureTime, from, to;
    cout << "Enter Bus Number: ";
    cin >> busNumber;
    cout << "Enter Driver Name: ";
    cin >> driverName;
    cout << "Enter Arrival Time: ";
    cin >> arrivalTime;
    cout << "Enter Departure Time: ";
    cin >> departureTime;
    cout << "Enter From: ";
    cin >> from;
    cout << "Enter To: ";
    cin >> to;
    Bus newBus(busNumber, driverName, arrivalTime, departureTime, from, to);
    return newBus;  }
// Function to reserve a seat in a bus
void reserveSeat(vector<Bus>& buses) {
    int busNumber, seatNumber;
    string passengerName;
    cout << "Enter Bus Number: ";
    cin >> busNumber;
    cout << "Enter Seat Number: ";
    cin >> seatNumber;
    cout << "Enter Passenger Name: ";
    cin >> passengerName;
    for (Bus& bus : buses) {
        if (bus.busNumber == busNumber) {
            bus.reserveSeat(seatNumber, passengerName);
            return;    }    }
    cout << "Bus not found." << endl;  }
// Function to display seat information for a bus
void displaySeats(const vector<Bus>& buses) {
    int busNumber;
    cout << "Enter Bus Number: ";
    cin >> busNumber;
    for (const Bus& bus : buses) {
        if (bus.busNumber == busNumber) {
            bus.displaySeats(); // This call now works because `displaySeats` is constant
            return;    }    }
    cout << "Bus not found." << endl;  }
// Function to display available buses
void displayAvailableBuses(const vector<Bus>& buses) {
    cout << "Available Buses:" << endl;
    cout << "Bus Number\tDriver\tArrival\tDeparture\tFrom\tTo" << endl;
    for (const Bus& bus : buses) {
        cout << bus.busNumber << "\t\t" << bus.driverName << "\t" << bus.arrivalTime << 
        "\t" << bus.departureTime << "\t"
        << bus.from << "\t" << bus.to << endl;    } }
int main() {
    vector<Bus> buses;
    int choice;
    do {
        cout << "\nSeat Reservation System" << endl;
        cout << "1. Create Bus Route" << endl;
        cout << "2. Reserve Seat(from 1 to 32)" << endl;
        cout << "3. Display Seats" << endl;
        cout << "4. Show Available Buses" << endl;
        cout << "5. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;
        switch (choice) {
            case 1:
                buses.push_back(createBusRoute());
                break;
            case 2:
                reserveSeat(buses);
                break;
            case 3:
                displaySeats(buses);
                break;
            case 4:
                displayAvailableBuses(buses);
                break;
            case 5:
                cout << "Exiting..." << endl;
                break;
            default:
                cout << "Invalid choice!" << endl;    }}
         while (choice != 5);
    return 0;   }

/* Sample Output
Seat Reservation System
1. Create Bus Route
2. Reserve Seat
3. Display Seats
4. Show Available Buses
5. Exit
Enter your choice: 1

Enter Bus Number: 101
Enter Driver Name: John Doe
Enter Arrival Time: 10:00 AM
Enter Departure Time: 2:00 PM
Enter From: City A
Enter To: City B

Seat Reservation System
1. Create Bus Route
2. Reserve Seat
3. Display Seats
4. Show Available Buses
5. Exit
Enter your choice: 1

Enter Bus Number: 102
Enter Driver Name: Jane Smith
Enter Arrival Time: 3:00 PM
Enter Departure Time: 7:00 PM
Enter From: City C
Enter To: City D

Seat Reservation System
1. Create Bus Route
2. Reserve Seat
3. Display Seats
4. Show Available Buses
5. Exit
Enter your choice: 4

Available Buses:
Bus Number   Driver      Arrival    Departure   From      To
101          John Doe    10:00 AM   2:00 PM     City A    City B
102          Jane Smith  3:00 PM    7:00 PM     City C    City D

Seat Reservation System
1. Create Bus Route
2. Reserve Seat
3. Display Seats
4. Show Available Buses
5. Exit
Enter your choice: 2

Enter Bus Number: 101
Enter Seat Number: 5
Enter Passenger Name: Alice

Seat 5 reserved for Alice

Seat Reservation System
1. Create Bus Route
2. Reserve Seat
3. Display Seats
4. Show Available Buses
5. Exit
Enter your choice: 2

Enter Bus Number: 101
Enter Seat Number: 5
Enter Passenger Name: Bob

Seat 5 is already booked.

Seat Reservation System
1. Create Bus Route
2. Reserve Seat
3. Display Seats
4. Show Available Buses
5. Exit
Enter your choice: 3

Enter Bus Number: 101
Bus Number: 101
Seat 1: Available
Seat 2: Available
Seat 3: Available
Seat 4: Available
Seat 5: Alice
Seat 6: Available
...
Seat 32: Available

Seat Reservation System
1. Create Bus Route
2. Reserve Seat
3. Display Seats
4. Show Available Buses
5. Exit
Enter your choice: 5

Exiting...*/


































































