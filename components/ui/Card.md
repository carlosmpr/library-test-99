---
  title: 'Card.tsx'
  description: 'component description'
  pubDate: 'July 23, 2024'
  author: 'Carlos P'
  ---
  
  
  
  # Card.tsx
  # Card Component

The `Card` component is a functional React component that represents a card UI element. It takes in three props: `title`, `description`, and `onclick`.

### Props

- `title`: A string representing the title of the card.
- `description`: A string representing the description or content of the card.
- `onclick`: A function that is called when the card is clicked. It does not take any arguments and returns `void`.

### Component Structure

The `Card` component returns a `div` element representing the card. It has the following structure:

1. The outer `div` element has a set of CSS classes defining its appearance, such as width, padding, shadow, cursor style, and rounded corners. It also includes a `onClick` event listener that triggers the `onclick` function passed as a prop.
   
2. Inside the outer `div`, there is a `div` element with CSS classes for flexbox layout, aligning items, and setting the gap between them.
   
3. Within this inner `div`, there is an `h3` element displaying the `title` prop. The `title` is styled with a specific font weight and text size.
   
4. Following the `h3` element, there is a `p` element displaying the `description` prop. The `description` text is styled with a smaller font size and a different color for content/70.

### Dependencies

- The component uses React for building the UI and managing component state.
- It relies on Tailwind CSS classes for styling the card elements, providing a responsive and visually appealing design.

This component serves as a reusable card element that can be used to display information in a structured and visually appealing manner. When a user clicks on the card, the `onclick` function is triggered, allowing for custom actions or behaviors to be implemented in the parent component.
  
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
  