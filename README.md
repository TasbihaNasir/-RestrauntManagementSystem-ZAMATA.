# 🍽️ ZAMATA - Restaurant Management System (RMS)

A comprehensive console-based Restaurant Management System built in C++, designed to streamline restaurant operations including menu management, order processing, inventory control, billing, employee management, and analytics reporting.

---

## ⚛️ Built With

This system is built using:

- **C++17** — Object-oriented programming with STL
- **File I/O** — CSV and TXT file-based data persistence
- **Standard Libraries** — iostream, fstream, sstream, vector, algorithm, chrono

---

## 👨‍💻 Developers

| Name | Role | GitHub |
|------|------|--------|
| Tasbiha Nasir | Full Stack Developer | @TasbihaNasir |
| Madiha Aslam | Full Stack Developer | @madihaslamnu |
| Zain Saqib | Full Stack Developer | @zainsaqib |

---

## 🧩 System Overview

ZAMATA RMS is a fully modular restaurant management system built using object-oriented principles in C++. The system manages all aspects of restaurant operations from inventory tracking to sales analytics, ensuring efficient workflow, data integrity, and role-based access control for different user types.

---

## 🗄️ Core Features & Modules

### 🔐 Authentication & Access Control
Implements secure role-based login system with:
- **Password Hashing**: Custom hash function for secure password storage
- **Role-Based Access**: Different menus and permissions for Owner, Manager, Cashier, and Customer
- **User Authentication**: Validates credentials against employee database
- **Session Management**: Login ID and password verification system

**Key Classes**: `AuthenticationAccessControl`, `Employee`

---

### 👥 Employee Management
Complete employee lifecycle management system:
- **Add Employees**: Register new staff with role assignment
- **Remove Employees**: Delete employee records from system
- **Update Information**: Modify employee details (salary, password, role)
- **Display Records**: View all employee data
- **Role Hierarchy**: Owner → Manager → Cashier with different access levels

**Key Classes**: `Employee`, `Restaurant_Owner`, `Manager`, `Cashier`

**Data Stored**: Login ID, Role, First Name, Last Name, Salary, Hashed Password

---

### 📦 Inventory Management
Real-time ingredient tracking and stock management:
- **Add Items**: Register new ingredients with quantity, price, and status
- **Auto-Restock**: Automatically replenish out-of-stock items (adds 15 units)
- **View Inventory**: Display all ingredients with availability status
- **Stock Monitoring**: Track which items need restocking (Y/N status)
- **Price Tracking**: Maintain cost prices for profit calculations

**Key Classes**: `Inventory`

**Inventory Attributes**:
- Name (ingredient)
- Quantity (in KG)
- Price (cost per unit)
- Stock Status (Y = in stock, N = needs restock)

---

### 🍕 Menu Management
Dynamic menu creation and maintenance:
- **Add Items**: Create dishes from available inventory ingredients
- **Automatic Pricing**: Calculate cost price from ingredients + 5% markup
- **Remove Items**: Delete menu items
- **Update Items**: Modify name, price, or category
- **Category Organization**: Appetizer, Entree, Dessert, Beverage, Pizza, Pasta, Burger
- **Inventory Integration**: Automatically reduces ingredient quantities when items are added
- **Display Menu**: Formatted category-wise menu presentation

**Key Classes**: `MenuManagement` (inherits from `Inventory`)

**Menu Structure**:
```
Item Name | Cost Price | Category | Selling Price
```

---

### 📝 Order Processing
Comprehensive order management system:
- **Place Order**: Select items from menu with quantities (1-10)
- **Modify Order**: Add, update, or remove items from current order
- **Cancel Order**: Clear entire order
- **Order Validation**: Ensures items exist in menu and quantities are valid
- **Real-time Display**: View current order status
- **Quantity Control**: Limits orders to reasonable quantities

**Key Classes**: `OrderProcessing` (inherits from `MenuManagement`)

**Data Structure**: 
```cpp
vector<pair<string, int>> OrderedItems; // (Item Name, Quantity)
```

---

### 💰 Billing & Payment
Automated billing with tax calculation and payment processing:
- **Generate Bill**: Calculate total from ordered items with quantities
- **Tax Calculation**: 
  - GST: 13%
  - Service Tax: 2%
  - Optional Tip
- **Formatted Receipt**: Professional bill layout with restaurant name and date
- **Sales Logging**: Automatically records transaction in SalesReport.txt
- **Payment Processing**: Multiple payment modes (Cash, Card)

**Key Classes**: `BillingPayment`

**Bill Components**:
- Itemized order list
- Subtotal
- GST (13%)
- Service Tax (2%)
- Tip (optional)
- Grand Total
- Date/Time stamp

---

### 📊 Reporting & Analytics
Comprehensive business intelligence and reporting:

#### Sales Reports
- **Yearly Revenue Analysis**: Aggregate sales data by year
- **Average Revenue**: Calculate average revenue per year
- **Performance Metrics**: Identify best and worst performing years
- **Trend Analysis**: Track revenue patterns over time

#### Customer Feedback
- **Rating System**: 0-5 star rating scale
- **Comment Collection**: Store customer feedback text
- **Year-wise Analysis**: View average ratings per year
- **Feedback History**: Access all reviews for specific years

**Key Classes**: `Reporting` (inherits from `Validation`)

**Reports Generated**:
1. Sales Report - Revenue trends with max/min analysis
2. Customer Feedback Report - Rating analytics and comments

---

### 👤 Customer Management
Track customer interactions and transaction history:
- **Add Customer**: Register customer details
- **Display Records**: View all customer transaction data
- **Payment Tracking**: Record payment methods
- **Transaction History**: Maintain customer purchase records

**Key Classes**: `Cashier` (manages customer data)

**Customer Data**: First Name, Last Name, Cell Number, Payment Mode, Total Bill

---

### ✅ Validation System
Robust input validation across all modules:
- **Name Validation**: Alphabetic characters and spaces only
- **Price Validation**: Non-negative values
- **Ingredient Validation**: Checks against inventory
- **Menu Validation**: Verifies item exists
- **Quantity Validation**: Range checking (1-10)
- **Year Validation**: Reasonable date ranges (1900-2100)

**Key Classes**: `Validation` (base class for inheritance)

---

## 🧱 System Architecture

### Class Hierarchy

```
Validation (Base Class)
│
├── Inventory
│   └── MenuManagement
│       └── OrderProcessing
│
├── Reporting
│
└── Employee
    ├── Restaurant_Owner
    ├── Manager
    └── Cashier

Standalone:
├── AuthenticationAccessControl
├── BillingPayment
└── Customer
```

### Inheritance Relationships
- **Inventory** → inherits from **Validation**
- **MenuManagement** → inherits from **Inventory**
- **OrderProcessing** → inherits from **MenuManagement**
- **Reporting** → inherits from **Validation**
- **Employee Roles** → inherit from **Employee**

---

## 📁 File Structure

```
RMS/
│
├── main.cpp                    # Main driver program
├── RMS_headers.h               # Central header file with all includes
│
├── validationFile.cpp          # Validation base class
├── InventoryFile.cpp           # Inventory management
├── MenuManagement.cpp          # Menu CRUD operations
├── orderProcessing.cpp         # Order handling
├── employee.cpp                # Employee & role management
├── BillingAndReport.cpp        # Billing and reporting
│
├── Data Files/
│   ├── Inventory.txt           # Ingredient stock data
│   ├── menu.csv                # Menu items database
│   ├── Employeedata.txt        # Employee records
│   ├── Customerdata.txt        # Customer transactions
│   ├── SalesReport.txt         # Sales history
│   └── CustomerFeedback.txt    # Feedback and ratings
│
└── README.md
```

---

## 🎯 Role-Based Features

### 🏆 Restaurant Owner
**Full System Access**:
- Add/Update/Remove stock
- Manage employees
- View profit/loss reports
- Access sales analytics
- View sorted price lists
- Monthly revenue reports
- Salary management

### 👔 Manager
**Operational Control**:
- Stock management
- Employee administration
- Price list access
- Salary records view
- Limited financial reports

### 💵 Cashier
**Customer-Facing Operations**:
- Add new customers
- Generate bills
- View customer records
- Process payments
- Access employee data (view-only)

### 🍽️ Customer
**Ordering Interface**:
- Place orders
- View order details
- View bill
- Modify orders
- Provide feedback

---

## ⚙️ Technical Implementation

### Data Persistence
| Feature | File Format | Purpose |
|---------|-------------|---------|
| Inventory | TXT (CSV-style) | Ingredient tracking |
| Menu | CSV | Menu items database |
| Employees | TXT (CSV-style) | Staff records |
| Customers | TXT (CSV-style) | Customer data |
| Sales | TXT (CSV-style) | Revenue tracking |
| Feedback | TXT (CSV-style) | Customer reviews |

### Key Algorithms

#### Password Hashing
```cpp
unsigned int Hash(string data) {
    unsigned int result = 0;
    for (unsigned int ch : data)
        result = ch + (result << 4) + (result << 10) - result;
    return result;
}
```

#### Automatic Price Calculation
```
Selling Price = Sum(Ingredient Prices) × 1.05
Final Bill = Subtotal + (GST × 13%) + (Service Tax × 2%) + Tip
```

#### Inventory Auto-Restock
- Monitors stock status
- Adds 15 units when status = 'N'
- Updates status to 'Y'

---

## 🚀 Setup Instructions

### Prerequisites
- C++17 compatible compiler (g++, MinGW, MSVC)
- Standard Template Library (STL) support

### Compilation

```bash
# Using g++
g++ -std=c++17 main.cpp -o RMS

# Using MinGW
g++ -std=c++17 main.cpp -o RMS.exe

# Run
./RMS
```

### First Time Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/TasbihaNasir/RMS.git
   cd RMS
   ```

2. **Ensure data files exist** (create if missing):
   - Inventory.txt
   - menu.csv
   - Employeedata.txt
   - Customerdata.txt
   - SalesReport.txt
   - CustomerFeedback.txt

3. **Compile and run**
   ```bash
   g++ -std=c++17 main.cpp -o RMS
   ./RMS
   ```

---

## 📊 Data Format Examples

### Inventory.txt
```
Flour,11,50,Y
Sugar,0,40,N
Chicken Thighs,8,250,Y
```
Format: `Name,Quantity(KG),Price,Stock Status(Y/N)`

### menu.csv
```
Pancakes,90,dessert,91.05
Roti,60,entree,61.05
```
Format: `ItemName,CostPrice,Category,SellingPrice`

### Employeedata.txt
```
=========== EMPLOYEE DATA =========
Login ID,Role,First Name,Last Name,Salary,Password
100,Manager,Tasbiha,Nasir,50000,2550816836
```

### SalesReport.txt
```
2024-01-15,1500.50
2024-02-20,2000.75
```
Format: `Date,Revenue`

---

## 🔒 Security Features

- **Password Hashing**: All passwords stored as hashed values
- **Role-Based Access Control (RBAC)**: Different permissions per role
- **Input Validation**: Comprehensive validation on all user inputs
- **Data Integrity**: Exception handling throughout system
- **Secure Authentication**: Login ID + hashed password verification

---

## 💡 Key Design Patterns

### Object-Oriented Principles
- **Inheritance**: Multi-level inheritance hierarchy
- **Polymorphism**: Virtual functions and method overriding
- **Encapsulation**: Private data members with public interfaces
- **Abstraction**: Base classes with derived implementations

### Design Patterns Used
- **Template Method**: Validation base class
- **Factory**: Role-based user creation
- **Singleton**: Restaurant name constant
- **Strategy**: Multiple payment methods

---

## 📈 Business Logic

### Profit Calculation
```
Revenue = Sum of all sales
Cost = Sum of ingredient costs
Profit = Revenue - Cost
```

### Inventory Management
- Automatic quantity reduction when menu items are created
- Restock threshold monitoring
- Out-of-stock prevention

### Pricing Strategy
- Cost-plus pricing (5% markup)
- Tax inclusion (13% GST + 2% Service Tax)
- Optional tipping system

---

## 🎨 User Experience Features

### Menu Display
- Category-based organization
- Formatted tables with proper alignment
- Clear pricing information
- Easy-to-read layout

### Error Handling
- Try-catch blocks throughout
- Meaningful error messages
- Input validation feedback
- File operation error handling

### User Guidance
- Clear menu options
- Step-by-step prompts
- Validation feedback
- Success/failure confirmations

---

## 🔮 Future Enhancements

- [ ] Database integration (MySQL/PostgreSQL)
- [ ] GUI implementation (Qt/wxWidgets)
- [ ] Table reservation system
- [ ] Delivery management module
- [ ] Multi-location support
- [ ] Loyalty program integration
- [ ] Online ordering interface
- [ ] Real-time inventory alerts
- [ ] Advanced analytics dashboard
- [ ] Mobile app integration
- [ ] Payment gateway integration
- [ ] QR code menu generation
- [ ] Kitchen display system
- [ ] Automated email receipts

---

## 🐛 Known Issues & Limitations

- File-based storage (no concurrent access support)
- No network/multi-user capability
- Limited to console interface
- Manual data backup required
- No transaction rollback mechanism
- Fixed ingredient list per menu item


---

## 📄 License

This project was created as an academic project for university coursework.

---

## 🙏 Acknowledgments

- FAST University for project guidance
- C++ Standard Library documentation
- Restaurant industry best practices
- Open source community for inspiration

---

## 📝 Code Documentation

### Main Functions Overview

#### Inventory Management
- `addItems()` - Add new ingredient to inventory
- `restock()` - Replenish out-of-stock items
- `view()` - Display all inventory items
- `show()` - Show items needing restock

#### Menu Management
- `additems()` - Create new menu items from ingredients
- `RemoveItems()` - Delete menu items
- `UpdateItem()` - Modify existing items
- `displayMenu()` - Show formatted menu

#### Order Processing
- `placeOrder()` - Create new customer order
- `modifyOrder()` - Update existing order
- `cancelOrder()` - Clear current order
- `printOrder()` - Display order summary

#### Billing
- `GenerateBill()` - Create formatted bill with taxes
- `CalculateProfit()` - Compute profit margins
- `CustomerFeedback()` - Collect ratings and comments

#### Reporting
- `GenerateSalesReport()` - Analyze revenue trends
- `GenerateCustomerFeedbackReports()` - Review ratings

#### Employee Management
- `addEmployee()` - Register new staff member
- `removeEmployee()` - Delete employee record
- `updateEmployeeInfo()` - Modify employee data
- `display_EmployeeData()` - View all employees

---

## 🏁 Conclusion

ZAMATA RMS is a comprehensive restaurant management solution demonstrating professional software engineering practices including object-oriented design, data persistence, input validation, and modular architecture. The system provides role-based access control, real-time inventory tracking, automated billing, and business analytics—all essential features for modern restaurant operations.

---

**💡 Developed By**

Tasbiha Nasir, Madiha Aslam, and Zain Saqib  
*Full Stack Developers | ZAMATA RMS Team*  
*Restaurant Management System Project*

---
*
