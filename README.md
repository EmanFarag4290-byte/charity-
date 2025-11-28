# charity-
a code for a charity using Java OOP
 import java.util.Scanner;
import java.util.ArrayList;

// Parent Class: Charity
class Charity {
    private String charityName;
    private String charityAddress;

    // Constructor
    public Charity(String charityName, String charityAddress) {
        this.charityName = charityName;
        this.charityAddress = charityAddress;
    }

    // Encapsulation: Getters and Setters
    public String getCharityName() {
        return charityName;
    }

    public void setCharityName(String charityName) {
        this.charityName = charityName;
    }

    public String getCharityAddress() {
        return charityAddress;
    }

    public void setCharityAddress(String charityAddress) {
        this.charityAddress = charityAddress;
    }

    // Display Charity Details
    public void displayCharityDetails() {
        System.out.println("Charity Name: " + charityName);
        System.out.println("Charity Address: " + charityAddress);
    }
}

// Child Class: Donor
class Donor extends Charity {
    private String donorName;
    private double totalDonations;
    private ArrayList<String> donatedItems; 

    // Constructor
    public Donor(String charityName, String charityAddress, String donorName) {
        super(charityName, charityAddress); // Call to Parent Constructor
        this.donorName = donorName;
        this.totalDonations = 0.0;
        this.donatedItems = new ArrayList<>();
    }

    // Method Overloading: Accept Donation (Money)
    public void donate(double amount) {
        totalDonations += amount;
        System.out.println("Thank you, " + donorName + "! You donated $" + amount);
    }

    // Method Overloading: Accept Donation (Items)
    public void donate(String item) {
        donatedItems.add(item);
        System.out.println("Thank you, " + donorName + "! You donated an item: " + item);
    }

    // Method Overriding: Display Donor Details
    @Override
    public void displayCharityDetails() {
        super.displayCharityDetails(); // Call Parent Method
        System.out.println("Donor Name: " + donorName);
        System.out.println("Total Monetary Donations: $" + totalDonations);
        System.out.println("Donated Items: " + (donatedItems.isEmpty() ? "None" : String.join(", ", donatedItems)));
    }
}

// Main Class
public class CharityManagementSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Create Charity
        Charity myCharity = new Charity("Helping Hands", "123 Main Street");
        System.out.println("Welcome to the Charity Management System!");
        myCharity.displayCharityDetails();
        System.out.println();

        // Get Donor Details
        System.out.print("Enter your name to register as a donor: ");
        String donorName = scanner.nextLine();
        Donor donor = new Donor(myCharity.getCharityName(), myCharity.getCharityAddress(), donorName);

        // Donation Menu
        boolean keepDonating = true;
        while (keepDonating) {
            System.out.println("\nDonation Menu:");
            System.out.println("1. Donate Money");
            System.out.println("2. Donate Item");
            System.out.println("3. View Donor Details");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter the amount to donate: $");
                    double amount = scanner.nextDouble();
                    scanner.nextLine(); // Consume newline
                    donor.donate(amount);
                    break;

                case 2:
                    System.out.print("Enter the name of the item to donate: ");
                    String item = scanner.nextLine();
                    donor.donate(item);
                    break;

                case 3:
                    System.out.println("\n--- Donor Details ---");
                    donor.displayCharityDetails();
                    break;

                case 4:
                    System.out.println("Thank you for your support! Goodbye!");
                    keepDonating = false;
                    break;

                default:
                    System.out.println("Invalid choice! Please try again.");
            }
        }

        scanner.close();
    }
}
