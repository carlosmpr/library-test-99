---
  title: 'Card.tsx'
  description: 'component description'
  pubDate: 'July 25, 2024'
  author: 'Carlos P'
  ---
  
  
  
  # Card.tsx
  # Card Component

The `Card` component is a functional React component that represents a card UI element. It takes in three props: `title`, `description`, and `onclick`.

### Props

- `title`: A string representing the title of the card.
- `description`: A string representing the description or content of the card.
- `onclick`: A function that is called when the card is clicked. It does not take any arguments and returns void.

### Component Structure

The `Card` component returns a `div` element that represents the card. It has the following structure:

1. The outer `div` element has a set of CSS classes that define its appearance, such as width, padding, shadow, cursor style, and rounded corners. It also has a `onClick` event listener that triggers the `onclick` function passed as a prop.
   
2. Inside the outer `div`, there is a `div` element with the class `flex items-center gap-2`, which aligns its children horizontally with a gap between them.
   
3. Within this inner `div`, there is an `h3` element displaying the `title` prop. The `h3` element has a class that defines its font weight and text size.
   
4. Following the `h3` element, there is a `p` element displaying the `description` prop. The `p` element has a class that defines its text size and color.

### Dependencies

- The component does not rely on any external libraries or dependencies for its functionality.

### Usage

To use the `Card` component in a React application, import it and pass the required props (`title`, `description`, and `onclick`). When the card is clicked, the `onclick` function will be executed. The component provides a simple and reusable way to display card elements with customizable content and click functionality.
  
  ## Component Code
  ```jsx
  import React from "react";

export interface CardProps {
  title: string;
  description: string;
  onclick: () => void;
}

const Card: React.FC<CardProps> = ({ title, description, onclick }) => {
  return (
    <div
      className="min-w-[200px] p-4 sm:w-[280px] shadow-xl  cursor-pointer text-start grid glass p-4 rounded-2xl"
      onClick={onclick}
    >
      <div className="flex items-center gap-2">
        <h3 className="font-semibold text-base-content-100">{title}</h3>
      </div>
      <p className="text-sm text-base-content/70">{description}</p>
    </div>
  );
};

export default Card;
  ```
  