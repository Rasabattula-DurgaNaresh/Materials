# Java Complete Tutorial — Basic to Advanced
### From Hello World to Production-Grade Patterns

> **Coverage:** Java 8–21 | OOP | Collections | Streams | Concurrency | Design Patterns | Spring Boot | Real-World Scenarios

---

## Table of Contents

| # | Topic | Level |
|---|-------|-------|
| 1 | [Java Basics — Syntax, Variables, Data Types](#1-java-basics) | 🟢 Basic |
| 2 | [Operators & Control Flow](#2-operators--control-flow) | 🟢 Basic |
| 3 | [Arrays & Strings](#3-arrays--strings) | 🟢 Basic |
| 4 | [Object-Oriented Programming](#4-object-oriented-programming) | 🟡 Intermediate |
| 5 | [Inheritance & Polymorphism](#5-inheritance--polymorphism) | 🟡 Intermediate |
| 6 | [Interfaces & Abstract Classes](#6-interfaces--abstract-classes) | 🟡 Intermediate |
| 7 | [Exception Handling](#7-exception-handling) | 🟡 Intermediate |
| 8 | [Collections Framework](#8-collections-framework) | 🟡 Intermediate |
| 9 | [Generics](#9-generics) | 🟡 Intermediate |
| 10 | [Java 8+ — Lambda, Streams, Optional](#10-java-8--lambda-streams-optional) | 🟠 Advanced |
| 11 | [Multithreading & Concurrency](#11-multithreading--concurrency) | 🟠 Advanced |
| 12 | [File I/O & NIO](#12-file-io--nio) | 🟠 Advanced |
| 13 | [Design Patterns](#13-design-patterns) | 🟠 Advanced |
| 14 | [Java Memory & JVM Internals](#14-java-memory--jvm-internals) | 🔴 Expert |
| 15 | [Real-World Spring Boot Project](#15-real-world-spring-boot-project) | 🔴 Expert |

---

## 1. Java Basics

### 1.1 Your First Java Program

```java
// HelloWorld.java
// Real-world scenario: Every Java application starts with main() entry point.
// Equivalent to Python's: if __name__ == "__main__":

public class HelloWorld {
    public static void main(String[] args) {
        // 'public'  — visible from anywhere
        // 'static'  — belongs to class, not an instance
        // 'void'    — returns nothing
        // 'args'    — command-line arguments

        System.out.println("Hello, World!");                         // with newline
        System.out.print("No newline here");                         // without newline
        System.out.printf("Name: %s, Age: %d%n", "Alice", 30);      // formatted output
    }
}
// Compile & Run: javac HelloWorld.java && java HelloWorld
```

---

### 1.2 Data Types

```java
// DataTypes.java
// Real-world: Choosing correct types prevents overflow in financial calculations

public class DataTypes {
    public static void main(String[] args) {

        // ── Primitive Types ────────────────────────────────────────────────
        byte    b  = 127;             // 8-bit  | -128 to 127         | sensor readings
        short   s  = 32767;           // 16-bit | -32,768 to 32,767   | rarely used
        int     i  = 2_147_483_647;   // 32-bit | ~2.1 billion        | counters, IDs
        long    l  = 9_999_999_999L;  // 64-bit | ~9.2 quintillion    | timestamps
        float   f  = 3.14f;           // 32-bit | ~7 decimal digits   | 3D graphics
        double  d  = 3.141592653589;  // 64-bit | ~15 decimal digits  | scientific
        char    c  = 'A';             // 16-bit | Unicode character   | text
        boolean ok = true;            // 1-bit  | true/false          | flags

        // ── Wrapper Classes ────────────────────────────────────────────────
        Integer count    = 42;        // Auto-boxing: int → Integer
        Double  price    = 9.99;      // Used in Collections, Generics
        Boolean isActive = false;

        // ── Type Casting ───────────────────────────────────────────────────
        int    x      = 100;
        long   xLong  = x;           // Implicit (widening — safe)
        double xDbl   = x;           // Implicit: int → double
        double pi     = 3.99;
        int    piInt  = (int) pi;    // Explicit (narrowing — truncates to 3, NOT rounded)

        // ── Overflow (common bug in financial systems) ─────────────────────
        int maxInt   = Integer.MAX_VALUE;  // 2,147,483,647
        int overflow = maxInt + 1;         // -2,147,483,648 ← BUG! Use long

        // ── Underscores in literals (Java 7+) ─────────────────────────────
        long creditCard = 1234_5678_9012_3456L;
        int  binary     = 0b1010_0101;
        int  hex        = 0xFF_A0_12;

        System.out.println("int max  : " + Integer.MAX_VALUE);
        System.out.println("overflow : " + overflow);
        System.out.println("pi cast  : " + piInt);
    }
}
```

---

### 1.3 Variables — var, final, static

```java
// Variables.java
// Real-world: ATM machine balance tracking

public class Variables {
    static int totalTransactions = 0;         // class-level: shared by all instances
    double     balance;                        // instance-level: each object has own copy
    final double WITHDRAWAL_FEE = 2.50;       // constant: never changes

    public static void main(String[] args) {
        var customerName    = "Bob";           // Java 10+: infers String
        var accountBalance  = 5000.00;         // infers double
        var transactions    = new java.util.ArrayList<String>(); // infers ArrayList<String>

        final int MAX_WITHDRAWAL = 1000;       // can only be assigned once
        // MAX_WITHDRAWAL = 2000;              // ← Compile error!

        System.out.println("Customer: " + customerName);
    }
}
```

---

## 2. Operators & Control Flow

### 2.1 Operators

```java
// Operators.java
// Real-world: E-commerce order calculation

public class Operators {
    public static void main(String[] args) {

        // ── Arithmetic ────────────────────────────────────────────────────
        double price    = 199.99;
        int    quantity = 3;
        double subtotal = price * quantity;           // 599.97
        double discount = subtotal * 0.10;            // 59.997
        double total    = subtotal - discount;         // 539.973
        int    page     = 17 % 5;                     // 2 (useful for pagination)

        // ── Comparison ────────────────────────────────────────────────────
        boolean isExpensive = price > 100;            // true
        boolean isFreeShip  = total >= 500;           // true

        // ── Logical ───────────────────────────────────────────────────────
        boolean eligible    = isExpensive && isFreeShip; // AND
        boolean hasCoupon   = isExpensive || quantity > 5; // OR
        boolean notVip      = !eligible;                   // NOT

        // ── Ternary ───────────────────────────────────────────────────────
        String shipMsg = isFreeShip ? "FREE SHIPPING" : "Shipping: $9.99";

        // ── Bitwise (permissions, flags, hashing) ─────────────────────────
        int readPerm  = 0b100; // 4
        int writePerm = 0b010; // 2
        int userPerm  = readPerm | writePerm;          // 6 (read + write)
        boolean canRead = (userPerm & readPerm) != 0;  // true

        // ── Shift operators (fast multiply/divide by 2) ────────────────────
        int doubled = 8 << 1;   // 16  (8 * 2)
        int halved  = 8 >> 1;   // 4   (8 / 2)

        System.out.printf("Total: %.2f%n", total);
        System.out.println(shipMsg);
    }
}
```

---

### 2.2 Control Flow

```java
// ControlFlow.java
// Real-world: Bank transaction processing

public class ControlFlow {

    // ── if / else if / else ──────────────────────────────────────────────
    static String getStatus(double amount, double balance) {
        if (amount <= 0)           return "INVALID: Amount must be positive";
        else if (amount > balance) return "DECLINED: Insufficient funds";
        else if (amount > 10000)   return "PENDING: Requires approval";
        else                       return "APPROVED";
    }

    // ── Switch Expression (Java 14+) — clean, returns value ──────────────
    static String getAccountType(String code) {
        return switch (code) {
            case "SAV" -> "Savings Account";
            case "CHK" -> "Checking Account";
            case "LON" -> "Loan Account";
            default    -> "Unknown: " + code;
        };
    }

    public static void main(String[] args) {
        double[] transactions = {500, -200, 1500, -300, 800};
        double   balance      = 0;

        // ── for loop ─────────────────────────────────────────────────────
        for (int i = 0; i < transactions.length; i++) {
            balance += transactions[i];
            System.out.printf("Tx[%d]: %.0f  Balance: %.0f%n", i+1, transactions[i], balance);
        }

        // ── enhanced for (for-each) — preferred for collections ───────────
        for (double tx : transactions) {
            System.out.println(tx > 0 ? "CREDIT: " + tx : "DEBIT: " + Math.abs(tx));
        }

        // ── while loop ───────────────────────────────────────────────────
        double currentBalance = 1000;
        int    month = 1;
        while (currentBalance > 100) {
            currentBalance -= 150;
            System.out.printf("Month %d: %.0f%n", month++, currentBalance);
        }

        // ── do-while — always runs at least once (e.g., PIN entry) ───────
        int pinAttempts = 0;
        do {
            System.out.println("PIN attempt " + ++pinAttempts);
        } while (pinAttempts < 3);

        // ── break and continue ────────────────────────────────────────────
        for (int i = 1; i <= 10; i++) {
            if (i % 2 == 0) continue;   // skip even
            if (i > 7)      break;       // stop
            System.out.print(i + " ");   // prints: 1 3 5 7
        }

        // ── Labeled break (exit nested loops) ─────────────────────────────
        outer:
        for (int row = 0; row < 3; row++) {
            for (int col = 0; col < 3; col++) {
                if (row == 1 && col == 1) {
                    System.out.println("\nFound at [" + row + "][" + col + "]");
                    break outer;
                }
            }
        }
    }
}
```

---

## 3. Arrays & Strings

### 3.1 Arrays

```java
// ArraysDemo.java
// Real-world: Student grade management system

import java.util.Arrays;

public class ArraysDemo {
    public static void main(String[] args) {

        // ── 1D Array ──────────────────────────────────────────────────────
        int[] scores = {85, 92, 78, 95, 88};
        Arrays.sort(scores);                               // [78, 85, 88, 92, 95]
        int   idx    = Arrays.binarySearch(scores, 88);   // 2 (must be sorted first)
        int[] copy   = Arrays.copyOf(scores, 3);          // [78, 85, 88]
        int[] range  = Arrays.copyOfRange(scores, 1, 4);  // [85, 88, 92]
        Arrays.fill(new int[5], -1);                      // [-1, -1, -1, -1, -1]

        System.out.println("Sorted: " + Arrays.toString(scores));
        System.out.println("Copy  : " + Arrays.toString(copy));

        // ── 2D Array ──────────────────────────────────────────────────────
        int[][] classroom = {
            {85, 92, 78},   // Student 1: Math, Science, English
            {90, 88, 95},   // Student 2
            {70, 75, 80}    // Student 3
        };
        String[] subjects = {"Math", "Science", "English"};

        for (int s = 0; s < classroom.length; s++) {
            int total = 0;
            System.out.printf("Student %d: ", s + 1);
            for (int sub = 0; sub < classroom[s].length; sub++) {
                System.out.printf("%s=%d ", subjects[sub], classroom[s][sub]);
                total += classroom[s][sub];
            }
            System.out.printf("| Avg: %.1f%n", (double) total / subjects.length);
        }

        // ── Jagged Array (rows of different lengths) ──────────────────────
        int[][] weeklySales = new int[4][];
        weeklySales[0] = new int[]{100, 200, 150};
        weeklySales[1] = new int[]{90, 120};
        weeklySales[2] = new int[]{200, 300, 250, 180};
        weeklySales[3] = new int[]{50};
    }
}
```

---

### 3.2 Strings

```java
// StringsDemo.java
// Real-world: User profile management, form validation

public class StringsDemo {
    public static void main(String[] args) {
        String name  = "Alice Johnson";
        String email = "alice@example.com";
        String phone = "  +1-555-0100  ";

        // ── Common Methods ────────────────────────────────────────────────
        System.out.println(name.length());             // 13
        System.out.println(name.toUpperCase());        // ALICE JOHNSON
        System.out.println(phone.trim());              // +1-555-0100
        System.out.println(name.substring(0, 5));      // Alice
        System.out.println(name.contains("Johnson"));  // true
        System.out.println(name.indexOf("o"));         // 10

        // ── Replace & Split ───────────────────────────────────────────────
        String masked  = email.replaceAll("[^@]+@", "****@"); // ****@example.com
        String csv     = "Alice,30,Developer,New York";
        String[] parts = csv.split(",");
        String joined  = String.join(" | ", parts);

        // ── Comparison — ALWAYS use equals(), not == ───────────────────────
        String s1 = "hello";
        String s3 = new String("hello");
        System.out.println(s1 == s3);       // false — different heap objects
        System.out.println(s1.equals(s3));  // true  — same content

        // ── Text Block (Java 15+) ─────────────────────────────────────────
        String json = """
                {
                    "name": "%s",
                    "email": "%s"
                }
                """.formatted(name, email);
        System.out.println(json);

        // ── StringBuilder — use in loops (10-100x faster than +) ──────────
        StringBuilder sb = new StringBuilder();
        String[] names = {"Alice", "Bob", "Charlie"};
        for (String n : names) sb.append(n).append(", ");
        if (sb.length() > 0) sb.setLength(sb.length() - 2); // remove trailing ", "
        System.out.println(sb);  // Alice, Bob, Charlie

        // ── Validation ────────────────────────────────────────────────────
        boolean isValidEmail = email.matches("[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}");
        boolean isBlank      = "".isBlank(); // Java 11+
        long    upperCount   = name.chars().filter(Character::isUpperCase).count();

        System.out.println("Valid email: " + isValidEmail);
        System.out.println("Uppercase letters: " + upperCount);
    }
}
```

---

## 4. Object-Oriented Programming

### 4.1 Classes, Objects, Constructors

```java
// BankAccount.java
// Real-world: Complete class design for banking system

public class BankAccount {

    private final String accountNumber;  // final: never changes after init
    private final String ownerName;
    private double  balance;
    private boolean isLocked;

    private static int    totalAccounts = 0;       // shared across all instances
    private static final double MIN_BALANCE = 100;

    // Primary constructor
    public BankAccount(String accountNumber, String ownerName, double initialDeposit) {
        if (initialDeposit < MIN_BALANCE)
            throw new IllegalArgumentException("Minimum deposit: " + MIN_BALANCE);
        this.accountNumber = accountNumber;
        this.ownerName     = ownerName;
        this.balance       = initialDeposit;
        this.isLocked      = false;
        totalAccounts++;
    }

    // Convenience constructor — delegates to primary
    public BankAccount(String ownerName, double initialDeposit) {
        this("ACC" + System.currentTimeMillis(), ownerName, initialDeposit);
    }

    // Business methods
    public boolean deposit(double amount) {
        if (isLocked || amount <= 0) return false;
        balance += amount;
        System.out.printf("[%s] Deposit: +%.2f | Balance: %.2f%n", accountNumber, amount, balance);
        return true;
    }

    public boolean withdraw(double amount) {
        if (isLocked || amount <= 0 || balance - amount < MIN_BALANCE) return false;
        balance -= amount;
        System.out.printf("[%s] Withdraw: -%.2f | Balance: %.2f%n", accountNumber, amount, balance);
        return true;
    }

    public static boolean transfer(BankAccount from, BankAccount to, double amount) {
        if (from.withdraw(amount)) { to.deposit(amount); return true; }
        return false;
    }

    // Getters
    public String getAccountNumber()  { return accountNumber; }
    public double getBalance()        { return balance; }
    public static int getTotalAccounts() { return totalAccounts; }

    @Override
    public String toString() {
        return String.format("BankAccount{acc='%s', owner='%s', balance=%.2f}",
                accountNumber, ownerName, balance);
    }

    @Override
    public boolean equals(Object o) {
        if (!(o instanceof BankAccount)) return false;
        return accountNumber.equals(((BankAccount) o).accountNumber);
    }

    @Override
    public int hashCode() { return accountNumber.hashCode(); }

    public static void main(String[] args) {
        BankAccount alice = new BankAccount("ACC001", "Alice", 5000);
        BankAccount bob   = new BankAccount("Bob", 1000);
        alice.deposit(500);
        alice.withdraw(200);
        BankAccount.transfer(alice, bob, 1000);
        System.out.println(alice);
        System.out.println(bob);
        System.out.println("Total accounts: " + BankAccount.getTotalAccounts());
    }
}
```

---

## 5. Inheritance & Polymorphism

```java
// Fleet Management System

// Base class
public class Vehicle {
    protected String make, model;
    protected int    year;
    protected double fuelLevel;  // 0.0–1.0

    public Vehicle(String make, String model, int year) {
        this.make = make; this.model = model; this.year = year; this.fuelLevel = 1.0;
    }

    public String startEngine() { return make + " " + model + " engine started"; }
    public final  String getRegistration() { return year + "-" + make + "-" + model; }

    @Override
    public String toString() {
        return String.format("%d %s %s (fuel: %.0f%%)", year, make, model, fuelLevel * 100);
    }
}

// Subclass
class Car extends Vehicle {
    private String transmission;

    public Car(String make, String model, int year, String transmission) {
        super(make, model, year);  // MUST call super first
        this.transmission = transmission;
    }

    @Override
    public String startEngine() {
        return super.startEngine() + " | " + transmission;
    }
}

// Subclass of subclass
class ElectricCar extends Car {
    private double batteryLevel;
    private int    rangeKm;

    public ElectricCar(String make, String model, int year, int rangeKm) {
        super(make, model, year, "AUTO");
        this.batteryLevel = 1.0;
        this.rangeKm      = rangeKm;
    }

    @Override
    public String startEngine() { return make + " " + model + " electric motor: silent start"; }

    public void charge(double amount) {
        batteryLevel = Math.min(1.0, batteryLevel + amount);
        System.out.printf("%s charged to %.0f%% | Range: %.0f km%n",
                model, batteryLevel * 100, batteryLevel * rangeKm);
    }
}

// Polymorphism demo
class FleetManager {
    public static void main(String[] args) {
        // Vehicle reference holds ANY subtype (polymorphism)
        Vehicle[] fleet = {
            new Car("Toyota", "Camry", 2022, "AUTO"),
            new ElectricCar("Tesla", "Model 3", 2023, 500),
            new ElectricCar("BMW", "iX", 2023, 630),
        };

        for (Vehicle v : fleet) {
            System.out.println(v.startEngine());    // calls correct override at runtime
            System.out.println("  → " + v);

            // Java 16+ pattern matching instanceof
            if (v instanceof ElectricCar ev) {
                ev.charge(0.2);                     // only ElectricCar has charge()
            }
        }
    }
}
```

---

## 6. Interfaces & Abstract Classes

```java
// Payment processing system

// Interface: defines the contract
public interface PaymentProcessor {
    boolean processPayment(double amount, String currency);    // abstract — must implement
    String  getProviderName();

    default String getReceipt(double amount, String currency) {    // optional to override
        return String.format("Receipt: %.2f %s via %s", amount, currency, getProviderName());
    }

    static boolean isValidAmount(double amount) {  // static utility (Java 8+)
        return amount > 0 && amount <= 1_000_000;
    }

    int MAX_RETRY = 3; // implicitly public static final
}

interface Refundable {
    boolean refund(String transactionId, double amount);
}

// Abstract class: partial implementation — can have constructors and state
abstract class BasePaymentGateway implements PaymentProcessor, Refundable {
    protected String apiKey;
    protected String environment;

    public BasePaymentGateway(String apiKey, String env) {
        this.apiKey = apiKey; this.environment = env;
    }

    // Concrete method — shared by all gateways
    protected void logTx(String type, double amount, boolean ok) {
        System.out.printf("[%s][%s] %s: %.2f → %s%n",
                environment, getProviderName(), type, amount, ok ? "OK" : "FAIL");
    }

    // Abstract — each gateway implements differently
    protected abstract String buildRequest(double amount, String currency);
}

// Stripe implementation
class StripeGateway extends BasePaymentGateway {
    public StripeGateway(String key) { super(key, "production"); }

    @Override public String getProviderName() { return "Stripe"; }

    @Override
    public boolean processPayment(double amount, String currency) {
        if (!PaymentProcessor.isValidAmount(amount)) return false;
        buildRequest(amount, currency);
        logTx("PAYMENT", amount, true);
        return true;
    }

    @Override
    public boolean refund(String txId, double amount) {
        logTx("REFUND", amount, true);
        return true;
    }

    @Override
    protected String buildRequest(double amount, String currency) {
        return String.format("stripe.charges.create({amount:%d,currency:'%s'})",
                (int)(amount * 100), currency.toLowerCase());
    }
}

class PaymentDemo {
    public static void main(String[] args) {
        PaymentProcessor gateway = new StripeGateway("sk_live_xxx");
        boolean ok = gateway.processPayment(99.99, "USD");
        if (ok) System.out.println(gateway.getReceipt(99.99, "USD"));
    }
}
```

---

## 7. Exception Handling

```java
// FileImportService.java
// Real-world: File processing pipeline with proper error handling

import java.io.*;
import java.util.*;

// Custom exception hierarchy
class AppException extends RuntimeException {
    private final String errorCode;
    public AppException(String code, String msg)           { super(msg); this.errorCode = code; }
    public AppException(String code, String msg, Throwable cause) { super(msg, cause); this.errorCode = code; }
    public String getErrorCode() { return errorCode; }
}

class ValidationException extends AppException {
    public ValidationException(String field, String msg) {
        super("VALIDATION_ERROR", "Field '" + field + "': " + msg);
    }
}

class UserImportService {

    // try-with-resources — auto-closes streams
    public List<String> readFile(String path) {
        try (BufferedReader reader = new BufferedReader(new FileReader(path))) {
            List<String> results = new ArrayList<>();
            String line;
            int lineNum = 0;

            while ((line = reader.readLine()) != null) {
                lineNum++;
                try {
                    results.add(validate(line, lineNum));
                } catch (ValidationException e) {
                    System.err.println("Skipping line " + lineNum + ": " + e.getMessage());
                }
            }
            return results;

        } catch (FileNotFoundException e) {
            throw new AppException("FILE_NOT_FOUND", "File not found: " + path, e);
        } catch (IOException e) {
            throw new AppException("IO_ERROR", "Cannot read: " + path, e);
        }
        // No finally needed — try-with-resources handles close()
    }

    private String validate(String line, int num) {
        if (line.isBlank()) throw new ValidationException("line_" + num, "Empty");
        String[] parts = line.split(",");
        if (parts.length != 3) throw new ValidationException("format", "Expected 3 fields");
        if (!parts[1].contains("@")) throw new ValidationException("email", "Invalid: " + parts[1]);
        return line.trim();
    }

    // Multi-catch (Java 7+)
    public void multiCatchDemo(String input) {
        try {
            int   value  = Integer.parseInt(input);
            int   result = 100 / value;
            String[] arr = {"a", "b"};
            System.out.println(arr[result]);
        } catch (NumberFormatException | ArithmeticException e) {
            System.err.println("Math/parse error: " + e.getMessage());
        } catch (ArrayIndexOutOfBoundsException e) {
            System.err.println("Array error: " + e.getMessage());
        } finally {
            System.out.println("Always runs — use for mandatory cleanup");
        }
    }

    public static void main(String[] args) {
        UserImportService svc = new UserImportService();
        try {
            svc.readFile("missing.csv");
        } catch (AppException e) {
            System.err.println("[" + e.getErrorCode() + "] " + e.getMessage());
            if (e.getCause() != null)
                System.err.println("Caused by: " + e.getCause().getClass().getSimpleName());
        }
        svc.multiCatchDemo("0");
    }
}
```

---

## 8. Collections Framework

```java
// CollectionsDemo.java
// Real-world: E-commerce inventory & order management

import java.util.*;

public class CollectionsDemo {

    static void listDemo() {
        // ArrayList: O(1) get, O(n) insert middle
        List<String> cart = new ArrayList<>();
        cart.add("Laptop"); cart.add("Mouse"); cart.add("Keyboard"); cart.add("Mouse");
        cart.add(1, "Monitor");   // insert at index
        cart.remove("Mouse");     // removes first occurrence
        cart.remove(0);           // removes by index

        // Sort
        List<Integer> nums = new ArrayList<>(Arrays.asList(5, 2, 8, 1, 9));
        Collections.sort(nums);                      // [1, 2, 5, 8, 9]
        nums.sort(Comparator.reverseOrder());         // [9, 8, 5, 2, 1]

        // Immutable (Java 9+)
        List<String> fixed = List.of("Red", "Green", "Blue");

        // LinkedList as Queue
        LinkedList<String> queue = new LinkedList<>();
        queue.offer("Order-1"); queue.offer("Order-2");
        System.out.println("Next: " + queue.poll()); // removes + returns head
    }

    static void setDemo() {
        Set<String> hashSet    = new HashSet<>();           // no order guarantee
        Set<String> linkedSet  = new LinkedHashSet<>();     // insertion order preserved
        Set<String> sortedSet  = new TreeSet<>();           // alphabetical order

        // Set operations
        Set<String> a = new HashSet<>(Arrays.asList("Java", "Python", "SQL"));
        Set<String> b = new HashSet<>(Arrays.asList("Java", "JavaScript", "SQL"));

        Set<String> intersection = new HashSet<>(a); intersection.retainAll(b); // [Java, SQL]
        Set<String> union        = new HashSet<>(a); union.addAll(b);
        Set<String> difference   = new HashSet<>(a); difference.removeAll(b);   // [Python]

        System.out.println("Intersection: " + intersection);
        System.out.println("Union       : " + union);
        System.out.println("Difference  : " + difference);
    }

    static void mapDemo() {
        Map<String, Double> inventory = new HashMap<>();
        inventory.put("Laptop", 999.99); inventory.put("Mouse", 29.99);
        inventory.put("Keyboard", 79.99);

        System.out.println("Laptop  : " + inventory.get("Laptop"));
        System.out.println("Has tab : " + inventory.containsKey("Tablet"));
        double price = inventory.getOrDefault("Tablet", 0.0); // safe access

        inventory.putIfAbsent("Mouse", 39.99);                // won't replace existing
        inventory.compute("Laptop", (k, v) -> v * 0.9);      // apply 10% discount
        inventory.forEach((item, p) -> System.out.printf("  %s → $%.2f%n", item, p));

        // Nested Map
        Map<String, Map<String, Double>> deptSalaries = new HashMap<>();
        deptSalaries.put("Engineering", new HashMap<>());
        deptSalaries.get("Engineering").put("Alice", 90000.0);
    }

    static void queueDemo() {
        // PriorityQueue: min-heap — smallest element dequeued first
        Queue<Integer> pq = new PriorityQueue<>();
        pq.offer(5); pq.offer(1); pq.offer(3);
        while (!pq.isEmpty()) System.out.print(pq.poll() + " "); // 1 3 5

        // Custom priority
        Queue<String> tasks = new PriorityQueue<>(Comparator.comparingInt(String::length));
        tasks.offer("Send email"); tasks.offer("Fix bug"); tasks.offer("Deploy");
        System.out.println("\nNext: " + tasks.poll()); // "Deploy" (shortest)

        // ArrayDeque as Stack
        Deque<String> stack = new ArrayDeque<>();
        stack.push("Page 1"); stack.push("Page 2"); stack.push("Page 3");
        System.out.println("Back: " + stack.pop()); // Page 3 (LIFO)
    }

    public static void main(String[] args) {
        listDemo(); setDemo(); mapDemo(); queueDemo();
    }
}
```

---

## 9. Generics

```java
// Generics.java
// Real-world: Generic Result wrapper and typed repository

// Generic class
public class ApiResult<T> {
    private final T       data;
    private final boolean success;
    private final String  error;
    private final int     statusCode;

    private ApiResult(T data, boolean success, String error, int code) {
        this.data = data; this.success = success; this.error = error; this.statusCode = code;
    }

    public static <T> ApiResult<T> ok(T data)               { return new ApiResult<>(data, true, null, 200); }
    public static <T> ApiResult<T> error(int code, String e){ return new ApiResult<>(null, false, e, code); }

    public boolean isSuccess() { return success; }
    public T       getData()   { return data; }

    @Override
    public String toString() {
        return success ? "OK(" + data + ")" : "ERROR[" + statusCode + ": " + error + "]";
    }
}

// Generic methods
class Utils {
    // T must implement Comparable
    public static <T extends Comparable<T>> T max(T a, T b) {
        return a.compareTo(b) >= 0 ? a : b;
    }

    // Wildcard: accept List<Integer>, List<Double>, etc.
    public static double sum(List<? extends Number> nums) {
        return nums.stream().mapToDouble(Number::doubleValue).sum();
    }

    // Lower bound: accept List<Integer> or List<Number>
    public static void addIntegers(List<? super Integer> list) {
        for (int i = 1; i <= 5; i++) list.add(i);
    }
}

// Generic repository interface
interface Repository<T, ID> {
    void    save(T entity);
    T       findById(ID id);
    List<T> findAll();
    void    delete(ID id);
}

class InMemoryRepository<T> implements Repository<T, Long> {
    private final Map<Long, T> store  = new HashMap<>();
    private long               nextId = 1;

    @Override public void    save(T e)       { store.put(nextId++, e); }
    @Override public T       findById(Long id){ return store.get(id); }
    @Override public List<T> findAll()        { return new ArrayList<>(store.values()); }
    @Override public void    delete(Long id)  { store.remove(id); }
}

class GenericsDemo {
    public static void main(String[] args) {
        ApiResult<String>  r1 = ApiResult.ok("User created");
        ApiResult<Integer> r2 = ApiResult.error(404, "Not found");
        System.out.println(r1); // OK(User created)
        System.out.println(r2); // ERROR[404: Not found]

        System.out.println(Utils.max(10, 20));          // 20
        System.out.println(Utils.max("apple", "zoo"));  // zoo

        List<Integer> ints = Arrays.asList(1, 2, 3, 4, 5);
        System.out.println("Sum: " + Utils.sum(ints));   // 15.0

        InMemoryRepository<String> repo = new InMemoryRepository<>();
        repo.save("Alice"); repo.save("Bob");
        System.out.println(repo.findAll()); // [Alice, Bob]
    }
}
```


---

## 10. Java 8+ — Lambda, Streams, Optional

```java
// Java8Features.java
// Real-world: Employee analytics dashboard

import java.util.*;
import java.util.function.*;
import java.util.stream.*;

public class Java8Features {

    record Employee(String name, String dept, double salary, int age, boolean active) {}

    static List<Employee> data() {
        return List.of(
            new Employee("Alice",   "Engineering", 95000, 32, true),
            new Employee("Bob",     "Engineering", 85000, 28, true),
            new Employee("Charlie", "Marketing",   65000, 35, false),
            new Employee("Diana",   "Engineering", 105000,40, true),
            new Employee("Eve",     "HR",          60000, 27, true),
            new Employee("Frank",   "Marketing",   72000, 45, true),
            new Employee("Grace",   "HR",          58000, 30, false)
        );
    }

    public static void main(String[] args) {
        List<Employee> employees = data();

        // ── Predicates ───────────────────────────────────────────────────
        Predicate<Employee> isActive      = Employee::active;
        Predicate<Employee> isEngineering = e -> e.dept().equals("Engineering");
        Predicate<Employee> highEarner    = e -> e.salary() > 90000;

        // Compose: AND / OR / NOT
        Predicate<Employee> activeEngHighEarner = isActive.and(isEngineering).and(highEarner);

        // ── Function<T,R> ─────────────────────────────────────────────────
        Function<Employee, String> getSummary =
            e -> e.name() + " | " + e.dept() + " | $" + e.salary();
        Function<String, String>   toUpper    = String::toUpperCase;
        Function<Employee, String> upperName  = getSummary.andThen(toUpper);

        // ── Consumer<T> ───────────────────────────────────────────────────
        Consumer<Employee> print = e ->
            System.out.printf("  %-10s %-15s $%,.0f%n", e.name(), e.dept(), e.salary());

        System.out.println("Active Engineering High Earners:");
        employees.stream().filter(activeEngHighEarner).forEach(print);

        // ── STREAMS ───────────────────────────────────────────────────────

        // filter + map + collect
        List<String> activeNames = employees.stream()
            .filter(Employee::active)
            .map(Employee::name)
            .sorted()
            .collect(Collectors.toList());
        System.out.println("\nActive: " + activeNames);

        // Statistics
        DoubleSummaryStatistics stats = employees.stream()
            .filter(Employee::active)
            .mapToDouble(Employee::salary)
            .summaryStatistics();
        System.out.printf("%nSalary stats: count=%d avg=$%,.0f max=$%,.0f min=$%,.0f%n",
            stats.getCount(), stats.getAverage(), stats.getMax(), stats.getMin());

        // Group by department
        Map<String, List<Employee>> byDept = employees.stream()
            .collect(Collectors.groupingBy(Employee::dept));
        byDept.forEach((dept, emps) -> {
            double avg = emps.stream().mapToDouble(Employee::salary).average().orElse(0);
            System.out.printf("  %-15s count=%d avgSal=$%,.0f%n", dept, emps.size(), avg);
        });

        // Average salary per department
        Map<String, Double> avgByDept = employees.stream()
            .collect(Collectors.groupingBy(
                Employee::dept,
                Collectors.averagingDouble(Employee::salary)));

        // Partition by active/inactive
        Map<Boolean, List<Employee>> partition = employees.stream()
            .collect(Collectors.partitioningBy(Employee::active));
        System.out.println("Active: " + partition.get(true).size());
        System.out.println("Inactive: " + partition.get(false).size());

        // Total payroll
        double payroll = employees.stream()
            .filter(Employee::active)
            .mapToDouble(Employee::salary)
            .reduce(0, Double::sum);
        System.out.printf("Total payroll: $%,.0f%n", payroll);

        // flatMap — flatten nested lists
        List<List<String>> nested = List.of(
            List.of("Java", "Spring"),
            List.of("Python", "Django"),
            List.of("SQL", "MongoDB")
        );
        List<String> allSkills = nested.stream()
            .flatMap(Collection::stream)
            .distinct().sorted()
            .collect(Collectors.toList());
        System.out.println("Skills: " + allSkills);

        // ── OPTIONAL ─────────────────────────────────────────────────────
        Optional<Employee> alice = employees.stream()
            .filter(e -> e.name().equals("Alice"))
            .findFirst();

        String dept = alice.map(Employee::dept).orElse("Unknown");
        alice.ifPresentOrElse(
            e  -> System.out.println("Found: " + e.name()),
            () -> System.out.println("Not found")
        );

        // Chain optionals safely
        Optional<String> upperDept = alice
            .filter(Employee::active)
            .map(Employee::dept)
            .map(String::toUpperCase);
        System.out.println("Dept: " + upperDept.orElse("N/A"));

        // ── PARALLEL STREAM ────────────────────────────────────────────────
        // Use for large datasets on multi-core machines
        double totalParallel = employees.parallelStream()
            .mapToDouble(Employee::salary)
            .sum();
        System.out.printf("Parallel sum: $%,.0f%n", totalParallel);
    }
}
```

---

## 11. Multithreading & Concurrency

```java
// ConcurrencyDemo.java
// Real-world: Async order processing system

import java.util.concurrent.*;
import java.util.concurrent.atomic.*;
import java.util.*;

public class ConcurrencyDemo {

    // ── Thread Creation ───────────────────────────────────────────────────
    static class OrderProcessor extends Thread {
        private final String orderId;
        public OrderProcessor(String id) { super("Worker-" + id); this.orderId = id; }

        @Override
        public void run() {
            System.out.printf("[%s] Processing %s%n", getName(), orderId);
            try { Thread.sleep(100); } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
            System.out.printf("[%s] Completed %s%n", getName(), orderId);
        }
    }

    // ── Atomic counters (lock-free, thread-safe) ──────────────────────────
    static final AtomicInteger processed = new AtomicInteger(0);
    static final AtomicLong    revenue   = new AtomicLong(0);

    // ── Synchronized (one thread at a time) ──────────────────────────────
    static class InventoryManager {
        private final Map<String, Integer> stock = new HashMap<>();

        public synchronized boolean reserve(String sku, int qty) {
            int available = stock.getOrDefault(sku, 0);
            if (available < qty) return false;
            stock.put(sku, available - qty);
            return true;
        }

        public synchronized void restock(String sku, int qty) {
            stock.merge(sku, qty, Integer::sum);
        }
    }

    // ── ExecutorService ───────────────────────────────────────────────────
    static void executorDemo() throws InterruptedException {
        ExecutorService pool = Executors.newFixedThreadPool(4);
        List<Future<String>> futures = new ArrayList<>();

        for (int i = 1; i <= 8; i++) {
            final int id = i;
            futures.add(pool.submit(() -> {
                Thread.sleep((long)(Math.random() * 200));
                processed.incrementAndGet();
                return "Order-" + id + " by " + Thread.currentThread().getName();
            }));
        }

        for (Future<String> f : futures) {
            try { System.out.println("  " + f.get(2, TimeUnit.SECONDS)); }
            catch (ExecutionException | TimeoutException e) {
                System.err.println("  Task failed: " + e.getMessage());
            }
        }

        pool.shutdown();
        pool.awaitTermination(5, TimeUnit.SECONDS);
        System.out.println("Processed: " + processed.get());
    }

    // ── CompletableFuture async pipeline ──────────────────────────────────
    static void completableFutureDemo() throws Exception {
        CompletableFuture<String> pipeline = CompletableFuture
            .supplyAsync(() -> {
                System.out.println("  [1] Validating...");
                return "ORDER-001";
            })
            .thenApplyAsync(id -> {
                System.out.println("  [2] Processing payment for " + id);
                return id + " | PAID";
            })
            .thenApply(result -> {
                System.out.println("  [3] Sending confirmation...");
                return result + " | NOTIFIED";
            })
            .exceptionally(ex -> {
                System.err.println("  Failed: " + ex.getMessage());
                return "FAILED";
            });

        System.out.println("Result: " + pipeline.get());

        // Combine two independent futures
        CompletableFuture<Double>  priceF = CompletableFuture.supplyAsync(() -> 99.99);
        CompletableFuture<Integer> stockF = CompletableFuture.supplyAsync(() -> 50);

        String combined = priceF.thenCombine(stockF,
            (p, s) -> String.format("Price: $%.2f | Stock: %d", p, s)).get();
        System.out.println(combined);
    }

    // ── CountDownLatch: wait for N threads to complete ────────────────────
    static void latchDemo() throws InterruptedException {
        CountDownLatch latch = new CountDownLatch(3);
        ExecutorService exec = Executors.newFixedThreadPool(3);
        String[] services = {"AuthService", "PaymentService", "InventoryService"};

        for (String svc : services) {
            exec.submit(() -> {
                try {
                    Thread.sleep((long)(Math.random() * 500 + 100));
                    System.out.println("  " + svc + " ready");
                    latch.countDown();
                } catch (InterruptedException e) { Thread.currentThread().interrupt(); }
            });
        }

        latch.await(5, TimeUnit.SECONDS); // blocks until count = 0
        System.out.println("All services ready!");
        exec.shutdown();
    }

    // ── Semaphore: limit concurrent resource access ────────────────────────
    static void semaphoreDemo() throws InterruptedException {
        Semaphore dbPool = new Semaphore(3, true); // max 3 concurrent connections
        ExecutorService exec = Executors.newFixedThreadPool(8);

        for (int i = 1; i <= 8; i++) {
            final int id = i;
            exec.submit(() -> {
                try {
                    dbPool.acquire();
                    System.out.println("  Thread " + id + " connected (permits: " + dbPool.availablePermits() + ")");
                    Thread.sleep(200);
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                } finally {
                    dbPool.release();
                }
            });
        }
        exec.shutdown();
        exec.awaitTermination(5, TimeUnit.SECONDS);
    }

    public static void main(String[] args) throws Exception {
        // Basic thread
        new OrderProcessor("ORD-001").start();

        // Lambda thread
        new Thread(() -> System.out.println("Quick task on " +
                Thread.currentThread().getName())).start();

        System.out.println("\n=== ExecutorService ===");
        executorDemo();

        System.out.println("\n=== CompletableFuture Pipeline ===");
        completableFutureDemo();

        System.out.println("\n=== CountDownLatch ===");
        latchDemo();

        System.out.println("\n=== Semaphore (DB Pool) ===");
        semaphoreDemo();
    }
}
```

---

## 12. File I/O & NIO

```java
// FileIODemo.java
// Real-world: Log file processing & report generation

import java.io.*;
import java.nio.file.*;
import java.util.*;
import java.util.stream.*;

public class FileIODemo {

    // Traditional I/O — write
    static void writeFile(String path, List<String> lines) throws IOException {
        try (BufferedWriter w = new BufferedWriter(new FileWriter(path))) {
            for (String line : lines) { w.write(line); w.newLine(); }
        }
    }

    // Traditional I/O — read
    static List<String> readFile(String path) throws IOException {
        List<String> lines = new ArrayList<>();
        try (BufferedReader r = new BufferedReader(new FileReader(path))) {
            String line;
            while ((line = r.readLine()) != null) lines.add(line);
        }
        return lines;
    }

    // NIO — modern file operations (Java 7+)
    static void nioDemo() throws IOException {
        Path dir  = Paths.get("reports");
        Path file = dir.resolve("report_2024.txt");

        Files.createDirectories(dir);  // creates full path if missing

        // Write atomically
        Files.write(file, List.of("=== Monthly Report ===", "Revenue: $98,430.50"));

        // Read entire file (Java 11+)
        String all = Files.readString(file);
        System.out.println(all);

        // Stream lines (lazy — good for large files)
        try (Stream<String> lines = Files.lines(file)) {
            lines.filter(l -> l.contains("Revenue"))
                 .forEach(System.out::println);
        }

        // Copy with options
        Files.copy(file, dir.resolve("report_backup.txt"),
                StandardCopyOption.REPLACE_EXISTING);

        // Walk directory tree
        try (Stream<Path> walk = Files.walk(dir)) {
            walk.filter(Files::isRegularFile)
                .forEach(p -> System.out.println("  " + p));
        }

        // File metadata
        System.out.println("Size   : " + Files.size(file) + " bytes");
        System.out.println("Exists : " + Files.exists(file));
    }

    // CSV processing
    static void csvDemo() throws IOException {
        Path csv = Paths.get("employees.csv");
        Files.write(csv, List.of(
            "name,department,salary",
            "Alice,Engineering,95000",
            "Bob,Marketing,65000",
            "Charlie,HR,60000"
        ));

        // Stream processing — no need to load entire file into memory
        try (Stream<String> lines = Files.lines(csv)) {
            lines.skip(1) // skip header
                .map(line -> line.split(","))
                .filter(p -> Double.parseDouble(p[2]) > 70000)
                .forEach(p -> System.out.printf("  %s (%s): $%s%n", p[0], p[1], p[2]));
        }
    }

    public static void main(String[] args) throws IOException {
        writeFile("output.txt", List.of("Line 1", "Line 2", "Line 3"));
        List<String> content = readFile("output.txt");
        System.out.println("Read " + content.size() + " lines");

        nioDemo();
        csvDemo();
    }
}
```

---

## 13. Design Patterns

```java
// DesignPatterns.java
// Real-world: Configuration, construction, notifications, events, sorting

import java.util.*;

// ── SINGLETON — thread-safe lazy init ─────────────────────────────────────────
class DatabasePool {
    private static volatile DatabasePool instance;
    private final List<String> connections = new ArrayList<>();

    private DatabasePool() {
        for (int i = 1; i <= 10; i++) connections.add("conn-" + i);
    }

    public static DatabasePool getInstance() {
        if (instance == null) {
            synchronized (DatabasePool.class) {
                if (instance == null) instance = new DatabasePool();
            }
        }
        return instance;
    }

    public synchronized String  getConnection()        { return connections.remove(0); }
    public synchronized void    release(String c)       { connections.add(c); }
    public synchronized int     available()             { return connections.size(); }
}

// ── BUILDER — fluent API for complex objects ───────────────────────────────────
class HttpRequest {
    private final String url, method, body;
    private final Map<String, String> headers;
    private final int timeoutMs;

    private HttpRequest(Builder b) {
        url = b.url; method = b.method; body = b.body;
        headers = Collections.unmodifiableMap(b.headers); timeoutMs = b.timeoutMs;
    }

    public static class Builder {
        private final String url;
        private String method = "GET", body;
        private final Map<String, String> headers = new LinkedHashMap<>();
        private int timeoutMs = 30_000;

        public Builder(String url)                { this.url = Objects.requireNonNull(url); }
        public Builder method(String m)           { method = m; return this; }
        public Builder post(String b)             { method = "POST"; body = b; return this; }
        public Builder header(String k, String v) { headers.put(k, v); return this; }
        public Builder bearerToken(String t)      { return header("Authorization", "Bearer " + t); }
        public Builder json()                     { return header("Content-Type", "application/json"); }
        public Builder timeout(int ms)            { timeoutMs = ms; return this; }
        public HttpRequest build()                { return new HttpRequest(this); }
    }

    @Override
    public String toString() {
        return method + " " + url + " headers=" + headers + " timeout=" + timeoutMs + "ms";
    }
}

// ── FACTORY — create objects based on type ────────────────────────────────────
interface Notification {
    void send(String to, String msg);
    String getChannel();
}

class EmailNotification implements Notification {
    public void send(String to, String msg)  { System.out.printf("[EMAIL → %s] %s%n", to, msg); }
    public String getChannel()               { return "EMAIL"; }
}

class SmsNotification implements Notification {
    public void send(String to, String msg)  { System.out.printf("[SMS → %s] %s%n", to, msg.substring(0, Math.min(160, msg.length()))); }
    public String getChannel()               { return "SMS"; }
}

class NotificationFactory {
    public static Notification create(String type) {
        return switch (type.toUpperCase()) {
            case "EMAIL" -> new EmailNotification();
            case "SMS"   -> new SmsNotification();
            default -> throw new IllegalArgumentException("Unknown: " + type);
        };
    }
}

// ── OBSERVER — event-driven programming ───────────────────────────────────────
interface OrderListener {
    void onOrderPlaced(String orderId, double amount);
}

class OrderEventBus {
    private final List<OrderListener> listeners = new ArrayList<>();
    public void subscribe(OrderListener l)     { listeners.add(l); }
    public void publish(String id, double amt) {
        System.out.println("Publishing event: " + id);
        listeners.forEach(l -> l.onOrderPlaced(id, amt));
    }
}

// ── STRATEGY — interchangeable algorithms ─────────────────────────────────────
interface SortStrategy {
    void sort(List<Integer> list);
    String name();
}

class BubbleSort implements SortStrategy {
    public void sort(List<Integer> list) {
        int n = list.size();
        for (int i = 0; i < n-1; i++)
            for (int j = 0; j < n-i-1; j++)
                if (list.get(j) > list.get(j+1)) {
                    int t = list.get(j); list.set(j, list.get(j+1)); list.set(j+1, t);
                }
    }
    public String name() { return "BubbleSort"; }
}

class QuickSort implements SortStrategy {
    public void sort(List<Integer> list) { Collections.sort(list); }
    public String name()                 { return "QuickSort (built-in)"; }
}

class Sorter {
    private SortStrategy strategy;
    public void setStrategy(SortStrategy s) { strategy = s; }
    public void sort(List<Integer> list) {
        long t = System.nanoTime(); strategy.sort(list); t = System.nanoTime() - t;
        System.out.printf("[%s] sorted %d items in %dns → %s%n", strategy.name(), list.size(), t, list);
    }
}

class DesignPatternDemo {
    public static void main(String[] args) {
        // Singleton
        DatabasePool p1 = DatabasePool.getInstance();
        DatabasePool p2 = DatabasePool.getInstance();
        System.out.println("Same instance: " + (p1 == p2));
        System.out.println("Available: " + p1.available());

        // Builder
        HttpRequest req = new HttpRequest.Builder("https://api.example.com/orders")
            .post("{\"item\":\"laptop\"}")
            .json()
            .bearerToken("eyJhbGci...")
            .timeout(5000)
            .header("X-Request-ID", UUID.randomUUID().toString())
            .build();
        System.out.println(req);

        // Factory
        for (String ch : new String[]{"EMAIL", "SMS"}) {
            NotificationFactory.create(ch).send("user@example.com", "Order shipped!");
        }

        // Observer
        OrderEventBus bus = new OrderEventBus();
        bus.subscribe((id, amt) -> System.out.println("  [Inventory] Reserved for " + id));
        bus.subscribe((id, amt) -> System.out.printf("  [Analytics] $%.2f sale%n", amt));
        bus.publish("ORD-001", 299.99);

        // Strategy
        List<Integer> nums = new ArrayList<>(Arrays.asList(64, 34, 25, 12, 22, 11, 90));
        Sorter sorter = new Sorter();
        sorter.setStrategy(new BubbleSort());
        sorter.sort(nums);
        sorter.setStrategy(new QuickSort());
        sorter.sort(new ArrayList<>(Arrays.asList(5, 3, 8, 1, 9)));
    }
}
```

---

## 14. Java Memory & JVM Internals

```java
// JvmInternals.java
// Real-world: Understanding memory leaks, GC tuning, performance optimization

public class JvmInternals {

    /*
     * JVM MEMORY LAYOUT
     * ══════════════════════════════════════════════════════════════
     *
     * ┌─────────────────────────────────────────────────────────┐
     * │                      JVM Process                         │
     * │                                                          │
     * │  ┌──────────────────────────────────────────────────┐   │
     * │  │                    HEAP                           │   │
     * │  │  ┌───────────────────┐  ┌────────────────────┐   │   │
     * │  │  │   Young Gen       │  │     Old Gen        │   │   │
     * │  │  │  [Eden|S0|S1]     │  │  (long-lived obj)  │   │   │
     * │  │  └───────────────────┘  └────────────────────┘   │   │
     * │  └──────────────────────────────────────────────────┘   │
     * │                                                          │
     * │  ┌────────────┐  ┌─────────────┐  ┌────────────────┐   │
     * │  │ Metaspace  │  │ Thread Stack│  │  Code Cache    │   │
     * │  │ (classes)  │  │ (per thread)│  │  (JIT output)  │   │
     * │  └────────────┘  └─────────────┘  └────────────────┘   │
     * └─────────────────────────────────────────────────────────┘
     *
     * GC Lifecycle:
     *   Minor GC → Young Gen only (fast, frequent)
     *   Major GC → Old Gen (slow, "stop-the-world")
     *   G1GC (Java 9+ default) → concurrent, region-based, low-pause
     */

    // Stack vs Heap
    static int stackExample() {
        int a = 10, b = 20;   // on stack — auto-freed when method returns
        return a + b;
    }

    static void heapExample() {
        // Object is on heap; reference 'sb' is on stack
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < 100; i++) sb.append(i);
        // sb goes out of scope — object eligible for GC
    }

    // String Pool
    static void stringPoolDemo() {
        String s1 = "hello";           // String pool
        String s2 = "hello";           // SAME pool reference
        String s3 = new String("hello");// New heap object
        String s4 = s3.intern();       // Back to pool

        System.out.println(s1 == s2); // true  (same pool ref)
        System.out.println(s1 == s3); // false (s3 is heap)
        System.out.println(s1 == s4); // true  (intern returns pool ref)
        System.out.println(s1.equals(s3)); // true (same content)
    }

    // WeakReference — GC can collect when memory is needed
    static void weakRefDemo() {
        java.lang.ref.WeakReference<byte[]> ref =
            new java.lang.ref.WeakReference<>(new byte[1024]);
        byte[] data = ref.get();
        if (data != null) System.out.println("Data: " + data.length + " bytes");
        // After GC: ref.get() returns null — entry removed from cache
    }

    /*
     * JVM TUNING FLAGS (reference)
     * ══════════════════════════════════════════════════════════════
     *
     * Memory:
     *   -Xms512m              → initial heap (set = -Xmx in prod)
     *   -Xmx2g                → max heap
     *   -Xss512k              → stack size per thread
     *   -XX:MaxMetaspaceSize=256m
     *
     * GC:
     *   -XX:+UseG1GC          → G1 (default Java 9+)
     *   -XX:+UseZGC           → ZGC (Java 15+, ultra-low pause)
     *   -XX:MaxGCPauseMillis=200
     *   -Xlog:gc*:file=gc.log → GC logging
     *
     * Debug:
     *   -XX:+HeapDumpOnOutOfMemoryError
     *   -XX:HeapDumpPath=/tmp/heap.hprof
     *   -agentlib:jdwp=transport=dt_socket,server=y,port=5005
     */

    public static void main(String[] args) {
        Runtime rt = Runtime.getRuntime();
        System.out.println("CPUs    : " + rt.availableProcessors());
        System.out.printf("Heap max: %,d MB%n", rt.maxMemory() / 1_048_576);
        System.out.printf("Free    : %,d MB%n", rt.freeMemory() / 1_048_576);

        stringPoolDemo();
        weakRefDemo();

        System.gc(); // hint only — JVM decides when to actually run
        System.out.printf("After GC: %,d MB free%n", rt.freeMemory() / 1_048_576);
    }
}
```

---

## 15. Real-World Spring Boot Project

### Employee Management REST API

```java
// ── Entity ────────────────────────────────────────────────────────────────────
import jakarta.persistence.*;
import jakarta.validation.constraints.*;
import lombok.*;
import java.time.LocalDate;

@Entity
@Table(name = "employees")
@Getter @Setter @NoArgsConstructor @AllArgsConstructor @Builder
public class Employee {

    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @NotBlank @Size(min = 2, max = 50)
    @Column(name = "first_name", nullable = false)
    private String firstName;

    @NotBlank
    @Column(name = "last_name", nullable = false)
    private String lastName;

    @Email @NotBlank
    @Column(unique = true, nullable = false)
    private String email;

    @NotBlank private String department;

    @Positive private Double salary;

    @PastOrPresent @Column(name = "join_date")
    private LocalDate joinDate;

    @Enumerated(EnumType.STRING)
    @Column(nullable = false)
    private Status status;

    @Version private Long version; // optimistic locking

    public enum Status { ACTIVE, INACTIVE, ON_LEAVE, TERMINATED }
}
```

```java
// ── Repository ────────────────────────────────────────────────────────────────
import org.springframework.data.jpa.repository.*;
import org.springframework.data.domain.*;

public interface EmployeeRepository extends JpaRepository<Employee, Long> {

    Optional<Employee> findByEmail(String email);
    boolean            existsByEmail(String email);
    Page<Employee>     findByDepartment(String dept, Pageable pageable);
    long               countByDepartment(String dept);

    List<Employee>     findByDepartmentAndStatus(String dept, Employee.Status status);

    @Query("SELECT e FROM Employee e WHERE e.salary BETWEEN :min AND :max ORDER BY e.salary DESC")
    List<Employee> findBySalaryRange(@Param("min") double min, @Param("max") double max);

    @Modifying @Transactional
    @Query("UPDATE Employee e SET e.status = :status WHERE e.department = :dept")
    int updateStatusByDepartment(@Param("dept") String dept, @Param("status") Employee.Status status);
}
```

```java
// ── Service ───────────────────────────────────────────────────────────────────
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
@Slf4j
@RequiredArgsConstructor
public class EmployeeService {

    private final EmployeeRepository repository;

    @Transactional(readOnly = true)
    public Page<EmployeeDto> getAll(Pageable pageable) {
        return repository.findAll(pageable).map(this::toDto);
    }

    @Transactional(readOnly = true)
    public EmployeeDto getById(Long id) {
        return repository.findById(id)
            .map(this::toDto)
            .orElseThrow(() -> new ResourceNotFoundException("Employee", id));
    }

    @Transactional
    public EmployeeDto create(CreateEmployeeRequest req) {
        if (repository.existsByEmail(req.getEmail()))
            throw new DuplicateEmailException(req.getEmail());

        Employee e = Employee.builder()
            .firstName(req.getFirstName()).lastName(req.getLastName())
            .email(req.getEmail()).department(req.getDepartment())
            .salary(req.getSalary())
            .joinDate(req.getJoinDate() != null ? req.getJoinDate() : LocalDate.now())
            .status(Employee.Status.ACTIVE)
            .build();

        Employee saved = repository.save(e);
        log.info("Created employee: {} (id={})", saved.getEmail(), saved.getId());
        return toDto(saved);
    }

    @Transactional
    public EmployeeDto update(Long id, CreateEmployeeRequest req) {
        Employee e = repository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("Employee", id));
        e.setFirstName(req.getFirstName()); e.setLastName(req.getLastName());
        e.setDepartment(req.getDepartment()); e.setSalary(req.getSalary());
        return toDto(repository.save(e));
    }

    @Transactional
    public void delete(Long id) {
        if (!repository.existsById(id)) throw new ResourceNotFoundException("Employee", id);
        repository.deleteById(id);
        log.info("Deleted employee id={}", id);
    }

    private EmployeeDto toDto(Employee e) {
        return EmployeeDto.builder()
            .id(e.getId()).firstName(e.getFirstName()).lastName(e.getLastName())
            .email(e.getEmail()).department(e.getDepartment()).salary(e.getSalary())
            .joinDate(e.getJoinDate()).status(e.getStatus().name())
            .fullName(e.getFirstName() + " " + e.getLastName())
            .build();
    }
}
```

```java
// ── Controller ────────────────────────────────────────────────────────────────
import org.springframework.web.bind.annotation.*;
import org.springframework.data.domain.*;
import org.springframework.http.*;

@RestController
@RequestMapping("/api/v1/employees")
@RequiredArgsConstructor
public class EmployeeController {

    private final EmployeeService service;

    @GetMapping                                          // GET /api/v1/employees?page=0&size=20
    public ResponseEntity<Page<EmployeeDto>> getAll(
            @PageableDefault(size = 20, sort = "lastName") Pageable pageable) {
        return ResponseEntity.ok(service.getAll(pageable));
    }

    @GetMapping("/{id}")                                 // GET /api/v1/employees/5
    public ResponseEntity<EmployeeDto> getById(@PathVariable Long id) {
        return ResponseEntity.ok(service.getById(id));
    }

    @PostMapping                                         // POST /api/v1/employees
    public ResponseEntity<EmployeeDto> create(@RequestBody @Valid CreateEmployeeRequest req) {
        EmployeeDto created = service.create(req);
        URI location = URI.create("/api/v1/employees/" + created.getId());
        return ResponseEntity.created(location).body(created);
    }

    @PutMapping("/{id}")                                 // PUT /api/v1/employees/5
    public ResponseEntity<EmployeeDto> update(
            @PathVariable Long id, @RequestBody @Valid CreateEmployeeRequest req) {
        return ResponseEntity.ok(service.update(id, req));
    }

    @DeleteMapping("/{id}")                              // DELETE /api/v1/employees/5
    public ResponseEntity<Void> delete(@PathVariable Long id) {
        service.delete(id);
        return ResponseEntity.noContent().build();       // 204 No Content
    }
}
```

```java
// ── Global Exception Handler ──────────────────────────────────────────────────
@RestControllerAdvice
@Slf4j
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND)
            .body(new ErrorResponse("NOT_FOUND", ex.getMessage()));
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ErrorResponse> handleValidation(MethodArgumentNotValidException ex) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors()
            .forEach(e -> errors.put(e.getField(), e.getDefaultMessage()));
        return ResponseEntity.badRequest()
            .body(new ErrorResponse("VALIDATION_FAILED", "Input validation failed", errors));
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleAll(Exception ex) {
        log.error("Unhandled exception", ex);
        return ResponseEntity.status(500)
            .body(new ErrorResponse("INTERNAL_ERROR", "Unexpected error"));
    }
}
```

```yaml
# application.yml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/employee_db
    username: ${DB_USER}
    password: ${DB_PASS}
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false
    properties:
      hibernate:
        format_sql: true
  flyway:
    enabled: true
    locations: classpath:db/migration

server:
  port: 8080

logging:
  level:
    com.example: DEBUG
```

---

## Quick Reference

### Java 8–21 Feature Timeline

| Version | Key Features |
|---|---|
| **Java 8** | Lambda, Stream API, Optional, `default` methods, `java.time` |
| **Java 9** | Modules, `List.of()`, `Map.of()`, `Stream.takeWhile()` |
| **Java 10** | `var` local type inference |
| **Java 11** | `String.isBlank()`, `Files.readString()`, HTTP Client |
| **Java 14** | Switch expressions (stable) |
| **Java 15** | Text blocks (stable) |
| **Java 16** | `instanceof` pattern matching, Records, `Stream.toList()` |
| **Java 17** | Sealed classes — LTS |
| **Java 21** | Virtual threads (Project Loom), pattern switch — LTS |

---

### Common Interview Topics

```java
// 1. String vs StringBuilder
//    String:        immutable — each + creates new object O(n²)
//    StringBuilder: mutable  — single object, append in-place O(n)

// 2. == vs equals
Integer a = 127, b = 127; System.out.println(a == b);  // true  (cached -128 to 127)
Integer c = 128, d = 128; System.out.println(c == d);  // false (not cached)

// 3. ArrayList vs LinkedList
//    ArrayList:   O(1) get,  O(n) insert/delete at middle
//    LinkedList:  O(n) get,  O(1) insert/delete at known node

// 4. HashMap internals (Java 8+)
//    Array of buckets → each bucket = linked list
//    When bucket size > 8 → converts to red-black tree O(log n)
//    Load factor 0.75 → resizes at 75% capacity

// 5. final vs finally vs finalize
//    final:    variable=no reassign, method=no override, class=no extend
//    finally:  always runs in try-catch block
//    finalize: deprecated Java 9, removed Java 18

// 6. Checked vs Unchecked Exceptions
//    Checked:   must declare/catch — IOException, SQLException
//    Unchecked: optional — NullPointerException, IllegalArgumentException

// 7. Abstract Class vs Interface
//    Abstract: state (fields), constructors, partial impl, single inherit
//    Interface: default/static methods (Java 8+), no state, multiple inherit

// 8. Comparable vs Comparator
class Product implements Comparable<Product> {
    double price; String name;
    public int compareTo(Product o) { return Double.compare(price, o.price); }
}
// Multiple sort orders with Comparator:
Comparator<Product> byPrice     = Comparator.comparingDouble(p -> p.price);
Comparator<Product> byNameThen  = Comparator.comparing(p -> p.name,
    Comparator.comparingDouble(p2 -> p2.price)); // then by price

// 9. Thread-safe collections
//    HashMap       → NOT thread-safe
//    ConcurrentHashMap → thread-safe (segmented locks)
//    Collections.synchronizedMap(map) → thread-safe but coarse lock
//    HashSet       → NOT thread-safe
//    CopyOnWriteArrayList → thread-safe for read-heavy workloads

// 10. Method References
// Type                  | Syntax              | Equivalent lambda
// Static method         | Math::abs           | x -> Math.abs(x)
// Instance method       | String::toUpperCase | s -> s.toUpperCase()
// Instance on obj       | obj::method         | x -> obj.method(x)
// Constructor           | ArrayList::new      | () -> new ArrayList<>()
```

---

*Complete guide covering Java 8–21 from basics to production-grade patterns.*
*Practice every example: copy it, run it, modify it, break it, fix it.*
