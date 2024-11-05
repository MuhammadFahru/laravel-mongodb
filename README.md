# Laravel MongoDB CRUD Example

This is a simple CRUD (Create, Read, Update, Delete) application using Laravel and MongoDB. The application demonstrates basic product management with image upload functionality.

## Features

- Product CRUD operations
- Image upload and management
- Search functionality by product name
- Price range filter
- Sort by price (ascending/descending)
- Bootstrap 5 UI

## Requirements

- PHP >= 8.1
- MongoDB >= 4.4
- Laravel 11.x
- Composer
- MongoDB PHP Driver

## Installation

1. Clone the repository
```bash
git clone https://github.com/MuhammadFahru/laravel-mongodb
cd laravel-mongodb
```

2. Install dependencies
```bash
composer install
```

3. Create environment file
```bash
cp .env.example .env
```

4. Configure MongoDB connection in `.env`
```env
DB_CONNECTION=mongodb
DB_HOST=127.0.0.1
DB_PORT=27017
DB_DATABASE=laravel_mongodb
DB_USERNAME=
DB_PASSWORD=
```

5. Update database configuration in `config/database.php`:
```php
'default' => env('DB_CONNECTION', 'mongodb'),

'connections' => [
    'mongodb' => [
        'driver' => 'mongodb',
        'dsn' => env('DB_URI', 'mongodb://localhost:27017'),
        'database' => env('DB_DATABASE', 'laravel_mongodb'),
    ],
],
```

6. Create storage symbolic link
```bash
php artisan storage:link
```

## MongoDB Setup

1. Install MongoDB (Ubuntu)
```bash
# Import MongoDB public GPG key
curl -fsSL https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -

# Add MongoDB repository
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list

# Update package list
sudo apt-get update

# Install MongoDB
sudo apt-get install -y mongodb-org

# Start MongoDB service
sudo systemctl start mongod

# Enable MongoDB service on boot
sudo systemctl enable mongod
```

2. Install MongoDB PHP Driver
```bash
sudo pecl install mongodb
```

3. Add MongoDB extension to php.ini
```bash
echo "extension=mongodb.so" | sudo tee -a /etc/php/8.1/cli/php.ini
echo "extension=mongodb.so" | sudo tee -a /etc/php/8.1/fpm/php.ini
```

## Running the Application

1. Start the development server
```bash
php artisan serve
```

2. Access the application at http://localhost:8000/products

## Usage

### Product Management
- View all products: Navigate to `/products`
- Create new product: Click "Add New Product" button
- Edit product: Click "Edit" button on a product row
- Delete product: Click "Delete" button on a product row

### Search and Filter
- Search by name: Enter product name in the search box
- Filter by price: Enter minimum and/or maximum price
- Sort by price: Select sorting order from the dropdown

## Database Structure

### Products Collection
```javascript
{
    "_id": ObjectId,
    "name": String,
    "price": Number,
    "description": String,
    "stock": Number,
    "image": String,
    "created_at": Timestamp,
    "updated_at": Timestamp
}
```

## File Structure

```
laravel-mongodb/
├── app/
│   ├── Http/
│   │   └── Controllers/
│   │       └── ProductController.php
│   └── Models/
│       └── Product.php
├── resources/
│   └── views/
│       └── products/
│           ├── index.blade.php
│           ├── create.blade.php
│           └── edit.blade.php
└── routes/
    └── web.php
```

## Development Notes

- Images are stored in `storage/app/public/products`
- Supported image formats: jpeg, png, jpg, gif
- Maximum image size: 2MB
- MongoDB queries use Laravel's Eloquent-style syntax
- Bootstrap 5 is included via CDN

## Contributing

1. Fork the repository
2. Create a new branch
3. Make your changes
4. Submit a pull request

## License

This project is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).

## Troubleshooting

### Common Issues

1. MongoDB Connection Failed
```bash
# Check if MongoDB service is running:
sudo systemctl status mongod
```

2. Storage Permission Issues
```bash
# Fix storage permissions
sudo chown -R www-data:www-data storage
chmod -R 775 storage
```

3. Image Upload Not Working
```bash
# Check if storage link exists
php artisan storage:link
```

### Need Help?

If you encounter any issues, please:
1. Check the Laravel and MongoDB logs
2. Ensure all requirements are met
3. Create an issue in the repository with:
    - Detailed description of the problem
    - Steps to reproduce
    - Error messages
    - Laravel and MongoDB versions

## Credits

- [Laravel](https://laravel.com)
- [MongoDB](https://www.mongodb.com)
- [Bootstrap](https://getbootstrap.com)
