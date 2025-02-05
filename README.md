# user-authentication-system-using-c-
#include <iostream>
#include <string>
#include <unordered_map>

using namespace std;


unordered_map<string, string> users = {
    {"kamal", "password123"},
    {"vivek", "12"}
};


string generateOTP() { 
    string otp = "";
    for (int i = 0; i < 6; i++) {
        otp += to_string(rand() % 10); 
    }
    return otp;
}	


bool authenticate(string username, string password) {
    auto it = users.find(username);
    if (it != users.end() && it->second == password) {
        return true;
    }
    return false;
}

int main() {
    string username, password, enteredOTP;
    cout << "Enter username: ";
    cin >> username;
    cout << "Enter password: ";
    cin >> password;

    if (!authenticate(username, password)) {
        cout << "Invalid credentials! Access Denied.\n";
        return 1;
    }

    
    string otp = generateOTP();
    cout << "\n[OTP sent to your registered email/phone: " << otp << "]\n"; 

    cout << "Enter OTP: ";
    cin >> enteredOTP;


    if (enteredOTP == otp) {
        cout << "✅ Authentication Successful! Access Granted.\n";
    } else {
        cout << "❌ Invalid OTP! Access Denied.\n";
    }

    return 0;
}
