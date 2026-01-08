# FLATS HR MANAGEMENT SYSTEM

This is a web-based **HR Management System** (HMS) built with PHP, MySQL, and Bootstrap, designed for managing employees in a flats/apartments context. Developed by AAQIL K.

## Key Technologies and Architecture

- **Backend**: PHP with PDO for database interactions. Sessions handle user authentication.
- **Frontend**: HTML, CSS, JavaScript with Bootstrap for responsive UI. Includes jQuery and custom JS for interactivity.
- **Database**: MySQL (MariaDB 10.11.9), with tables for users, roles, salaries, leaves, borrows, customers, permissions, and more.
- **File Structure**: Organized into `admin/` for backend operations, `assets/` for static files (CSS, JS, images, uploads), and root-level files for login/logout.
- **Security**: Basic login via email/password (hashed passwords in DB). No advanced security like CSRF protection or encryption noted.
- **Deployment**: Runs on Apache (via XAMPP), with PHP 7.2+ and MySQL.

## How It Works

1. **Login Process**:

   - Users access `index.php`, which displays a login form with email/password fields.
   - Form submits to `assets/app/auth.php`, which verifies credentials against the `admin` table.
   - On success, starts a session and redirects to `admin/index.php` (admin dashboard).
   - Failed logins show alerts via `assets/constants/check-reply.php`.

2. **Admin Dashboard (`admin/index.php`)**:

   - Central hub with sidebar navigation (`admin/include/sidebar.php`) for modules like Users, Roles, Salaries, Leaves, Borrows, Reports, Settings.
   - Includes header/footer from `admin/include/` for consistent layout.
   - Uses Bootstrap components for cards, tables, and modals.

3. **Core Modules**:

   - **User Management**: Add/edit/view employees (`admin/Add_User.php`, `admin/Update_User.php`, `admin/View_user.php`). Stores in `admin` table with fields like name, email, salary, role, bank details.
   - **Role & Permissions**: Manage roles (`groups` table) and permissions (`permissions`, `permission_role` tables). Assign access to modules like Salary, Leaves, Borrows.
   - **Salary Management**: Calculate salaries (`admin/add_salary.php`, `admin/view_salary.php`). Factors in leaves, borrows, and actual pay. Stored in `salary` table with monthly/yearly breakdowns.
   - **Leave Management**: Track paid/unpaid leaves (`admin/add_leaves.php`, `admin/view_leaves.php`). Uses `leaves` table with approval workflow.
   - **Borrow/Loan Management**: Handle employee loans (`admin/add_borrow.php`, `admin/view_borrow.php`). Stored in `borrow` table with amounts, reasons, dates.
   - **Reports**: Generate reports on salaries, leaves, borrows, GST, etc. (`admin/salary_report.php`, `admin/app_report.php`). Uses AJAX for dynamic data fetching (`admin/ajax_*.php`).
   - **Customers & Units**: Manage tenants/customers (`customer` table) and units (`unit` table, e.g., for apartments).
   - **Settings**: Update site details (`manage_website` table) like logo, title, currency (INR).
   - **Other Features**: Email config (`tbl_email_config`), alerts (`tbl_alerts`), inventory deductions (`tbl_deduct`), installments (`installement`), backup (`admin/backup/`).

4. **Data Flow**:

   - All operations query/update the MySQL DB via PHP scripts.
   - AJAX calls (`admin/ajax_*.php`) fetch data dynamically (e.g., product details, user info).
   - File uploads handled in `assets/uploadImage/` for profiles, logos, etc.
   - Reports export/print via `admin/print_*.php`.
   - Logout via `logout.php` destroys session.

5. **Workflow Example**:
   - Admin logs in → Navigates to "Add User" → Fills form → Submits to `admin/Operation/User.php` → Inserts into `admin` table → Redirects with success alert.
   - For salaries: Select employee/month → Calculate deductions (leaves, borrows) → Save final amount.

## Limitations/Notes

- No advanced features like real-time notifications, multi-tenancy, or API integrations.
- Basic error handling; relies on PHP's default settings.
- Database has sample data (e.g., employees like Mayuri, Hitesh).
- Appears incomplete or in development (e.g., some tables like `installement` are empty).

## Installation

1. Clone the repository.
2. Import `Database/hr_soft1.sql` into MySQL.
3. Update `assets/constants/config.php` with your DB credentials.
4. Run on XAMPP or similar local server.

## Usage

- Access `index.php` for login.
- Default admin: Check `admin` table in DB.

For more details, refer to the code files.
