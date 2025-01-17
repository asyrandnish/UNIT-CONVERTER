#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Function to convert lengths between units (m, km, cm, mm)
double convertLength(double value, string from, string to) {
    // Length conversions
    if (from == "m" && to == "km") return value / 1000;
    if (from == "m" && to == "cm") return value * 100;
    if (from == "m" && to == "mm") return value * 1000;
    if (from == "km" && to == "m") return value * 1000;
    if (from == "cm" && to == "m") return value / 100;
    if (from == "mm" && to == "m") return value / 1000;
    // Add more conversions as needed
    return value; // Return the original value if no conversion match
}

// Function to convert mass between units (kg, g, mg)
double convertMass(double value, string from, string to) {
    // Mass conversions
    if (from == "kg" && to == "g") return value * 1000;
    if (from == "g" && to == "kg") return value / 1000;
    if (from == "kg" && to == "mg") return value * 1000000;
    if (from == "mg" && to == "kg") return value / 1000000;
    // Add more conversions as needed
    return value; // Return the original value if no conversion match
}

// Function to convert temperatures between units (Celsius, Fahrenheit, Kelvin)
double convertTemperature(double value, string from, string to) {
    // Temperature conversions
    if (from == "Celsius" && to == "Fahrenheit") return (value * 9 / 5) + 32;
    if (from == "Celsius" && to == "Kelvin") return value + 273.15;
    if (from == "Fahrenheit" && to == "Celsius") return (value - 32) * 5 / 9;
    if (from == "Fahrenheit" && to == "Kelvin") return (value - 32) * 5 / 9 + 273.15;
    if (from == "Kelvin" && to == "Celsius") return value - 273.15;
    if (from == "Kelvin" && to == "Fahrenheit") return (value - 273.15) * 9 / 5 + 32;
    // Add more conversions as needed
    return value; // Return the original value if no conversion match
}

// Main function for running the conversion program
int main() {
    vector<string> savedConversions; // List to store saved conversions
    int choice;
    
   do {
        // Displaying the menu options
        cout << "\nUnit Conversion Program" << endl;
        cout << "1. Length Conversion" << endl;
        cout << "2. Mass Conversion" << endl;
        cout << "3. Temperature Conversion" << endl;
        cout << "4. Show Saved Conversions" << endl;
        cout << "5. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;
        
  double value;
  string fromUnit, toUnit;
        
  // Switch case to handle different types of conversions
        switch (choice) {
            case 1: // Length Conversion
                cout << "Enter the length value: ";
                cin >> value;
                cout << "Enter unit to convert from (m, km, cm, mm): ";
                cin >> fromUnit;
                cout << "Enter unit to convert to (m, km, cm, mm): ";
                cin >> toUnit;
                cout << "Converted value: " << convertLength(value, fromUnit, toUnit) << endl;
                savedConversions.push_back(fromUnit + " to " + toUnit); // Save conversion
                break;
            
  case 2: // Mass Conversion
                cout << "Enter the mass value: ";
                cin >> value;
                cout << "Enter unit to convert from (kg, g, mg): ";
                cin >> fromUnit;
                cout << "Enter unit to convert to (kg, g, mg): ";
                cin >> toUnit;
                cout << "Converted value: " << convertMass(value, fromUnit, toUnit) << endl;
                savedConversions.push_back(fromUnit + " to " + toUnit); // Save conversion
                break;
                
  case 3: // Temperature Conversion
                cout << "Enter the temperature value: ";
                cin >> value;
                cout << "Enter unit to convert from (Celsius, Fahrenheit, Kelvin): ";
                cin >> fromUnit;
                cout << "Enter unit to convert to (Celsius, Fahrenheit, Kelvin): ";
                cin >> toUnit;
                cout << "Converted value: " << convertTemperature(value, fromUnit, toUnit) << endl;
                savedConversions.push_back(fromUnit + " to " + toUnit); // Save conversion
                break;
                
  case 4: // Show Saved Conversions
                cout << "Saved conversions: " << endl;
                for (const string& conversion : savedConversions) {
                    cout << conversion << endl;
                }
                break;
                
  case 5: // Exit the program
                cout << "Exiting program." << endl;
                break;
                
  default:
                cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 5); // Loop until the user chooses to exit
    
  return 0;
}
