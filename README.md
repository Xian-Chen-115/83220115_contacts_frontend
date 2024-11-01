# 83220115_contacts_frontend

---

# Contact Management System

This project is a Vue 3 application that uses Element Plus and Axios to create a contacts management system with pagination, add/edit dialogs, and search functionality.

## Features

- **User Management**: Add, edit, delete, and search contacts.
- **Pagination**: Paginated contacts data display.
- **Responsive UI**: Built with Element Plus components for a consistent and responsive UI.
- **Axios Interceptors**: Request and response interceptors handle API requests and responses efficiently.

## Tech Stack

- **Vue 3**: Front-end framework for building the application.
- **Element Plus**: UI component library for Vue 3.
- **Axios**: Library for HTTP requests with request/response interceptors.
- **SCSS**: Styling with global styles applied from `global.css`.

## Setup Instructions

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/your-repository.git
   cd your-repository
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Environment Variables**:
   - Copy the `.env.example` file to `.env`.
   - Set `VUE_APP_BASEURL` to the base URL of your API backend.
   - Example:
     ```env
     VUE_APP_BASEURL=https://api.example.com
     ```

4. **Run the application**:
   ```bash
   npm run serve
   ```

5. **Build for production**:
   ```bash
   npm run build
   ```

## Project Structure

```plaintext
├── src
│   ├── assets
│   │   └── css
│   │       └── global.css       # Global styles
│   ├── components               # Vue components
│   ├── router                   # Vue Router setup
│   ├── store                    # Vuex store setup
│   ├── utils
│   │   └── request.js           # Axios setup and interceptors
│   ├── views
│   │   └── HomeView.js
│   ├── App.vue
│   ├── main.js                  # Main entry file            
├── public
└── package.json                 # Dependencies and scripts
```

## Key Code Components

- **Data Fetching and Pagination**: Fetches user data with pagination and search options.
- **Dialog Forms**: Supports add and edit operations through modal dialogs.
- **Axios Setup**: `request.js` handles API requests with interceptors for error handling and customization.

### Axios Interceptor Configuration

- `request.js` sets a JSON content type in headers and provides response handling.
- Example:
  ```javascript
  request.interceptors.request.use(config => {
      config.headers['Content-Type'] = 'application/json;charset=utf-8';
      return config;
  });
  ```

## Usage

- **Search Users**: Enter a name in the search box and click the "Search" button.
- **Add User**: Click the "+" button to open the add user dialog.
- **Edit User**: Click the "Edit" button in the user row to update user information.
- **Delete User**: Click the "Delete" button in the user row and confirm to delete a user.

---

This setup should get you running the application smoothly. Adjust as needed based on your backend specifics.
