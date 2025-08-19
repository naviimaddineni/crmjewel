
# CRM Application for Jewel Maintainance: Project Documentation

[Watch Demo Video](https://drive.google.com/file/d/1Q83hncz8eUlS61A83Ui15aPf71xsBgKV/view?usp=drive_link)

## Table of Contents

- Data Model: Creating Custom Objects
- User Interface: Tabs and Lightning App
- Object Relationships
- Field Creation
- UI Control and Data Validation
- Security: Profiles, Roles, and Users
- Page Layouts
- Automation
- Reports and Dashboards

## 1. Data Model: Creating Custom Objects

The foundation of the application is built on five custom objects designed to store and manage all relevant data.

### 1.1. Jewel Customer

- Stores information about customers.
- **Label**: `Jewel Customer`
- **Plural Label**: `Jewel Customers`
- **Record Name**: `Customer name` (Data Type: Text)
- **Features**: Allow Reports, Allow Search

### 1.2. Item

- Manages the inventory of gold and silver items.
- **Label**: `Item`
- **Plural Label**: `Items`
- **Record Name**: `Item Id` (Data Type: Auto Number, Format: `Item-{00}`)
- **Features**: Allow Reports, Allow Search

### 1.3. Customer Order

- Tracks orders placed by customers.
- **Label**: `Customer Order`
- **Plural Label**: `Customer Orders`
- **Record Name**: `Customer Order Id` (Data Type: Auto Number, Format: `CO-{000}`)
- **Features**: Allow Reports, Allow Search

### 1.4. Price

- Stores and manages the pricing of precious metals.
- **Label**: `Price`
- **Plural Label**: `Prices`
- **Record Name**: `Price Id` (Data Type: Auto Number, Format: `PR-{000}`)
- **Features**: Allow Reports, Allow Search

### 1.5. Billing

- Handles billing and payment information for orders.
- **Label**: `Billing`
- **Plural Label**: `Billings`
- **Record Name**: `Billing Id` (Data Type: Auto Number, Format: `BL-{000}`)
- **Features**: Allow Reports, Allow Search

## 2. User Interface: Tabs and Lightning App

To ensure easy user access and a consolidated experience, custom tabs and a dedicated Lightning App are configured.

### 2.1. Custom Tabs

Custom tabs are created for each of the five objects (`Jewel Customer`, `Item`, `Customer Order`, `Price`, `Billing`) by navigating to **Setup > Tabs**.

### 2.2. Jewelry Inventory System Lightning App

A custom Lightning App centralizes all components of the system.

- **App Name**: `Jewelry Inventory System`
- **Navigation Style**: Console Navigation
- **Navigation Items**: `Jewel Customer`, `Item`, `Customer Order`, `Price`, `Billing`, `Reports`, `Dashboard`
- **Assigned Profiles**: `System Administrator`

## 3. Object Relationships

Relationships are established to link objects and create a logical data structure, which can be visualized using the **Schema Builder**.

- **Lookup Relationship**: A lookup field `Customer` is created on the `Customer Order` object, linking it to the `Jewel Customer` object.
- **Master-Detail Relationship**: A master-detail field `Item` is created on the `Customer Order` object, linking it to the `Item` object.

## 4. Field Creation

Custom fields are added to each object to capture detailed information.

### 4.1. Jewel Customer Fields

| Field Label    | Data Type | Details       |
|----------------|-----------|--------------|
| City           | Text      | Length: 20   |
| Phone          | Phone     |              |
| State          | Text      | Length: 20   |
| Street         | Text      | Length: 20   |
| Country        | Text      | Length: 18   |
| Zip/Postal code| Text      | Length: 6    |

### 4.2. Price Fields

| Field Label    | Data Type | Details                 |
|----------------|-----------|------------------------|
| Gold Price     | Currency  | Length: 8, Decimals: 5 |
| Silver Price   | Currency  | Length: 8, Decimals: 5 |

### 4.3. Item Fields

*(Add table as needed, following your format above for all the fields and formulas.)*

### 4.4. Customer Order Fields

| Field Label | Data Type | Details                              |
|-------------|-----------|--------------------------------------|
| Order Status| Picklist  | Values: Started, On Hold, Completed...|

### 4.5. Billing Fields

*(Add table as needed, following your format above.)*

## 5. UI Control and Data Validation

### 5.1. Field Dependencies

A dependency is configured on the `Item` object.

- **Controlling Field**: `Priority`
- **Dependent Field**: `Expected Days of Return`
- **Logic**: The available return day options change based on the selected priority level.

### 5.2. Validation Rules

- **Jewel Customer - Postal Code**: Ensures the `Zip/Postal code` field is a 6-digit number.
- **Jewel Customer - Required Fields**: Enforces that `City`, `Country`, `Phone`, `State`, and `Street` are not blank.
- **Item - Required Fields**: Ensures all key financial and descriptive fields on the `Item` record are filled before saving.

## 6. Security: Profiles, Roles, and Users

### 6.1. Profiles

- **Gold Smith Profile**: Cloned from `System Administrator`, with full CRUD access to all custom objects.
- **Worker Profile**: Cloned from `Salesforce Platform User`, with R/C/E access to `Item`, `Price`, and `Customer Order`.

### 6.2. Roles

- **Gold Smith Role**: An upper-level role.
- **Worker Role**: Reports directly to `Gold Smith`.

### 6.3. Users

- **Sample User**: Niklaus Mikaelson (Gold Smith profile and role).
- **Sample User**: Elijah Worker (Worker profile and role).

### 6.4. Permission Set

- **Label**: `Per to Worker`
- **Permissions**: R/C/E access to `Item` object.
- **Assignment**: Workers.

## 7. Page Layouts

A custom page layout enhances the user experience for different item types.

- **Object**: `Item`
- **Page Layout Name**: `Page Layout for Gold`
- **Configuration**: Shows only relevant fields for Gold items.

## 8. Automation

### 8.1. Apex Trigger for Billing

- **Trigger**: `UpdatePaidAmountTrigger`
- **Handler**: `UpdatePaidAmountTriggerHandler`
- **Purpose**: Automatically calculate `Paid_Amount__c` on a `Billing` record.

### 8.2. Record-Triggered Flow for Email

- **On Billing**
- Automatically sends a formatted email to customer when a Billing record is created or updated.

## 9. Reports and Dashboards

- **Report Creation**: Users can create custom reports by navigating to the Reports tab.
- **UI Customization**: `Reports` and `Dashboards` tabs are added to app navigation.



## ERD <img width="1164" height="631" alt="ERD_Salesforce" src="https://github.com/user-attachments/assets/f2441f61-d005-4679-9ee2-34e60095f5b0" />


## Conclusion

The Jewelry Inventory System presents a robust solution for managing customers, items, orders, pricing, and billing within a streamlined Salesforce environment. By leveraging custom objects, automated processes, tailored layouts, and strong security controls, this application ensures accuracy, transparency, and efficiency for jewelry businesses. The modular design enables easy customization and future scalability, while comprehensive reporting and dashboard tools empower users to make data-driven decisions. This project demonstrates best practices in Salesforce application development and provides a solid foundation for expanding CRM functionality in other domains.


