# priyanshu_assignment

# Vendor Management System

This Django-based Vendor Management System provides a robust API for managing vendors, purchase orders, and vendor performance metrics.

## Setup Instructions

1. Clone the repository:

2. Create a virtual environment and activate it:

python -m venv venv
source venv/bin/activate  # On Windows use venv\Scripts\activate

3. Install the required packages:

pip install -r requiremnets.txt

4. Apply migrations:

python manage.py migrate

5. Create a superuser (optional):

python manage.py createsuperuser

6. Run the development server:

python manage.py runserver

The API will be available at `http://localhost:8000/api/`.

## API Endpoints

### Vendor Management

- **List all vendors / Create a new vendor**
- `GET/POST /api/vendors/`

- **Retrieve, update, or delete a specific vendor**
- `GET/PUT/DELETE /api/vendors/{vendor_id}/`

- **Retrieve vendor performance metrics**
- `GET /api/vendors/{vendor_id}/performance/`

### Purchase Order Management

- **List all purchase orders / Create a new purchase order**
- `GET/POST /api/purchase_orders/`
- Use query parameter `?vendor_id={vendor_id}` to filter by vendor

- **Retrieve, update, or delete a specific purchase order**
- `GET/PUT/DELETE /api/purchase_orders/{po_id}/`

- **Acknowledge a purchase order**
- `POST /api/purchase_orders/{po_id}/acknowledge/`

## Using the API

1. **Authentication**: 
- The API uses token-based authentication. Include the token in the header of your requests:
  ```
  Authorization: Token your_token_here
  ```

2. **Content Type**:
- Set the content type for POST and PUT requests:
  ```
  Content-Type: application/json
  ```

3. **Example Requests**:

- Create a new vendor:
  ```
  POST /api/vendors/
  {
      "name": "Acme Corp",
      "contact_details": "John Doe, john@acme.com",
      "address": "123 Main St, Anytown, USA",
      "vendor_code": "ACME001"
  }
  ```

- Create a purchase order:
  ```
  POST /api/purchase_orders/
  {
      "po_number": "PO001",
      "vendor": 1,
      "order_date": "2023-01-01T00:00:00Z",
      "delivery_date": "2023-01-15T00:00:00Z",
      "items": {"item1": 10, "item2": 20},
      "quantity": 30,
      "status": "pending",
      "quality_rating": null,
      "issue_date": "2023-01-01T00:00:00Z"
  }
  ```

- Acknowledge a purchase order:
  ```
  POST /api/purchase_orders/1/acknowledge/
  ```

4. **Response Format**:
- Successful responses will return HTTP 200 OK or 201 Created with JSON data.
- Errors will return appropriate HTTP status codes (400, 404, etc.) with error details.

## Testing

To run the test suite:
python manage.py test

## Additional Notes

- The system automatically calculates and updates vendor performance metrics based on purchase order data.
- Historical performance data is stored and can be retrieved for trend analysis.
- Ensure all date fields are in ISO 8601 format (YYYY-MM-DDTHH:MM:SSZ).

