# Product Requirements - VendorVue

## 1. Product Overview
VendorVue is a hyperlocal vendor discovery platform designed to bridge the gap between local street vendors (rehris, kiosks, small shops) and digitally-savvy customers. It provides a mobile-first experience for ordering, tracking, and secure pickup.

## 2. Target Audience
- **Customers**: Individuals looking for convenient discovery and ordering from local nearby vendors.
- **Vendors**: Small-scale hyperlocal businesses wanting to digitize their operations with zero upfront cost.

## 3. User Roles & Capabilities

### 3.1 Customer
- **Discovery**: Find nearby vendors using a location-based map and list view.
- **Filtering**: Filter vendors by distance (0.5km to 5km).
- **Ordering**: Browse digital menus and place orders.
- **Payment**: Pay via integrated wallet or cash (with split payment support).
- **Tracking**: Monitor real-time order status (Pending → Preparing → Ready → Completed).
- **Secure Pickup**: Provide a 4-digit OTP for order verification at pickup.

### 3.2 Vendor
- **Onboarding**: Register and set up a digital storefront in under 5 minutes.
- **Menu Management**: Add, edit, and toggle stock for menu items.
- **Order Management**: Receive new order alerts, update status, and track historical data.
- **Verification**: Verify customer OTPs to finalize order completion.
- **Availability**: Toggle shop Open/Closed status.

## 4. Functional Requirements

### 4.1 Discovery & Search
- **FR1**: The system shall use the customer's geolocation to show vendors within a specified radius.
- **FR2**: Users shall be able to adjust search distance using a slider.

### 4.2 Ordering System
- **FR3**: The system shall generate sequential order numbers for easy tracking.
- **FR4**: Real-time status updates shall be visible to customers without page refreshes (via polling).

### 4.3 Payment & Wallet
- **FR5**: The platform shall maintain a digital wallet for each customer.
- **FR6**: The system shall support split payments (Partial Wallet + Cash).
- **FR7**: Top-ups ≥ ₹100 shall receive a ₹10 bonus.

### 4.4 Security
- **FR8**: Every order must be secured with a unique 4-digit OTP for pickup.
- **FR9**: Phone number validation (10-digit) is required for registration/ordering.

## 5. Non-Functional Requirements
- **Performance**: Order status polling should occur every 10 seconds for customers.
- **Scalability**: Backend should handle multiple concurrent order updates.
- **Usability**: Mobile-first responsive design for on-the-go usage.
- **Reliability**: Persistence of cart and session data using browser localStorage.

