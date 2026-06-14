UBEASISWA

UBEASISWA is a web-based scholarship management system built with Laravel. It allows students to register for scholarships, receive mentoring, get notifications, and enables admins to manage and report scholarship data.


Deployed on AWS EC2 as a live production environment.




✨ Features


Student scholarship registration
Mentoring management
Notification system
Admin dashboard with reporting
Role-based access (Admin / Student)



🚀 Tech Stack

ComponentTechnologyBackendLaravel (PHP)DatabaseMySQLFrontendBlade TemplateDeploymentAWS EC2


⚙️ Local Development Setup

Requirements


PHP >= 8.1
Composer
MySQL
Node.js & NPM (for frontend assets)


Installation

1. Clone the repository

bashgit clone https://github.com/AmosJuang/ubeasiswa.git
cd ubeasiswa

2. Install PHP dependencies

bashcomposer install

3. Install frontend dependencies

bashnpm install && npm run build

4. Configure environment

bashcp .env.example .env
php artisan key:generate

Edit .env and set your database credentials:

envDB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=ubeasiswa
DB_USERNAME=root
DB_PASSWORD=your_password

5. Run database migrations & seeders

bashphp artisan migrate
php artisan db:seed --class=ScholarshipSeeder


⚠️ If you encounter migration conflicts, run:

bashphp artisan migrate:fresh
php artisan db:seed --class=ScholarshipSeeder



6. Verify data

bashphp artisan tinker
# then run:
# \DB::table('scholarships')->get();

7. Start the development server

bashphp artisan serve

App will be available at http://localhost:8000


☁️ AWS EC2 Deployment

This project was deployed on an AWS EC2 instance (Ubuntu) with the following setup:


Web Server: Nginx as reverse proxy
PHP: PHP-FPM
Database: MySQL running on the same instance
Access: Via EC2 public IP / subdomain


Deployment Steps (EC2)

bash# Update & install dependencies
sudo apt update
sudo apt install php php-fpm php-mysql nginx mysql-server composer -y

# Clone project
git clone https://github.com/AmosJuang/ubeasiswa.git /var/www/ubeasiswa

# Set permissions
sudo chown -R www-data:www-data /var/www/ubeasiswa
sudo chmod -R 755 /var/www/ubeasiswa/storage

# Install & configure
cd /var/www/ubeasiswa
composer install --no-dev
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan db:seed --class=ScholarshipSeeder

Configure Nginx to point to /var/www/ubeasiswa/public.


📁 Project Structure

ubeasiswa/
├── app/
│   ├── Http/Controllers/     ← Admin, Student, Auth controllers
│   └── Models/               ← Scholarship, User, Mentoring models
├── database/
│   ├── migrations/           ← Table definitions
│   └── seeders/              ← ScholarshipSeeder
├── resources/views/          ← Blade templates
├── routes/
│   └── web.php               ← Route definitions
└── .env.example              ← Environment template


👤 Default Roles

RoleAccessAdminManage scholarships, mentoring, reportsStudentRegister, view status, receive notifications


📚 References


Laravel Documentation
AWS EC2 Documentation
