cmake_minimum_required(VERSION 3.31)

project(FinanceTracker)

set(CMAKE_CXX_STANDARD 17)

# Include directories for headers
include_directories(include/models)
include_directories(include/services)
include_directories(include/utils)

# Add executable with ONLY source files
add_executable(FinanceTracker
        src/models/category.cpp
        src/models/Transactions.cpp
        src/models/user.cpp
        src/models/wallet.cpp
        src/services/CategoryManager.cpp
        src/services/DataPersistence.cpp
        src/services/ReportGenerator.cpp
        src/services/TransactionsManager.cpp
        src/services/WalletManager.cpp
        src/utils/constants.cpp
        src/utils/dateTimeHelper.cpp
        src/utils/FileManager.cpp
        src/utils/inputValidator.cpp
        src/main.cpp
)
