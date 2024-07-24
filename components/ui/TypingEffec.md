---
  title: 'TypingEffec.tsx'
  description: 'component description'
  pubDate: 'July 24, 2024'
  author: 'Carlos P'
  ---
  
  
  
  # TypingEffec.tsx
  # TypingEffect Component

The `TypingEffect` component is a React functional component that simulates a typing effect for a given text. It progressively displays the text character by character at a specified speed, creating an animated typing effect. The component also includes a cursor element that scrolls into view when it is not visible on the screen.

### React Hooks Used
1. **useState**: Used to manage the state of `index` and `currentText` within the component.
2. **useEffect**: Used to perform side effects in the component. Two `useEffect` hooks are used in this component.
3. **useRef**: Used to create references to the cursor element and an IntersectionObserver instance.

### Helper Functions and Operations
1. **IntersectionObserver**: An observer is set up to ensure that the cursor element is always visible on the screen. If the cursor is not visible, it is scrolled into view.
2. **setLoading**: A function obtained from the `useMessagesData` context to set the loading state.

### Props
- **text (string)**: The text that will be displayed with the typing effect. Default value is an empty string.
- **speed (number)**: The speed at which the text is typed out. Default value is 1.

### External Dependencies
- **useMessagesData**: A custom hook imported from `"../Context/MessageDataContext"` that provides access to the loading state.

### Component Usage
1. The `TypingEffect` component takes in the `text` and `speed` props to determine the text content and typing speed.
2. It progressively displays the text character by character at the specified speed.
3. The cursor element is included in the output to simulate a typing effect.
4. Once the typing is complete, the observer is disconnected, and the loading state is set to false.

Overall, the `TypingEffect` component provides a visually appealing way to display text content with a typing animation effect.
  
  ## Component Code
  ```jsx
  import React, { useState, useEffect, useRef } from "react";
import { useMessagesData } from "../Context/MessageDataContext";

const TypingEffect = ({ text = "", speed = 1 }) => {
  const [index, setIndex] = useState(0);
  const [currentText, setCurrentText] = useState("");
  const cursorRef = useRef<HTMLSpanElement | null>(null); // Ref for the cursor to track its visibility
  const observerRef = useRef<IntersectionObserver | null>(null); // Ref to store the observer
  const { setLoading } = useMessagesData();

  useEffect(() => {
    // Setup IntersectionObserver to ensure the cursor is always visible
    observerRef.current = new IntersectionObserver(
      (entries) => {
        if (entries[0] && !entries[0].isIntersecting) {
          // If the cursor is not visible, scroll it into view
          if (cursorRef.current) {
            cursorRef.current.scrollIntoView({
              behavior: "smooth",
              block: "end",
            });
          }
        }
      },
      {
        root: null, // Default viewport as the scroll container
        threshold: 0.1, // At least 10% of the item is visible
      }
    );

    if (cursorRef.current) {
      observerRef.current.observe(cursorRef.current);
    }

    // Clean up the observer to avoid memory leaks
    return () => {
      if (observerRef.current && cursorRef.current) {
        // eslint-disable-next-line react-hooks/exhaustive-deps
        observerRef.current.unobserve(cursorRef.current);
      }
    };
  }, []); // Ensures this effect runs only once on mount

  useEffect(() => {
    if (index < text.length) {
      const timer = setTimeout(() => {
        setCurrentText((prev) => prev + text[index]);
        setIndex((prev) => prev + 1);
      }, speed);
      return () => clearTimeout(timer);
    } else {
      // After finishing typing, disconnect the observer and set loading to false
      if (observerRef.current && cursorRef.current) {
        observerRef.current.unobserve(cursorRef.current);
      }
      setLoading(false); // Notify that typing has finished
    }
  }, [index, text, speed, setLoading]);

  const lines = currentText.split("\n").map((line, idx) => (
    <div key={idx} style={{ marginBottom: "1em" }}>
      {line}
    </div>
  ));

  return (
    <p>
      {lines}
      <span ref={cursorRef} className="cursor"></span>
    </p>
  );
};

export default TypingEffect;
  ```
  