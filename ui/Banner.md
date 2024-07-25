---
  title: 'Banner.tsx'
  description: 'component description'
  pubDate: 'July 25, 2024'
  author: 'Carlos P'
  ---
  
  
  
  # Banner.tsx
  # Banner Component

The `Banner` component is a functional component in React that displays a banner with an image, a greeting message, and a description text. Let's break down the key aspects of this component:

### External Dependencies
- **Next.js Image Component**: The component imports the `Image` component from Next.js, which is used to optimize and serve images with the best performance.

### Component Structure
- The component is a `div` element with flexbox properties to center its contents vertically and horizontally.
- It consists of an image, a greeting message, and a description text.

### Image Component
- The `Image` component from Next.js is used to display an optimized image.
  - `src`: Specifies the path to the image file.
  - `alt`: Provides alternative text for the image.
  - `className`: Applies styling to the image, setting a width of 80px, a background color of primary, and a rounded border.
  - `width` and `height`: Define the size of the image for large desktop screens, maintaining a 1:1 aspect ratio.
  - `quality`: Sets the general quality of the image to 75.
  - `loading`: Specifies the loading strategy for the image as eager.
  - `priority`: Indicates that the image is considered high priority and should be loaded immediately.

### Greeting Message and Description
- The component includes a greeting message "Hola, Jhon Doe" with styling for different font sizes and weights.
- A description text follows the greeting message, providing placeholder content.

### Conclusion
The `Banner` component is a simple banner display with an optimized image, a greeting message, and a description. It leverages the Next.js `Image` component for efficient image loading and performance optimization. The component's structure and styling focus on centering the content and providing a visually appealing banner section.
  
  ## Component Code
  ```jsx
  import Image from "next/image";

export default function Banner() {
  return (
    <div className="flex flex-col gap-2 items-center justify-center text-center ">
      
      <Image
            src={"/logo.svg"}
            alt={"/logo.svg"}
           
            className="w-[80px] bg-primary rounded-xl"
            width={1800} // Define the size of the image for large desktop screens
            height={1800} // This maintains a 1:1 aspect ratio, adjust as necessary
            quality={75} // General quality setting, can adjust lower or higher based on testing
            loading="eager"
            priority
           
          />
      <h1 className="text-4xl sm:text-7xl font-light ">
        Hola,{" "}
        <span className="font-bold text-primary ">
          Jhon Doe
        </span>
      </h1>
      <p className="text-base-content/80 max-w-[500px]">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
        tempor incididunt ut labore et dolore magna aliqua.
      </p>
    </div>
  );
}
  ```
  