Certainly! Using hooks in a Preact app simplifies managing state and side effects. Here’s how you can implement a theme switcher using Preact's hooks, such as `useState` and `useEffect`.

### 1. Define Your CSS for Light and Dark Modes

First, make sure you have the CSS for light and dark modes. You’ll need these styles in your `index.css` or a similar stylesheet:

```css
/* index.css */
body.light-mode {
  background-color: #ffffff;
  color: #000000;
}

body.dark-mode {
  background-color: #000000;
  color: #ffffff;
}

/* Add any additional styling for light and dark modes here */
```

### 2. Create the Theme Switcher Component Using Hooks

Here’s a functional component in Preact that uses hooks to manage theme switching:

```jsx
import { h } from 'preact';
import { useState, useEffect } from 'preact/hooks';

const ThemeSwitcher = () => {
  // Initialize state from localStorage or default to light mode
  const [isDarkMode, setIsDarkMode] = useState(() => {
    const savedMode = localStorage.getItem('themeMode');
    return savedMode === 'dark';
  });

  // Update body class when `isDarkMode` changes
  useEffect(() => {
    const mode = isDarkMode ? 'dark' : 'light';
    document.body.className = `${mode}-mode`;
    localStorage.setItem('themeMode', mode);
  }, [isDarkMode]);

  // Toggle theme mode
  const toggleMode = () => {
    setIsDarkMode(prevMode => !prevMode);
  };

  return (
    <button onClick={toggleMode}>
      Switch to {isDarkMode ? 'Light' : 'Dark'} Mode
    </button>
  );
};

export default ThemeSwitcher;
```

### 3. Use the Theme Switcher in Your App

Include the `ThemeSwitcher` component in your main application component or wherever appropriate:

```jsx
import { h } from 'preact';
import ThemeSwitcher from './ThemeSwitcher';

const App = () => (
  <div>
    <h1>Hello Preact!</h1>
    <ThemeSwitcher />
    {/* Other components */}
  </div>
);

export default App;
```

### 4. Run and Test

Run your Preact app to test the theme switcher. Make sure that switching themes updates the `localStorage` and the body class, which persists the user's theme preference across page reloads.

### Summary

In this implementation:
- **`useState`** is used to manage the `isDarkMode` state.
- **`useEffect`** is used to apply the theme to the body class and to store the preference in `localStorage` whenever `isDarkMode` changes.
- The `toggleMode` function updates the state to switch between dark and light modes.

This approach leverages hooks for a clean and modern way to handle theme toggling in your Preact application.
