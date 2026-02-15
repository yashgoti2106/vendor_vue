# Technical Design - VendorVue

## 1. System Architecture
VendorVue follows a standard MERN-like architecture (Node/Express/MongoDB) with a React frontend.

### 1.1 Architecture Components
- **Frontend**: React 18 + Vite, Tailwind CSS for styling, Leaflet for maps.
- **Backend**: Node.js + Express.js REST API.
- **Database**: MongoDB (NoSQL) for flexible schema handling.
- **Communication**: REST API using Axios with polling-based real-time updates.

## 2. Data Models (Mongoose Schemas)

### 2.1 Vendor
- `name`: String
- `phone`: String (Unique)
- `category`: String
- `location`: { `lat`: Number, `lng`: Number, `address`: String }
- `isOpen`: Boolean
- `rating`: Number
- `totalOrders`: Number

### 2.2 MenuItem
- `vendorId`: ObjectId (Ref: Vendor)
- `name`: String
- `description`: String
- `price`: Number
- `category`: String
- `inStock`: Boolean
- `preparationTime`: Number

### 2.3 Order
- `orderNumber`: Number (Auto-incrementing)
- `vendorId`: ObjectId (Ref: Vendor)
- `customerName`: String
- `customerPhone`: String
- `items`: Array of { `name`, `price`, `quantity` }
- `total`: Number
- `paymentMethod`: Enum ('wallet', 'cash', 'split')
- `walletAmount`: Number
- `cashAmount`: Number
- `otp`: String (4-digit)
- `status`: Enum ('pending', 'preparing', 'ready', 'completed')

### 2.4 Customer/Wallet
- `phone`: String (Unique ID)
- `name`: String
- `walletBalance`: Number
- `transactions`: Array of { `type`, `amount`, `date`, `description` }

## 3. Key Logic Implementations

### 3.1 Distance Calculation
The system calculates distance between the customer (browser geolocation) and vendor coordinates using the Haversine formula:
```javascript
d = 2R * asin(sqrt(sin²(Δlat/2) + cos(lat1).cos(lat2).sin²(Δlon/2)))
```

### 3.2 Order Sequencing
Orders are assigned a per-vendor or global sequential number (e.g., #1, #2) to simplify the pickup process for street vendors who may not use complex POS systems.

### 3.3 Security Flow (OTP)
1. Order created → Server generates a random 4-digit OTP.
2. Order marked 'Ready' → Customer notified via UI.
3. Pickup → Customer shows OTP; Vendor enters it in the system.
4. Server validates OTP → Order status set to 'Completed'.

## 4. API Structure
- **/api/vendors**: Discovery and registration.
- **/api/menu**: Menu item CRUD operations.
- **/api/orders**: Lifecycle management and OTP verification.
- **/api/customers**: Wallet and order history.

## 5. UI/UX Principles
- **Mobile-First**: Designed primarily for handheld devices.
- **Minimalistic**: High contrast, large buttons for outdoor visibility.
- **Feedback**: Immediate visual/audio feedback for order status changes.
