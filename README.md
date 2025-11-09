# Oil Shop Management System

A comprehensive web-based management system for oil shops with barcode scanning, inventory tracking, sales management, and reporting features.

## Features

### 🎯 Core Features
- **Barcode Scanning Integration** - Quick product lookup and sales processing
- **Inventory Management** - Real-time stock tracking with low stock alerts
- **Sales & Billing** - Complete POS system with invoice generation
- **Supplier Management** - Track suppliers and purchase orders
- **User Management** - Role-based access control (Admin, Manager, Staff)
- **Reports & Analytics** - Comprehensive sales and inventory reports with charts
- **Modern UI** - Responsive design with Bootstrap 5

### 🔒 Security Features
- Password hashing with Werkzeug
- Role-based access control
- Session management with Flask-Login
- Input validation and SQL injection prevention

### 📊 Reporting Features
- Daily/Monthly sales reports
- Product sales analysis
- Low stock alerts
- Revenue tracking
- PDF invoice generation

## Technology Stack

- **Backend**: Python 3.8+, Flask
- **Database**: MySQL
- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **UI Framework**: Bootstrap 5
- **Charts**: Chart.js
- **Icons**: Bootstrap Icons
- **PDF Generation**: ReportLab

## Installation

### Prerequisites
- Python 3.8 or higher
- MySQL Server 5.7 or higher
- pip (Python package manager)

### Step 1: Clone or Download the Project

```bash
# If using git
git clone <repository-url>
cd oil-shop-management

# Or extract the downloaded ZIP file
```

### Step 2: Install Python Dependencies

```bash
pip install -r requirements.txt
```

### Step 3: Setup MySQL Database

1. Start your MySQL server
2. Open MySQL command line or MySQL Workbench
3. Run the database initialization script:

```bash
mysql -u root -p < database_init.sql
```

Or manually execute the SQL file in MySQL Workbench.

### Step 4: Configure Database Connection

Edit `app.py` and update the database configuration:

```python
DB_CONFIG = {
    'host': 'localhost',
    'user': 'root',
    'password': 'your_mysql_password',  # Change this!
    'database': 'oil_shop_db'
}
```

### Step 5: Create Required Directories

Create the following directory structure:

```
oil-shop-management/
├── app.py
├── requirements.txt
├── database_init.sql
├── templates/
│   ├── base.html
│   ├── login.html
│   ├── dashboard.html
│   ├── sales.html
│   ├── inventory.html
│   ├── suppliers.html
│   ├── reports.html
│   └── users.html
└── static/ (optional, for custom assets)
```

### Step 6: Run the Application

```bash
python app.py
```

The application will start on `http://localhost:5000`

## Default Login Credentials

- **Username**: admin
- **Password**: admin123

⚠️ **Important**: Change the default admin password after first login!

## Usage Guide

### 1. Dashboard
- View today's sales and monthly revenue
- Check low stock alerts
- Access recent sales
- Quick navigation to all modules

### 2. Sales (Point of Sale)
- **Barcode Scanning**: Focus on the barcode input field and scan products
- **Manual Search**: Type product name to search
- **Quick Add**: Click on popular products for quick addition
- **Cart Management**: Adjust quantities, remove items
- **Checkout**: Enter customer details, apply discounts, select payment method
- **Invoice**: Print or download PDF invoices

### 3. Inventory Management
- View all products with stock levels
- Add new products with barcode, pricing, and supplier info
- Edit existing products
- Search and filter by category
- Color-coded stock levels (red = low, yellow = medium, green = good)

### 4. Supplier Management
- Add and manage supplier information
- Track contact details and addresses
- Link suppliers to products

### 5. Reports & Analytics
- Filter reports by date range
- View sales trends with charts
- Analyze product performance
- Track revenue and average sale value
- Export detailed sales reports

### 6. User Management (Admin Only)
- Create new users with different roles
- Manage user permissions
- Delete users

## Role Permissions

### Admin
- Full system access
- Manage users
- Delete any records
- View all reports
- Manage products, suppliers, and settings

### Manager
- Manage products and suppliers
- Process sales
- View reports
- Cannot delete users or critical data

### Staff
- Process sales only
- View inventory
- View limited reports
- No management access

## Barcode Scanner Setup

### Hardware Barcode Scanner
1. Connect USB barcode scanner to your computer
2. The scanner acts as a keyboard input device
3. Focus on the barcode input field in the Sales page
4. Scan any product barcode

### Supported Barcode Formats
- EAN-13
- UPC-A
- Code-128
- Any standard retail barcode format

## Database Schema

### Tables
- **products** - Product information and inventory
- **sales** - Sales transactions
- **sale_items** - Individual items in each sale
- **suppliers** - Supplier information
- **employees** - System users and authentication

### Relationships
- Products → Suppliers (Many-to-One)
- Sales → Employees (Many-to-One)
- Sales → Sale Items (One-to-Many)
- Sale Items → Products (Many-to-One)

## API Endpoints

### Products
- `GET /api/products` - List all products
- `GET /api/products/<barcode>` - Get product by barcode
- `POST /api/products` - Add new product
- `PUT /api/products/<id>` - Update product
- `DELETE /api/products/<id>` - Delete product

### Sales
- `GET /api/sales` - List sales (with date filter)
- `POST /api/sales` - Create new sale
- `GET /api/sales/<id>/items` - Get sale items
- `GET /api/sales/<id>/invoice` - Generate PDF invoice

### Suppliers
- `GET /api/suppliers` - List all suppliers
- `POST /api/suppliers` - Add new supplier
- `PUT /api/suppliers/<id>` - Update supplier
- `DELETE /api/suppliers/<id>` - Delete supplier

### Dashboard
- `GET /api/dashboard/stats` - Get dashboard statistics
- `GET /api/inventory/low-stock` - Get low stock products

### Users
- `GET /api/users` - List all users (Admin only)
- `POST /api/users` - Create new user (Admin only)
- `DELETE /api/users/<id>` - Delete user (Admin only)

## Troubleshooting

### Database Connection Error
- Verify MySQL is running
- Check database credentials in `app.py`
- Ensure database `oil_shop_db` exists

### Port Already in Use
Change the port in `app.py`:
```python
app.run(debug=True, host='0.0.0.0', port=5001)
```

### Import Errors
Reinstall dependencies:
```bash
pip install -r requirements.txt --force-reinstall
```

### Barcode Scanner Not Working
- Ensure scanner is in HID/keyboard mode
- Test scanner in a text editor first
- Check USB connection
- Focus must be on the barcode input field

## Production Deployment

### Security Checklist
1. Change `app.secret_key` to a secure random value
2. Set `debug=False` in `app.run()`
3. Use environment variables for database credentials
4. Enable HTTPS
5. Configure firewall rules
6. Regular database backups
7. Change default admin password

### Recommended Production Setup
- Use Gunicorn or uWSGI as WSGI server
- Nginx as reverse proxy
- SSL certificate (Let's Encrypt)
- Automated backups
- Monitoring and logging

### Example Production Command
```bash
gunicorn -w 4 -b 0.0.0.0:8000 app:app
```

## Backup & Restore

### Backup Database
```bash
mysqldump -u root -p oil_shop_db > backup_$(date +%Y%m%d).sql
```

### Restore Database
```bash
mysql -u root -p oil_shop_db < backup_20240101.sql
```

## Support & Maintenance

### Regular Maintenance Tasks
1. Weekly database backups
2. Monitor disk space for invoice storage
3. Review user access logs
4. Update stock levels from physical inventory
5. Clear old session data

### Updating Products
- Use CSV import for bulk updates (feature can be added)
- Update prices seasonally
- Review and adjust minimum stock levels

## Future Enhancements

Potential features to add:
- Mobile app integration
- Customer loyalty program
- Email notifications for low stock
- Barcode label printing
- Multi-location support
- Advanced analytics and forecasting
- Integration with accounting software
- SMS notifications
- WhatsApp integration for order updates

## License

This project is provided as-is for educational and commercial use.

## Credits

Developed using modern web technologies and best practices for retail management systems.

---

For questions or issues, please refer to the documentation or contact your system administrator.