# 🏗️ Architecture Documentation

## Overview

FinanceTracker follows a **layered architecture** pattern with clear separation of concerns. The application is structured into three main layers: Models, Services, and Utils.

---

## 📊 System Architecture

```
┌─────────────────────────────────────┐
│         Application Layer           │
│           (main.cpp)                │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│         Service Layer               │
│  ┌─────────────────────────────┐    │
│  │ CategoryManager             │    │
│  │ TransactionManager          │    │
│  │ WalletManager               │    │
│  │ ReportGenerator             │    │
│  │ DataPersistence             │    │
│  └─────────────────────────────┘    │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│         Model Layer                 │
│  ┌─────────────────────────────┐    │
│  │ User                        │    │
│  │ Wallet                      │    │
│  │ Transaction                 │    │
│  │ Category                    │    │
│  └─────────────────────────────┘    │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│         Utility Layer               │
│  ┌─────────────────────────────┐    │
│  │ FileManager                 │    │
│  │ DateTimeHelper              │    │
│  │ InputValidator              │    │
│  │ Constants                   │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
```

---

## 📦 Layer Descriptions

### **1. Model Layer** (`include/models/`, `src/models/`)

**Purpose:** Represents core business entities and data structures.

- **User.h/cpp** - User account information
- **Wallet.h/cpp** - Financial account/wallet data
- **Transaction.h/cpp** - Individual transaction records
- **Category.h/cpp** - Transaction categorization

**Responsibilities:**
- Define data structures
- Encapsulate entity logic
- Provide getters/setters
- Data validation

**Design Pattern:** Plain Old C++ Objects (POCOs) with encapsulation

---

### **2. Service Layer** (`include/services/`, `src/services/`)

**Purpose:** Implements business logic and orchestrates operations.

#### **Manager Classes:**

- **CategoryManager** - CRUD operations for categories
- **TransactionManager** - Transaction handling and queries
- **WalletManager** - Wallet operations and balance management
- **ReportGenerator** - Financial report generation
- **DataPersistence** - Data loading/saving operations

**Responsibilities:**
- Business logic execution
- Data manipulation
- Validation and error handling
- Coordination between models

**Design Pattern:** Manager/Service pattern for business logic separation

---

### **3. Utility Layer** (`utils/`)

**Purpose:** Provides reusable helper functions and constants.

- **FileManager** - File I/O operations
- **DateTimeHelper** - Date/time manipulation utilities
- **InputValidator** - User input validation
- **Constants** - Application-wide constants

**Responsibilities:**
- Common functionality
- Cross-cutting concerns
- Configuration management
- Helper functions

---

## 🔄 Data Flow

```
User Input → InputValidator → Manager (Service) → Model → DataPersistence → File Storage
                                  ↓
                          ReportGenerator → Output
```

### Example Flow: Adding a Transaction

1. **User inputs transaction data** via application interface
2. **InputValidator** validates the input
3. **TransactionManager** creates a Transaction object
4. **Transaction** model is populated with validated data
5. **WalletManager** updates the wallet balance
6. **DataPersistence** saves changes to file storage

---

## 🎯 Design Principles

### **Separation of Concerns**
Each layer has a distinct responsibility:
- Models = Data
- Services = Logic
- Utils = Helpers

### **Single Responsibility**
Each class has one primary purpose and reason to change.

### **Encapsulation**
Internal implementation details are hidden behind clean interfaces.

### **DRY (Don't Repeat Yourself)**
Common functionality is extracted into utility classes.

---

## 📂 File Organization

```
include/
├── models/           # Model headers (data structures)
├── services/         # Service headers (business logic)
└── utils/            # Utility headers (helpers)

src/
├── models/           # Model implementations
├── services/         # Service implementations
├── utils/            # Utility implementations
└── main.cpp          # Application entry point

data/                 # Runtime data storage
```

---

## 🔌 Dependencies

### **Model Dependencies:**
- **None** - Models are independent POCOs

### **Service Dependencies:**
- Models (use model classes)
- Utils (use helper functions)
- Other services (minimal coupling)

### **Utils Dependencies:**
- **None** - Utilities are standalone

---

## 💾 Data Persistence Strategy

- **Format:** JSON/Text files (via FileManager)
- **Location:** `data/` directory
- **Strategy:** File-based storage for simplicity
- **Loading:** On application startup
- **Saving:** On data modification

---

## 🚀 Future Improvements

- [ ] Implement Observer pattern for real-time updates
- [ ] Add database support (SQLite)
- [ ] Introduce dependency injection
- [ ] Add unit testing framework
- [ ] Implement logging system
- [ ] Add configuration management

---

## 🧪 Testing Strategy

Currently manual testing. Future plan:
- Unit tests for models
- Integration tests for services
- End-to-end tests for complete flows

---

## 📝 Notes

- All managers follow the same interface pattern
- File operations are abstracted through FileManager
- Date/time operations use DateTimeHelper for consistency
- Input validation is centralized in InputValidator
