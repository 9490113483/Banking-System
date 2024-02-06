# Banking-Systemimport java.util.*;
 class Account {
    private String accountNumber;
    private String accountHolder;
    private double balance;

    // Constructor
    public Account(String accountNumber, String accountHolder, double balance) {
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.balance = balance;
    }

    // Getters and Setters
    public String getAccountNumber() { return accountNumber; }
    public String getAccountHolder() { return accountHolder; }
    public double getBalance() { return balance; }

    // Deposit money
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Amount deposited successfully. Current Balance: " + balance);
        } else {
            System.out.println("Invalid amount");
        }
    }

    // Withdraw money
    public boolean withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
            System.out.println("Amount withdrawn successfully. Remaining Balance: " + balance);
            return true;
        } else {
            System.out.println("Insufficient balance");
            return false;
        }
    }

    @Override
    public String toString() {
        return "Account{" +
                "accountNumber='" + accountNumber + '\'' +
                ", accountHolder='" + accountHolder + '\'' +
                ", balance=" + balance +
                '}';
    }
}


public class Naveen {
    private List<Account> accounts = new ArrayList<>();
    private Scanner scanner = new Scanner(System.in);

    // Create a new Account
    public void createAccount() {
        System.out.println("Enter Account Number: ");
        String accountNumber = scanner.nextLine();
        System.out.println("Enter Account Holder Name: ");
        String accountHolder = scanner.nextLine();
        accounts.add(new Account(accountNumber, accountHolder, 0.0));
        System.out.println("Account created successfully.");
    }

    // Find an account by account number
    private Account findAccount(String accountNumber) {
        for (Account account : accounts) {
            if (account.getAccountNumber().equals(accountNumber)) {
                return account;
            }
        }
        return null;
    }

    // Deposit money
    public void deposit() {
        System.out.println("Enter Account Number: ");
        String accountNumber = scanner.nextLine();
        Account account = findAccount(accountNumber);
        if (account != null) {
            System.out.println("Enter Amount to Deposit: ");
            double amount = scanner.nextDouble();
            account.deposit(amount);
        } else {
            System.out.println("Account not found.");
        }
        scanner.nextLine(); // consume the leftover newline
    }

    // Withdraw money
    public void withdraw() {
        System.out.println("Enter Account Number: ");
        String accountNumber = scanner.nextLine();
        Account account = findAccount(accountNumber);
        if (account != null) {
            System.out.println("Enter Amount to Withdraw: ");
            double amount = scanner.nextDouble();
            account.withdraw(amount);
        } else {
            System.out.println("Account not found.");
        }
        scanner.nextLine(); // consume the leftover newline
    }

    // Main method to run the application
    public static void main(String[] args) {
        Naveen bank = new Naveen();
        boolean running = true;
        Scanner scanner = new Scanner(System.in);
        while (running) {
            System.out.println("\n---Bank Management System---");
            System.out.println("1. Create Account");
            System.out.println("2. Deposit Money");
            System.out.println("3. Withdraw Money");
            System.out.println("4. Exit");
            System.out.print("Enter choice: ");
            int choice = scanner.nextInt();
            switch (choice) {
                case 1:
                    bank.createAccount();
                    break;
                case 2:
                    bank.deposit();
                    break;
                case 3:
                    bank.withdraw();
                    break;
                case 4:
                    running = false;
                    break;
                default:
                    System.out.println("Invalid choice, please enter 1-4.");
            }
        }
    }
}
