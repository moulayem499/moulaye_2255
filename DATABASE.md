# Database Documentation

## Overview

The Container Lookup app uses a JSON-based file database to store container information. The database is stored in `data/containers.json` and is automatically initialized with sample data on first run.

## Database Structure

Each container record contains the following fields:

```json
{
  "id": "unique-id",
  "containerNumber": "ABCD1234567",
  "billOfLading": "BOL001234",
  "supplierName": "Global Trading Co. Ltd.",
  "invoiceNumber": "INV-2024-001234",
  "totalAmount": 50000,
  "depositAmount": 15000,
  "depositPaid": true,
  "balanceAmount": 35000,
  "balancePaid": false,
  "startDate": "2024-01-15",
  "startLocation": "Shanghai, China",
  "endDate": "2024-02-20",
  "portDestination": "Los Angeles, USA",
  "createdAt": "2024-01-01T00:00:00.000Z",
  "updatedAt": "2024-01-01T00:00:00.000Z"
}
```

## Payment Structure

- **Total Amount**: Total invoice amount
- **Deposit (30%)**: 30% of total amount, usually paid as deposit
- **Balance (70%)**: 70% of total amount, paid before shipment

The deposit and balance amounts are automatically calculated when you provide the total amount.

## API Endpoints

### GET `/api/containers`
Get all containers from the database.

### POST `/api/containers`
Create a new container.

**Required fields:**
- `containerNumber`
- `billOfLading`
- `supplierName`
- `invoiceNumber`

**Optional fields:**
- `totalAmount` (will auto-calculate deposit and balance)
- `depositAmount`
- `depositPaid` (default: false)
- `balanceAmount`
- `balancePaid` (default: false)
- `startDate`
- `startLocation`
- `endDate`
- `portDestination`

### GET `/api/containers/[id]`
Get a specific container by ID.

### PUT `/api/containers/[id]`
Update a container by ID.

### DELETE `/api/containers/[id]`
Delete a container by ID.

### GET `/api/search?type=[type]&query=[query]`
Search containers by:
- `container` - Container Number
- `billOfLading` - Bill of Lading
- `supplier` - Supplier Name
- `invoice` - Invoice Number

## Database Location

The database file is stored at:
```
frontend/data/containers.json
```

This file is automatically created on first run with sample data.

## Backup

To backup your database, simply copy the `data/containers.json` file.

## Notes

- The database is file-based and suitable for development and small-scale production
- For larger deployments, consider migrating to a proper database (PostgreSQL, MySQL, MongoDB, etc.)
- The database is automatically initialized with 8 sample containers on first run

