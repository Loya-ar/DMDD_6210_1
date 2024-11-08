# Project Overview

This project sets up an inventory and order management database with various tables, views, and user roles, each with specific permissions. The goal is to allow different types of users to interact with the database based on their roles—some users will manage inventory, others will track influencer sales performance, and so on. Here’s a clear breakdown of each step involved to make this setup as smooth as possible.

## Step-by-Step Setup

### Step 1: Start with the APP_ADMIN User

The setup begins with the System DBA (Database Administrator) creating an admin user called `APP_ADMIN`. This user, `APP_ADMIN`, will be in charge of setting up the rest of the database and managing other users, tables, and views.

- Log in as System DBA and create the `APP_ADMIN` user.
- Grant `APP_ADMIN` the necessary permissions to manage tables, views, and users.
  - This includes permissions for creating tables, views, managing user permissions, and handling general database operations.

By setting up `APP_ADMIN` first, we’re creating a "superuser" who will oversee the setup and manage access for other users in the system.

### Step 2: Create the Database Tables (DDL Script)

Once `APP_ADMIN` is set up, log in as `APP_ADMIN` to start creating the tables required for the project. These tables include `Users`, `Orders`, `Order_Details`, `Products`, and `Influencers`.

- Run the DDL script for each table, which will define the structure of each table in the database.
- The script will ensure that, if a table already exists, it will be dropped before being recreated. This approach prevents errors from multiple runs and allows you to re-run the setup as needed.

These tables are the foundation of the database, holding the data on users, orders, products, and influencers. Each table also includes primary keys and foreign keys to maintain relationships and data integrity across the database.

### Step 3: Add Sample Data to the Tables (DML Script)

With the tables set up, the next step is to populate them with some sample data. This will make it easier to test the views and permissions later on.

- Run the DML script to insert data into each table. This script adds a few rows to each table—enough to provide meaningful data for testing the views and permissions.
- Make sure to commit the data once it’s been added, so it’s saved in the database and available for testing.

Adding sample data now will allow us to see real results in the views and validate that each user role only has access to the data they’re supposed to see.

### Step 4: Create Views for Summarized Data

With tables and data in place, the next step is to create views, which provide summarized data from the tables. These views will make it easy for different user roles to access relevant information, like inventory levels, regional sales data, influencer performance, and customer purchase histories.

- Run the view creation script for each view. Each view is created using a "replace if exists" approach to allow for multiple runs.
- Key views include:
  - **Current Inventory Status**: Shows product stock levels.
  - **Total Sales by Region**: Summarizes sales data by geographical region.
  - **Influencer Sales Performance**: Tracks revenue generated by each influencer.
  - **Customer Purchase Behavior**: Summarizes purchase history for each customer.
  - **Order Fulfillment Status**: Provides the status of each order.

Each view is tailored to a specific need, making it easy for users to retrieve the insights they need without direct access to the raw data.

### Step 5: Set Up Users and Assign Permissions

With views ready, set up specific users and assign them appropriate permissions. Each user will have access to specific views and tables based on their role in the system.

1. Create each user with a defined role:
   - **APP_ADMIN**: The superuser with full access to all tables and views.
   - **INVENTORY_MANAGER**: Has access to inventory and order-related data, allowing them to manage product stock levels and check order statuses.
   - **INFLUENCER_USER**: Has access to influencer-related data, including product and sales information.
   - **APP_USER**: The end-user, who can place orders and view their purchase history.
2. Grant specific view access to each user. For example:
   - **INVENTORY_MANAGER** can access views related to inventory management.
   - **INFLUENCER_USER** can access views that track influencer performance and product details.
   - **APP_USER** can view their own purchasing history and order statuses.

By assigning these roles and permissions, we’re implementing role-based access control. This means each user can only access the data relevant to their role, helping maintain security and data privacy within the system.

### Step 6: Validate Each User’s Permissions

After setting up users and permissions, log in as each user to confirm they have access only to their relevant data.

1. Log in as `APP_ADMIN` and verify that all views and tables are accessible, as `APP_ADMIN` has full access.
2. Log in as `INVENTORY_MANAGER` and confirm they can only access inventory views and order-related tables.
3. Log in as `INFLUENCER_USER` and check that they have access to influencer-specific views but cannot access other restricted data.
4. Log in as `APP_USER` and ensure they can only view their order and purchase history, with no access to unrelated data.
