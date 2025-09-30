# 💰 FinanceTracker

<div align="center">

**A powerful C++ personal finance management system**

[![C++](https://img.shields.io/badge/C++-17-blue.svg)](https://isocpp.org/)
[![CMake](https://img.shields.io/badge/CMake-3.31-064F8C.svg)](https://cmake.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

*Track expenses • Manage wallets • Generate insights*

</div>

---

## ✨ Features

- 📊 **Transaction Management** - Track income and expenses with detailed categorization
- 💼 **Multi-Wallet Support** - Manage multiple accounts and wallets simultaneously
- 📈 **Smart Reports** - Generate comprehensive financial reports and analytics
- 🏷️ **Category System** - Organize transactions with customizable categories
- 💾 **Data Persistence** - Secure local data storage with file management
- ⚡ **Fast & Efficient** - Built with modern C++ for optimal performance

---

## 🚀 Quick Start

### Prerequisites

- C++ compiler with C++17 support (GCC 7+, Clang 5+, MSVC 2017+)
- CMake 3.31 or higher
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/Enmilo-dev/FinanceTracker.git
cd FinanceTracker

# Create build directory
mkdir build && cd build

# Configure and build
cmake ..
make

# Run the application
./FinanceTracker
```

---

## 📁 Project Structure

```
FinanceTracker/
├── include/          # Header files
│   ├── models/       # Data model headers
│   ├── services/     # Service layer headers
│   └── utils/        # Utility headers
├── src/              # Source files
│   ├── models/       # Model implementations
│   ├── services/     # Service implementations
│   └── utils/        # Utility implementations
├── data/             # Data storage directory
├── docs/             # Documentation
└── CMakeLists.txt    # Build configuration
```

---

## 💡 Usage Example

```cpp
// Create a new user
User user("John Doe", "john@example.com");

// Create a wallet
Wallet wallet("Main Account", 1000.0);

// Add a transaction
Transaction expense("Groceries", -50.0, "Food");
transactionManager.addTransaction(expense);

// Generate report
reportGenerator.generateMonthlyReport();
```

---

## 🛠️ Built With

- **C++17** - Modern C++ features
- **CMake** - Build system
- **STL** - Standard Template Library

---

## 📚 Documentation

- [API Reference](docs/API_REFERENCE.md) - Detailed API documentation
- [Architecture](docs/ARCHITECTURE.md) - System design and structure

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Your Name**
- GitHub: [@yourusername](https://github.com/Enmilo-dev)
- Email: your.email@example.com

---

<div align="center">

**⭐ Star this repo if you find it helpful!**

Made with ❤️ using C++

</div>
