# Frontend Directory

This folder contains the frontend application for SingleWallet.

## 🎨 Structure Overview

```
frontend/
├── src/
│   ├── components/      # Reusable UI components
│   ├── pages/          # Full-page components (routes)
│   ├── services/       # API communication layer
│   └── utils/          # Helper functions
├── public/             # Static assets
└── README.md
```

## 🚀 Getting Started

### Option 1: React (Recommended for beginners)
```bash
cd frontend
npx create-react-app .
npm install axios
```

### Option 2: Vue.js
```bash
cd frontend
npm init vue@latest
```

### Option 3: Angular
```bash
cd frontend
ng new . --routing --style=css
```

## 📂 Folder Details

### `src/components/`
Reusable UI components that can be used across multiple pages.

Example structure:
```
components/
├── WalletCard/
│   ├── WalletCard.jsx
│   ├── WalletCard.css
│   └── WalletCard.test.js
├── TransactionList/
├── Button/
└── Header/
```

### `src/pages/`
Full-page components representing different routes.

Example structure:
```
pages/
├── Dashboard/
│   ├── Dashboard.jsx
│   └── Dashboard.css
├── WalletDetails/
├── Settings/
└── Login/
```

### `src/services/`
API communication services - handles all backend requests.

Example `walletService.js`:
```javascript
import axios from 'axios';

const API_URL = 'http://localhost:8080/api';

export const walletService = {
    getAllWallets: () => axios.get(`${API_URL}/wallets`),
    getWalletById: (id) => axios.get(`${API_URL}/wallets/${id}`),
    createWallet: (wallet) => axios.post(`${API_URL}/wallets`, wallet),
    updateWallet: (id, wallet) => axios.put(`${API_URL}/wallets/${id}`, wallet),
    deleteWallet: (id) => axios.delete(`${API_URL}/wallets/${id}`)
};
```

### `src/utils/`
Helper functions and utilities.

Examples:
- `formatCurrency.js` - Format money values
- `dateHelpers.js` - Date formatting functions
- `validators.js` - Form validation helpers

## 🔗 Connecting to Backend

1. **Install Axios** (or use Fetch API):
   ```bash
   npm install axios
   ```

2. **Create API service** in `src/services/api.js`:
   ```javascript
   import axios from 'axios';
   
   const api = axios.create({
       baseURL: 'http://localhost:8080/api'
   });
   
   export default api;
   ```

3. **Use in components**:
   ```jsx
   import { walletService } from '../services/walletService';
   
   const fetchWallets = async () => {
       const response = await walletService.getAllWallets();
       setWallets(response.data);
   };
   ```

## 🎯 Team Workflow

### Member 3: Components & UI
- Build reusable components
- Style the application
- Ensure responsive design

### Member 4: Pages & Integration
- Create page layouts
- Connect components
- Integrate with backend APIs
- Handle routing

## 📋 Best Practices

- **Component naming**: Use PascalCase (e.g., `WalletCard.jsx`)
- **File organization**: Keep related files together
- **State management**: Consider Redux/Zustand for complex state
- **Error handling**: Always handle API errors
- **Loading states**: Show loading indicators
- **Environment variables**: Use `.env` for API URLs

## 🛠️ Development Commands

```bash
npm start          # Start development server
npm test           # Run tests
npm run build      # Build for production
npm run lint       # Check code quality
```

## 📦 Recommended Packages

```bash
npm install axios                 # HTTP client
npm install react-router-dom      # Routing (React)
npm install @mui/material         # Material-UI components
npm install formik yup            # Form handling
npm install date-fns              # Date utilities
npm install chart.js react-chartjs-2  # Charts
```
