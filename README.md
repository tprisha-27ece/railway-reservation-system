# railway-reservation-system
Simple Railway Reservation System in Java

import java.util.*;

class Passenger {
    int id;
    String name;
    int seatNumber;

    Passenger(int id, String name, int seatNumber) {
        this.id = id;
        this.name = name;
        this.seatNumber = seatNumber;
    }
}

public class RailwayReservationSystem {

    static int totalSeats = 5;
    static List<Integer> availableSeats = new ArrayList<>();
    static List<Passenger> bookedPassengers = new ArrayList<>();
    static int idCounter = 1;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Initialize seats
        for (int i = 1; i <= totalSeats; i++) {
            availableSeats.add(i);
        }

        while (true) {
            System.out.println("\n===== Railway Reservation System =====");
            System.out.println("1. Book Ticket");
            System.out.println("2. Cancel Ticket");
            System.out.println("3. View Available Seats");
            System.out.println("4. View Booked Passengers");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            int choice = sc.nextInt();
            sc.nextLine(); // consume newline

            switch (choice) {
                case 1:
                    bookTicket(sc);
                    break;
                case 2:
                    cancelTicket(sc);
                    break;
                case 3:
                    viewAvailableSeats();
                    break;
                case 4:
                    viewPassengers();
                    break;
                case 5:
                    System.out.println("Thank you!");
                    return;
                default:
                    System.out.println("Invalid choice!");
            }
        }
    }

    static void bookTicket(Scanner sc) {
        if (availableSeats.isEmpty()) {
            System.out.println("No seats available!");
            return;
        }

        System.out.print("Enter passenger name: ");
        String name = sc.nextLine();

        int seat = availableSeats.remove(0); // assign first available seat
        Passenger p = new Passenger(idCounter++, name, seat);
        bookedPassengers.add(p);

        System.out.println("Ticket booked successfully!");
        System.out.println("Passenger ID: " + p.id);
        System.out.println("Seat Number: " + p.seatNumber);
    }

    static void cancelTicket(Scanner sc) {
        System.out.print("Enter Passenger ID to cancel: ");
        int id = sc.nextInt();

        for (Passenger p : bookedPassengers) {
            if (p.id == id) {
                availableSeats.add(p.seatNumber);
                bookedPassengers.remove(p);
                System.out.println("Ticket cancelled successfully!");
                return;
            }
        }

        System.out.println("Passenger not found!");
    }

    static void viewAvailableSeats() {
        System.out.println("Available Seats: " + availableSeats);
    }

    static void viewPassengers() {
        if (bookedPassengers.isEmpty()) {
            System.out.println("No bookings yet.");
            return;
        }

        System.out.println("\nBooked Passengers:");
        for (Passenger p : bookedPassengers) {
            System.out.println("ID: " + p.id + " | Name: " + p.name + " | Seat: " + p.seatNumber);
        }
    }
}
