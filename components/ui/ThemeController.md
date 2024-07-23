---
  title: 'ThemeController.tsx'
  description: 'component description'
  pubDate: 'July 23, 2024'
  author: 'Carlos P'
  ---
  
  
  
  # ThemeController.tsx
  # ThemeController Component

The `ThemeController` component is a React functional component that renders a dropdown menu to select a theme from a predefined list of themes. It displays a label "Select Theme" and a list of radio buttons, each representing a theme option.

### React Hooks Used
- No React hooks are used in this component.

### Helper Function
- `handleClick`: This function is a click event handler that stops the propagation of the click event. It takes an event object as a parameter and calls `stopPropagation()` on it to prevent the event from bubbling up the DOM tree.

### Component Usage
- The component renders a dropdown menu with a label and a list of theme options represented by radio buttons.
- Clicking on the dropdown menu does not trigger any action due to the `handleClick` function that stops the event propagation.
- Each theme option is displayed as a radio button with the theme name capitalized as the aria-label.

### External Libraries or Dependencies
- There are no external libraries or dependencies used in this component.

### TypeScript Typings for Props
- There are no props defined for this component, so no TypeScript typings for props are present.

Overall, the `ThemeController` component provides a simple interface for selecting a theme from a predefined list without any additional functionality or state management.
  
  ## Component Code
  ```jsx
  import React from 'react';

const themes = [
  "light", "dark", "cupcake", "bumblebee", "emerald", "corporate", "synthwave",
  "retro", "cyberpunk", "valentine", "halloween", "garden", "forest", "aqua",
  "lofi", "pastel", "fantasy", "wireframe", "black", "luxury", "dracula", "cmyk",
  "autumn", "business", "acid", "lemonade", "night", "coffee", "winter", "dim",
  "nord", "sunset",
];

const ThemeController = () => {
  // Handler to stop propagation of click events
  const handleClick = (event: { stopPropagation: () => void; }) => {
    event.stopPropagation();
  };

  return (
    <div className="dropdown" onClick={handleClick}>
      <label tabIndex={0} className="btn m-1">Select Theme</label>
      <ul tabIndex={0} className="dropdown-content z-[1] p-2 shadow-2xl bg-base-300 rounded-box w-52 h-52 overflow-y-scroll">
        {themes.map((theme) => (
          <li key={theme}>
            <input
              type="radio"
              name="theme-dropdown"
              className="theme-controller btn btn-sm btn-block btn-ghost justify-start"
              aria-label={theme.charAt(0).toUpperCase() + theme.slice(1)}
              value={theme}
            />
          </li>
        ))}
      </ul>
    </div>
  );
};

export default ThemeController;
  ```
  