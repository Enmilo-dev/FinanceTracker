# 📖 API Reference

Complete API documentation for FinanceTracker classes and methods.

---

## Table of Contents

- [Models](#models)
  - [User](#user)
  - [Wallet](#wallet)
  - [Transaction](#transaction)
  - [Category](#category)
- [Services](#services)
  - [CategoryManager](#categorymanager)
  - [TransactionManager](#transactionmanager)
  - [WalletManager](#walletmanager)
  - [ReportGenerator](#reportgenerator)
  - [DataPersistence](#datapersistence)
- [Utils](#utils)
  - [FileManager](#filemanager)
  - [DateTimeHelper](#datetimehelper)
  - [InputValidator](#inputvalidator)
  - [Constants](#constants)

---

## Models

### User

Represents a user account in the system.

#### Constructor

```cpp
User(const string& name, const string& email);
```

**Parameters:**
- `name` - User's full name
- `email` - User's email address

#### Methods

```cpp
string getName() const;
void setName(const string& name);

string getEmail() const;
void setEmail(const string& email);

int getUserId() const;
```

#### Example Usage

```cpp
User user("John Doe", "john@example.com");
cout << user.getName() << endl;  // Output: John Doe
user.setEmail("newemail@example.com");
```

---

### Wallet

Represents a financial wallet/account.

#### Constructor

```cpp
Wallet(const string& name, double initialBalance);
```

**Parameters:**
- `name` - Wallet name/identifier
- `initialBalance` - Starting balance

#### Methods

```cpp
string getName() const;
void setName(const string& name);

double getBalance() const;
void setBalance(double balance);

void deposit(double amount);
void withdraw(double amount);

int getWalletId() const;
```

#### Example Usage

```cpp
Wallet wallet("Savings", 1000.0);
wallet.deposit(500.0);
wallet.withdraw(200.0);
cout << wallet.getBalance() << endl;  // Output: 1300.0
```

---

### Transaction

Represents a financial transaction.

#### Constructor

```cpp
Transaction(const string& description, double amount,
            const string& category, const string& date);
```

**Parameters:**
- `description` - Transaction description
- `amount` - Transaction amount (negative for expenses, positive for income)
- `category` - Category name
- `date` - Transaction date (format: YYYY-MM-DD)

#### Methods

```cpp
string getDescription() const;
void setDescription(const string& desc);

double getAmount() const;
void setAmount(double amount);

string getCategory() const;
void setCategory(const string& category);

string getDate() const;
void setDate(const string& date);

int getTransactionId() const;

bool isExpense() const;  // Returns true if amount < 0
bool isIncome() const;   // Returns true if amount > 0
```

#### Example Usage

```cpp
Transaction expense("Groceries", -75.50, "Food", "2025-09-30");
if (expense.isExpense()) {
    cout << "This is an expense" << endl;
}
```

---

### Category

Represents a transaction category.

#### Constructor

```cpp
Category(const string& name, const string& type);
```

**Parameters:**
- `name` - Category name
- `type` - Category type ("income" or "expense")

#### Methods

```cpp
string getName() const;
void setName(const string& name);

string getType() const;
void setType(const string& type);

int getCategoryId() const;
```

#### Example Usage

```cpp
Category foodCategory("Food", "expense");
Category salaryCategory("Salary", "income");
```

---

## Services

### CategoryManager

Manages category operations.

#### Methods

```cpp
void addCategory(const Category& category);
void removeCategory(int categoryId);
void updateCategory(int categoryId, const Category& category);

Category getCategoryById(int id) const;
Category getCategoryByName(const string& name) const;

vector<Category> getAllCategories() const;
vector<Category> getCategoriesByType(const string& type) const;

bool categoryExists(const string& name) const;
```

#### Example Usage

```cpp
CategoryManager manager;
Category food("Food", "expense");
manager.addCategory(food);

vector<Category> expenses = manager.getCategoriesByType("expense");
```

---

### TransactionManager

Manages transaction operations.

#### Methods

```cpp
void addTransaction(const Transaction& transaction);
void removeTransaction(int transactionId);
void updateTransaction(int transactionId, const Transaction& transaction);

Transaction getTransactionById(int id) const;
vector<Transaction> getAllTransactions() const;

vector<Transaction> getTransactionsByCategory(const string& category) const;
vector<Transaction> getTransactionsByDateRange(const string& startDate,
                                                 const string& endDate) const;

double getTotalIncome() const;
double getTotalExpenses() const;
double getNetBalance() const;
```

#### Example Usage

```cpp
TransactionManager manager;
Transaction t("Coffee", -5.50, "Food", "2025-09-30");
manager.addTransaction(t);

double total = manager.getTotalExpenses();
vector<Transaction> food = manager.getTransactionsByCategory("Food");
```

---

### WalletManager

Manages wallet operations.

#### Methods

```cpp
void addWallet(const Wallet& wallet);
void removeWallet(int walletId);
void updateWallet(int walletId, const Wallet& wallet);

Wallet getWalletById(int id) const;
Wallet getWalletByName(const string& name) const;

vector<Wallet> getAllWallets() const;

void transferFunds(int fromWalletId, int toWalletId, double amount);

double getTotalBalance() const;  // Sum of all wallets
```

#### Example Usage

```cpp
WalletManager manager;
Wallet checking("Checking", 1000.0);
Wallet savings("Savings", 5000.0);

manager.addWallet(checking);
manager.addWallet(savings);

manager.transferFunds(savingsId, checkingId, 500.0);
```

---

### ReportGenerator

Generates financial reports and analytics.

#### Methods

```cpp
string generateMonthlyReport(int month, int year) const;
string generateYearlyReport(int year) const;
string generateCategoryReport() const;

map<string, double> getCategoryBreakdown() const;
map<string, double> getMonthlyTrends(int year) const;

double getAverageMonthlyIncome() const;
double getAverageMonthlyExpense() const;

string exportToCSV() const;
string exportToJSON() const;
```

#### Example Usage

```cpp
ReportGenerator generator;
string report = generator.generateMonthlyReport(9, 2025);
cout << report << endl;

map<string, double> breakdown = generator.getCategoryBreakdown();
for (const auto& [category, amount] : breakdown) {
    cout << category << ": $" << amount << endl;
}
```

---

### DataPersistence

Handles data loading and saving.

#### Methods

```cpp
bool saveData() const;
bool loadData();

bool saveUsers(const vector<User>& users);
bool loadUsers(vector<User>& users);

bool saveWallets(const vector<Wallet>& wallets);
bool loadWallets(vector<Wallet>& wallets);

bool saveTransactions(const vector<Transaction>& transactions);
bool loadTransactions(vector<Transaction>& transactions);

bool saveCategories(const vector<Category>& categories);
bool loadCategories(vector<Category>& categories);

void setDataDirectory(const string& path);
string getDataDirectory() const;
```

#### Example Usage

```cpp
DataPersistence persistence;
persistence.setDataDirectory("./data");

if (persistence.loadData()) {
    cout << "Data loaded successfully" << endl;
}

// After modifications
if (persistence.saveData()) {
    cout << "Data saved successfully" << endl;
}
```

---

## Utils

### FileManager

Handles file I/O operations.

#### Methods

```cpp
static bool fileExists(const string& filepath);
static bool createDirectory(const string& path);

static string readFile(const string& filepath);
static bool writeFile(const string& filepath, const string& content);

static vector<string> readLines(const string& filepath);
static bool writeLines(const string& filepath, const vector<string>& lines);

static bool deleteFile(const string& filepath);
static bool copyFile(const string& source, const string& destination);
```

#### Example Usage

```cpp
if (FileManager::fileExists("data/users.json")) {
    string content = FileManager::readFile("data/users.json");
    // Process content
}

FileManager::writeFile("data/backup.txt", "Backup data");
```

---

### DateTimeHelper

Provides date and time utilities.

#### Methods

```cpp
static string getCurrentDate();           // Format: YYYY-MM-DD
static string getCurrentDateTime();       // Format: YYYY-MM-DD HH:MM:SS
static string getCurrentTime();           // Format: HH:MM:SS

static bool isValidDate(const string& date);
static bool isDateInRange(const string& date, const string& start,
                          const string& end);

static int getDaysBetween(const string& date1, const string& date2);
static string addDays(const string& date, int days);

static int getMonth(const string& date);
static int getYear(const string& date);
static int getDay(const string& date);

static string formatDate(const string& date, const string& format);
```

#### Example Usage

```cpp
string today = DateTimeHelper::getCurrentDate();
cout << today << endl;  // Output: 2025-09-30

if (DateTimeHelper::isValidDate("2025-09-30")) {
    int days = DateTimeHelper::getDaysBetween("2025-09-01", "2025-09-30");
    cout << "Days: " << days << endl;  // Output: 29
}
```

---

### InputValidator

Validates user input.

#### Methods

```cpp
static bool isValidEmail(const string& email);
static bool isValidAmount(const string& amount);
static bool isValidDate(const string& date);

static bool isPositiveNumber(double number);
static bool isNonEmpty(const string& str);

static string sanitizeInput(const string& input);
static string trim(const string& str);

static bool isInRange(double value, double min, double max);
```

#### Example Usage

```cpp
string email = "user@example.com";
if (InputValidator::isValidEmail(email)) {
    cout << "Valid email" << endl;
}

string input = "  test  ";
string clean = InputValidator::trim(input);  // Output: "test"
```

---

### Constants

Application-wide constants.

#### Constants

```cpp
namespace Constants {
    extern const string APP_NAME;
    extern const string APP_VERSION;

    extern const string DATA_DIR;
    extern const string USER_FILE;
    extern const string WALLET_FILE;
    extern const string TRANSACTION_FILE;
    extern const string CATEGORY_FILE;

    extern const double MIN_AMOUNT;
    extern const double MAX_AMOUNT;

    extern const string DATE_FORMAT;
    extern const string DATETIME_FORMAT;
}
```

#### Example Usage

```cpp
cout << Constants::APP_NAME << " v" << Constants::APP_VERSION << endl;

string dataPath = Constants::DATA_DIR + "/" + Constants::USER_FILE;
```

---

## Error Handling

Most methods throw exceptions on errors:

```cpp
try {
    transactionManager.addTransaction(transaction);
} catch (const exception& e) {
    cerr << "Error: " << e.what() << endl;
}
```

Common exceptions:
- `invalid_argument` - Invalid input parameters
- `runtime_error` - Operation failures
- `out_of_range` - Invalid ID or index

---

## Notes

- All IDs are auto-generated and start from 1
- Dates should be in YYYY-MM-DD format
- Amounts are in double precision (2 decimal places recommended)
- All string comparisons are case-sensitive
- File operations require proper permissions
