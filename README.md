# Inventory Management System

This project is an Inventory Management System built with Django, allowing users to manage inventory items, suppliers, and access data through both a web interface and a RESTful API.

## Requirements

- Python (3.6 or higher)
- Django (3.0 or higher)
- Django Rest Framework (3.0 or higher)

## Project Overview

The project includes the following main components:

- **inventory:** Django app managing inventory items, suppliers, and views for the inventory.
- **api:** Django app providing RESTful API endpoints to access inventory data.

The `db.sqlite3` file (the SQLite database) is gitignored to prevent versioning of the database.

## Environment Setup

### Setting up the Environment

#### macOS and Linux

1. Clone the repository.
   ```bash
   git clone https://github.com/gydox/django-ims.git
   ```

2. Create a virtual environment.
   ```bash
   python3 -m venv venv
   ```

3. Activate the virtual environment.
   - macOS/Linux:
     ```bash
     source venv/bin/activate
     ```
   - Windows:
     ```bash
     venv\Scripts\activate
     ```

4. Install dependencies from `requirements.txt`.
   ```bash
   pip install -r requirements.txt
   ```

5. Apply migrations to create database tables.
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

6. Create a superuser to manage the database.
   ```bash
   python manage.py createsuperuser
   ```

### Running the Application

Run the development server:
   ```bash
   python manage.py runserver
   ```

Access the web interface at `http://localhost:8000/` and explore the different views. The Django admin panel is available at `http://localhost:8000/admin/`.

## API Endpoints

### Inventory API Endpoints

#### GET `/api/inventory/`

Retrieves a list of inventory items. This endpoint supports filtering by name using a URL query parameter `name`. Example: `/api/inventory/?name=<query>`.

##### Example Response without Query Parameter

Request: `/api/inventory/`

Response:
```json
[
    {
        "id": 1,
        "name": "Item 1",
        "description": "Description for Item 1",
        "note": "Note for Item 1",
        "stock": 10,
        "availability": true,
        "supplier": {
            "id": 1,
            "name": "Supplier A"
        }
    },
    {
        "id": 2,
        "name": "Item 2",
        "description": "Description for Item 2",
        "note": "Note for Item 2",
        "stock": 15,
        "availability": true,
        "supplier": {
            "id": 2,
            "name": "Supplier B"
        }
    }
    // Other inventory items without filtering...
]
```


##### Example Response with Query Parameter

Request: `/api/inventory/?name=Item 1`

Response:
```json
[
    {
        "id": 1,
        "name": "Item 1",
        "description": "Description for Item 1",
        "note": "Note for Item 1",
        "stock": 10,
        "availability": true,
        "supplier": {
            "id": 1,
            "name": "Supplier A"
        }
    },
    {
        "id": 3,
        "name": "Item 1 Variant",
        "description": "Description for Item 1 Variant",
        "note": "Note for Item 1 Variant",
        "stock": 8,
        "availability": true,
        "supplier": {
            "id": 2,
            "name": "Supplier B"
        }
    }
    // Other inventory items matching the query...
]
```

### Testing

To run tests, execute:
   ```bash
   python manage.py test
   ```

The test cases include:

- `test_inventory_list_page_status`: Checks if the `/inventory` page returns a status code of 200 and contains expected content.
- `test_inventory_detail_page_status`: Checks if the `/inventory/<id>` page returns a status code of 200 and contains expected content.
- `test_api_inventory_page_status`: Checks if the `/api/inventory` API endpoint returns a status code of 200.

This will execute the unit tests to ensure functionality.

## Contributing

If you wish to contribute to this project, please fork the repository, make your changes, and submit a pull request. Contributions are welcome!

