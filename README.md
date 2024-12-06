# COP-2334-1-Module-15-Final-Group-Project
This is a GitHub repository link for the Final Group Programming Project from Module 15 created by Carlos Gonzalez and Amari Wellington.

// This program is used to calculate the total shipping cost of a package through a FedEx shipping system.

#include <iostream> // Used for cin and cout
#include <string> // Used for string variables
#include <iomanip> // Used for setprecision
using namespace std; // Allows all standard library items to be used.

class Package { // Defines the class Package.
protected: // Protected variables.
    // Strings for the sender's details (name, address, city, state, and ZIP Code).
    string senderName, senderAddress, senderCity, senderState, senderZip;
    // Recipient's details (name, address, city, state, and ZIP Code).
    string recipientName, recipientAddress, recipientCity, recipientState, recipientZip;
    double weight, costPerOunce; // Package weight and cost per ounce.
public: // Public variables.
    // initialize package details for the sender and recipient information.
    Package(string sender, string senderAddr, string senderCity, string senderState, string senderZip,
            string recipient, string recipientAddr, string recipientCity, string recipientState, string recipientZip,
            double w, double cpo)
        : senderName(sender), senderAddress(senderAddr), senderCity(senderCity), senderState(senderState), senderZip(senderZip), // Sender's details and Constructor.
          recipientName(recipient), recipientAddress(recipientAddr), recipientCity(recipientCity), recipientState(recipientState), recipientZip(recipientZip), // Recipient's details.
          weight(w > 0 ? w : 0), costPerOunce(cpo > 0 ? cpo : 0) {} // Sets the weight and cost per ounce to 0 if negative.
    double calculateCost() const { // Calculates the cost of the package.
        return weight * costPerOunce; // Returns the cost of the package.
    }
    void display() const { // Displays the package details.
        cout << fixed << setprecision(2); // Sets two decimal places.
        cout << "Sender: " << senderName << "\nAddress: " << senderAddress << ", " << senderCity << ", " << senderState << " " << senderZip << endl; // Displays the sender's information.
        cout << "Recipient: " << recipientName << "\nAddress: " << recipientAddress << ", " << recipientCity << ", " << recipientState << " " << recipientZip << endl; // Displays the recipient's information.
        cout << "Weight: " << weight << " oz | Cost per ounce: $" << costPerOunce << endl; // Displays the weight and cost per ounce.
        cout << "Total Cost: $" << calculateCost() << endl; // Total cost of the package.
    } // end of display function
}; // end of class Package.

class TwoDayPackage : public Package { // Defines the class TwoDayPackage.
    double flatFee;  // Displays the flat fee for TwoDay delivery.
public: // Public variables.
    TwoDayPackage(string sender, string senderAddr, string senderCity, string senderState, string senderZip, // Sets the sender's information.
                  string recipient, string recipientAddr, string recipientCity, string recipientState, string recipientZip,
                  double w, double cpo, double fee) // Sets the recipient's information.
        : Package(sender, senderAddr, senderCity, senderState, senderZip, recipient, recipientAddr, recipientCity, recipientState, recipientZip, w, cpo), flatFee(fee > 0 ? fee : 0) {} // Sets the flat fee to 0 if negative.
    double calculateCost() const { // Calculates the cost of the package.
        return Package::calculateCost() + flatFee; // Returns the cost of the package.
    } // end of calculateCost function.
    void display() const { // Displays the two-day package details and flat fee.
        cout << "--- Two-Day Package ---" << endl; // Prints the two-day package details.
        Package::display();  // Displays the base package information.
        cout << "Flat fee for two-day delivery: $" << flatFee << endl; // Prints the flat fee for two-day delivery.
        cout << "Total Cost (with flat fee): $" << calculateCost() << endl; // Prints the total cost of the package.
    } // end of display function.
}; // end of class TwoDayPackage.

class OvernightPackage : public Package { // Defines the class OvernightPackage.
    double additionalFeePerOunce; // Displays the additional fee per ounce for overnight delivery.
public: // Public variables.
    OvernightPackage(string sender, string senderAddr, string senderCity, string senderState, string senderZip,
                    string recipient, string recipientAddr, string recipientCity, string recipientState, string recipientZip,
                    double w, double cpo, double addFee) // Sets the sender's information.
        : Package(sender, senderAddr, senderCity, senderState, senderZip, recipient, recipientAddr, recipientCity, recipientState, recipientZip, w, cpo), additionalFeePerOunce(addFee > 0 ? addFee : 0) {} // Sets the additional fee per ounce to 0 if negative.
    double calculateCost() const { // Calculates the cost of the package.
        return weight * (costPerOunce + additionalFeePerOunce);
    } // end of calculateCost function.

    void display() const { // Displays the overnight package details and additional fee per ounce.
        cout << "--- Overnight Package ---" << endl;
        Package::display();  // Prints the overnight package information.
        cout << "Additional fee per ounce: $" << additionalFeePerOunce << endl; // Prints the additional fee per ounce.
        cout << "Total Cost (with additional fees): $" << calculateCost() << endl; // Prints the total cost of the package.
    } // end of display function.
}; // end of class OvernightPackage.

int main() { // Start of the main function.
    cout << "Hello and Welcome to your FedEx Package Delivery Service!" << endl << endl; // Prints a welcome message.
    cout << "This system will let you know how much the shipping cost will be depending on the amount of days it arrives at the recipient's doorstep." << endl << endl; // Prints the system's purpose.
    
    Package base("Amari Wellington", "123 Main St", "New York", "NY", "10001", "Carlos Gonzalez", "456 Elm St", "Los Angeles", "CA", "90001", 25, 86.62); // Creates a base package object.
    cout << "--- Base Package ---" << endl; // Prints the base package details.
    base.display(); // Displays the base package details.
    cout << endl; // Prints a blank line.
    
    TwoDayPackage twoDay("Spencer Pratt", "789 Maple Ave", "Seattle", "WA", "98101", "Phil Donahue", "321 Pine St", "Chicago", "IL", "60601", 50, 97.70, 2.75); // Creates a two-day package object.
    twoDay.display(); // Displays the two-day package details.
    cout << endl; // Prints a blank line.

    OvernightPackage overnight("Garrison Cade", "555 Oak Blvd", "Houston", "TX", "77001", "Luis Alfonso", "999 Birch Rd", "Miami", "FL", "33101", 100, 307.00, 10.30); // Creates an overnight package object.
    overnight.display(); // Displays the overnight package details.
    cout << endl; // Prints a blank line.
    return 0; // Returns 0 to indicate successful execution.
}
