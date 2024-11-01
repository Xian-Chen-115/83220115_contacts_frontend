


Here's a `CODESTYLE.md` based on general practices for Vue and JavaScript development, inspired by the content in the Alibaba article:

---
https://developer.aliyun.com/article/850913

# Code Style Guide

This document outlines the coding conventions and best practices for this Vue project. Consistent code style helps improve readability, maintainability, and team collaboration.

## 1. Directory and File Naming Conventions

- **Directory Names**: Use all lowercase letters, and separate words with hyphens (e.g., `user-management`).
- **Component Files**: Component file names should use `PascalCase` to indicate they export a Vue component (e.g., `HomeView.vue`).
- **Other Files**: Use `camelCase` for JavaScript and utility files (e.g., `request.js`).

## 2. Component Structure

Each Vue component should follow this structure in order:

1. **Imports**: Import dependencies and components at the top.
2. **Component Setup**: Use `<script setup>` for composition API.
3. **Template**: Use the `<template>` section to define UI markup.
4. **Styles**: Scoped styles should be at the bottom of each component file.

## 3. Naming Conventions

- **Variables and Functions**: Use `camelCase` for naming variables, functions, and instance properties.
- **Components**: Use `PascalCase` for naming Vue components.
- **Constants**: Use uppercase with underscores, like `BASE_URL`.
- **Props and Events**: Use `camelCase` in JavaScript, and `kebab-case` in templates (e.g., `<MyComponent :user-name="userName" />`).

## 4. Template Structure

- **Attributes Order**: Arrange attributes in a consistent order: `directives`, `props`, `events`, and `standard attributes` (e.g., `class` and `style`).
- **Event Modifiers**: Use event modifiers instead of methods where possible (e.g., `@click.prevent`).

### Example:
```html
<el-button
  class="primary-button"
  type="primary"
  size="small"
  @click.prevent="handleClick"
>
  Button
</el-button>
```

## 5. Script Code Style

- **Variable Declaration**: Use `const` for constants, `let` for variables that change.
- **Arrow Functions**: Prefer arrow functions for anonymous functions.
- **Comments**: Use `//` for single-line comments and `/** */` for multi-line documentation.
- **API Requests**: Use `async`/`await` syntax for asynchronous code, and handle errors using `try/catch`.

### Example:
```javascript
const fetchData = async () => {
  try {
    const response = await request.get('/user/selectByPage', { params });
    data.value.arr = response.data.list;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};
```

## 6. CSS and SCSS Guidelines

- **BEM Naming**: Use the BEM (Block, Element, Modifier) naming convention for classes.
- **Scoped Styles**: Each component should use scoped CSS to avoid conflicts.
- **Global Styles**: Place global styles in the `global.css` file within the `assets/css` directory.

### Example:
```css
.primary-button {
  /* block */
}

.primary-button--small {
  /* modifier */
}

.primary-button__icon {
  /* element */
}
```

## 7. API Requests with Axios

- **Base URL**: Use `VUE_APP_BASEURL` for the API base URL.
- **Interceptors**: Configure Axios interceptors in `request.js` to set headers and handle responses globally.
- **Error Handling**: Log errors in the console and ensure any async function has error handling.

### Example:
```javascript
request.interceptors.request.use(config => {
  config.headers['Content-Type'] = 'application/json;charset=utf-8';
  return config;
}, error => {
  return Promise.reject(error);
});
```

## 8. ESLint Rules

- **Spaces**: Use 2 spaces for indentation.
- **Quotes**: Use single quotes for JavaScript strings.
- **Semicolons**: Always use semicolons.
- **Line Length**: Limit lines to 80 characters where possible.

Ensure that ESLint and Prettier configurations are set to follow these conventions for automated linting and formatting.

---

This `CODESTYLE.md` should keep the codebase clean, consistent, and easy for team members to read and maintain. Adjust any rule as needed based on team feedback or specific project requirements.