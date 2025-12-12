# Database Seeders Implementation

A comprehensive database seeding system for the Lantaw TBD Backend project. This implementation provides Django management commands to populate the database with realistic test data for development and testing environments.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [File Structure](#file-structure)
- [Seeder Details](#seeder-details)
- [Dependencies](#dependencies)
- [Data Relationships](#data-relationships)
- [Cleanup Utility](#cleanup-utility)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## 🎯 Overview

This seeding system consists of 7 Django management commands organized by application module. Each seeder populates specific database models with realistic test data using the `django-seed` library and Faker for data generation.

### What Gets Seeded

- **Users**: Admin, Executive, and Project Staff accounts
- **Projects**: Sample projects with various statuses and grant amounts
- **Personnel**: Roles, departments, and personnel records
- **Budget**: Budget line items and compensation records
- **Activities**: Objectives and activities linked to projects and budgets
- **Core**: Placeholder for future core app data

## ✨ Features

- ✅ **Idempotent Operations**: Safe to run multiple times without creating duplicates
- ✅ **Dependency Management**: Automatic checking and validation of required dependencies
- ✅ **Realistic Data**: Uses Faker library for authentic-looking test data
- ✅ **Modular Design**: Each app has its own seeder for easy maintenance
- ✅ **Master Seeder**: Single command to seed all data in correct order
- ✅ **Cleanup Utility**: Command to remove all seeded data safely
- ✅ **User Feedback**: Colored console output with progress messages
- ✅ **Error Handling**: Clear error messages when dependencies are missing

## 📦 Prerequisites

- Django 6.0+
- Python 3.x
- `django-seed` library (v0.3.1)

## 🔧 Installation

The required dependency is already included in `requirements.txt`:

```bash
django-seed==0.3.1
```

If you need to install it separately:

```bash
pip install django-seed
```

## 🚀 Usage

### Seed All Data

To seed all database tables with test data:

```bash
python manage.py seed_data
```

This command executes all seeders in the correct dependency order:
1. Users
2. Projects
3. Personnel
4. Budget
5. Activities
6. Core

### Seed Individual Apps

You can also run individual seeders:

```bash
# Seed users only
python manage.py seed_users

# Seed projects only
python manage.py seed_projects

# Seed personnel only
python manage.py seed_personnel

# Seed budget only
python manage.py seed_budget

# Seed activities only
python manage.py seed_activities

# Seed core (placeholder)
python manage.py seed_core
```

**Note**: Individual seeders check for required dependencies and will display error messages if prerequisites are missing.

### Cleanup Seeded Data

To remove all seeded data from the database:

```bash
python manage.py cleanup_seeded_data
```

This command deletes all seeded data in reverse dependency order to prevent foreign key constraint violations.

## 📁 File Structure

```
lantaw/
├── core/
│   └── management/
│       └── commands/
│           ├── seed_data.py              # Master seeder (orchestrates all)
│           ├── seed_core.py              # Core app seeder (placeholder)
│           └── cleanup_seeded_data.py    # Cleanup utility
├── users/
│   └── management/
│       └── commands/
│           └── seed_users.py             # User accounts seeder
├── projects/
│   └── management/
│       └── commands/
│           └── seed_projects.py          # Projects seeder
├── personnel/
│   └── management/
│       └── commands/
│           └── seed_personnel.py         # Personnel, roles, departments seeder
├── budget/
│   └── management/
│       └── commands/
│           └── seed_budget.py            # Budget items and compensations seeder
└── activities/
    └── management/
        └── commands/
            └── seed_activities.py       # Objectives and activities seeder
```

## 📝 Seeder Details

### 1. Users Seeder (`seed_users`)

**File**: `lantaw/users/management/commands/seed_users.py`

**Creates**:
- 1 Admin user (`admin@lantaw.com` / `admin123`)
- 1 Executive user (`executive@lantaw.com` / `executive123`)
- 3 Project Staff users (Faker-generated names / `staff123`)

**Features**:
- Sets proper roles (ADMIN, EXECUTIVE, PROJECT_STAFF)
- All accounts set to ACTIVE status
- Secure password hashing
- Prevents duplicate creation

**Dependencies**: None (foundation seeder)

---

### 2. Projects Seeder (`seed_projects`)

**File**: `lantaw/projects/management/commands/seed_projects.py`

**Creates**:
- 3 Projects with:
  - Faker-generated names (catch phrases)
  - Descriptions (200 characters)
  - Grant amounts (₱1M - ₱10M)
  - Statuses: 2 ACTIVE, 1 ON_HOLD
  - Realistic date ranges
- Project memberships linking users to projects

**Features**:
- Dynamic date generation (start: 15-60 days ago, end: 180-730 days ahead)
- Automatic project member assignment
- Status variety for testing

**Dependencies**: Requires `seed_users` to be run first

---

### 3. Personnel Seeder (`seed_personnel`)

**File**: `lantaw/personnel/management/commands/seed_personnel.py`

**Creates**:
- 5 Roles (Faker-generated job titles, project-specific)
- 4 Departments (from predefined list: Engineering, Design, Operations, etc.)
- 4 Personnel records with names, roles, departments, and employment status

**Features**:
- Project-specific roles and departments
- Mix of employment statuses (3 ACTIVE, 1 INACTIVE)
- Realistic name generation

**Dependencies**: Requires `seed_projects` to be run first

---

### 4. Budget Seeder (`seed_budget`)

**File**: `lantaw/budget/management/commands/seed_budget.py`

**Creates**:
- 3 Budget Line Items: MOOE, PS (Personal Services), CO (Capital Outlay)
- 4 Compensations:
  - SALARY and HONORARIA types
  - Linked to personnel and PS budget item
  - Realistic amounts (₱30K-₱80K for salary, ₱5K-₱20K for honoraria)
  - Effective dates (15-60 days ago)

**Features**:
- Standard budget categories
- Multiple compensation types per personnel
- Realistic financial data

**Dependencies**: Requires `seed_projects` and `seed_personnel` to be run first

---

### 5. Activities Seeder (`seed_activities`)

**File**: `lantaw/activities/management/commands/seed_activities.py`

**Creates**:
- 2 Objectives (linked to first project, Faker-generated titles)
- 5 Activities:
  - Linked to objectives
  - Various statuses (COMPLETED, ACTIVE, PENDING)
  - Linked to budget items (MOOE, PS, CO)
  - Projected expenses (₱10K-₱100K)
  - Actual expenses for completed activities only

**Features**:
- Objective-Activity relationship modeling
- Status-based expense calculation
- Budget item allocation

**Dependencies**: Requires `seed_projects` and `seed_budget` to be run first

---

### 6. Core Seeder (`seed_core`)

**File**: `lantaw/core/management/commands/seed_core.py`

**Status**: Placeholder (no models to seed currently)

**Purpose**: Maintains consistency in seeder structure and ready for future expansion

**Dependencies**: None

---

### 7. Master Seeder (`seed_data`)

**File**: `lantaw/core/management/commands/seed_data.py`

**Purpose**: Orchestrates all individual seeders in the correct dependency order

**Execution Order**:
1. `seed_users` (foundation)
2. `seed_projects` (depends on Users)
3. `seed_personnel` (depends on Projects)
4. `seed_budget` (depends on Projects & Personnel)
5. `seed_activities` (depends on Projects & Budget)
6. `seed_core` (placeholder)

**Output**: Success messages for each seeder and final confirmation

---

## 🔗 Dependencies

### External Libraries

- **django-seed (v0.3.1)**: Library for generating fake data
- **Faker**: Integrated with django-seed for realistic data generation

### Internal Dependencies

The seeders have the following dependency chain:

```
Users (no dependencies)
    ↓
Projects (requires Users)
    ↓
Personnel (requires Projects)
    ↓
Budget (requires Projects + Personnel)
    ↓
Activities (requires Projects + Budget)
    ↓
Core (no dependencies, placeholder)
```

Each seeder checks for required dependencies and displays helpful error messages if prerequisites are missing.

## 🔄 Data Relationships

The seeded data creates realistic relationships:

- **Users** → **Projects** (via ProjectMembers)
- **Projects** → **Roles** & **Departments**
- **Projects** → **BudgetLineItems**
- **Personnel** → **Roles** & **Departments**
- **Personnel** → **Compensations** → **BudgetLineItems**
- **Projects** → **Objectives** → **Activities** → **BudgetLineItems**

## 🧹 Cleanup Utility

**File**: `lantaw/core/management/commands/cleanup_seeded_data.py`

The cleanup utility safely removes all seeded data in reverse dependency order:

1. Activities
2. Objectives
3. Compensations
4. Budget Line Items
5. Personnel
6. Roles & Departments
7. Project Members
8. Projects
9. Seeded Users (admin, executive, project staff with @lantaw.com)

**Usage**:
```bash
python manage.py cleanup_seeded_data
```

**Features**:
- Safe deletion respecting foreign key constraints
- Detailed count reporting for each deletion
- Colored output for better visibility
- Summary report at the end

## 💡 Best Practices

### 1. Idempotency
All seeders use `get_or_create()` to prevent duplicate data. They're safe to run multiple times.

### 2. Dependency Checking
Each seeder validates required dependencies before proceeding, providing clear error messages.

### 3. Realistic Data
Uses Faker for authentic-looking data with proper date ranges, amounts, and relationships.

### 4. Error Handling
Graceful failure with informative error messages guiding users to fix issues.

### 5. User Feedback
Colored console output (SUCCESS, WARNING, ERROR) provides clear feedback during execution.

### 6. Modular Design
Each app manages its own seeder, making the codebase maintainable and extensible.

## 🐛 Troubleshooting

### Issue: "Users not found. Please run seed_users first."

**Solution**: Run the seeders in order, starting with `seed_users`:
```bash
python manage.py seed_users
python manage.py seed_projects
# ... etc
```

Or use the master seeder:
```bash
python manage.py seed_data
```

### Issue: Duplicate data warnings

**Solution**: This is normal! The seeders use `get_or_create()` and will warn if data already exists. This is safe and expected behavior.

### Issue: Foreign key constraint errors during cleanup

**Solution**: Use the provided `cleanup_seeded_data` command which handles deletion order automatically.

### Issue: Want to customize seed counts

**Solution**: Edit the individual seeder files. Look for `range()` calls and adjust the numbers:
```python
# Example: Change from 3 to 5 users
for _ in range(5):  # Changed from range(3)
    # ... create user
```

## 📊 Data Statistics

When all seeders are run, approximately **31 database records** are created:

- 5 Users (1 Admin, 1 Executive, 3 Project Staff)
- 3 Projects
- 5 Roles
- 4 Departments
- 4 Personnel
- 3 Budget Line Items
- 4 Compensations
- 2 Objectives
- 5 Activities

All records are properly linked with foreign key relationships.

## 🔮 Future Enhancements

Potential improvements for future versions:

- [ ] Configuration file for customizable seed counts
- [ ] Environment-specific data (dev/staging/prod)
- [ ] Data export/import functionality
- [ ] Progress bars for large datasets
- [ ] Selective seeding (seed only specific apps)
- [ ] Data validation and integrity checks
- [ ] Seed data templates/snapshots

## 📄 License

This implementation is part of the Lantaw TBD Backend project.

## 👥 Contributing

When adding new models or apps:

1. Create a new seeder file following the existing pattern
2. Add it to the master seeder (`seed_data.py`)
3. Update the cleanup utility if needed
4. Document dependencies and relationships
5. Test idempotency (run multiple times)

## 📞 Support

For issues or questions regarding the seeders:

1. Check the error messages - they often guide you to the solution
2. Verify dependencies are seeded in the correct order
3. Review the file structure and ensure all files are in place
4. Check Django management command syntax

---

**Last Updated**: 2024
**Version**: 1.0.0

