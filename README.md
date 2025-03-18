# Banking System in C++

## Overview
This is a simple Banking System implemented in C++ that allows users to create bank accounts, deposit and withdraw money, check balances, and close accounts. The system stores account information using file handling.

## Features
- Open a new bank account
- Check account balance
- Deposit funds into an account
- Withdraw funds from an account (minimum balance enforced)
- Close an account
- Show all existing accounts
- Persistent storage using file handling (`Bank.data`)

## Requirements
- C++ compiler (e.g., g++)

## How to Compile and Run
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/banking-system.git
   cd banking-system
   ```
2. Compile the program:
   ```bash
   g++ banking_system.cpp -o banking_system
   ```
3. Run the program:
   ```bash
   ./banking_system
   ```

## Usage
1. Run the program and select an option from the menu.
2. Follow the on-screen instructions to perform banking operations.
3. Data is automatically saved to `Bank.data` file.

## Code Explanation
```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <vector>
#include <map>
using namespace std;

#define MIN_BALANCE 500

class InsufficientFunds {};

class Account {
private:
    long accountNumber;
    string firstName;
    string lastName;
    float balance;
    static long NextAccountNumber;

public:
    Account() {}
    Account(string fname, string lname, float balance);
    long getAccNo() { return accountNumber; }
    string getFirstName() { return firstName; }
    string getLastName() { return lastName; }
    float getBalance() { return balance; }
    void Deposit(float amount);
    void Withdraw(float amount);
    static void setLastAccountNumber(long accountNumber);
    static long getLastAccountNumber();
    friend ofstream &operator<<(ofstream &ofs, Account &acc);
    friend ifstream &operator>>(ifstream &ifs, Account &acc);
    friend ostream &operator<<(ostream &os, Account &acc);
};

long Account::NextAccountNumber = 0;

class Bank {
private:
    map<long, Account> accounts;

public:
    Bank();
    Account OpenAccount(string fname, string lname, float balance);
    Account BalanceEnquiry(long accountNumber);
    Account Deposit(long accountNumber, float amount);
    Account Withdraw(long accountNumber, float amount);
    void CloseAccount(long accountNumber);
    void ShowAllAccounts();
    ~Bank();
};
``` 

## Future Enhancements
- Implement authentication (PIN/password-based security)
- Enhance file handling for better efficiency
- Introduce more banking operations (loans, interest calculation, etc.)

