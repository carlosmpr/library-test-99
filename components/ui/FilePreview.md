---
  title: 'FilePreview.tsx'
  description: 'component description'
  pubDate: 'July 24, 2024'
  author: 'Carlos P'
  ---
  
  
  
  # FilePreview.tsx
  # FilePreview Component

The `FilePreview` component is a React functional component that displays a preview of a file. It conditionally renders either an image preview or a file icon with the file name based on the type of file provided. It also includes a "Remove" button that triggers the `onRemove` function when clicked.

## React Hooks Used
- No React hooks are used in this component.

## Helper Functions
- No explicit helper functions are defined in this component.

## Usage
The `FilePreview` component takes two props:
1. `file`: A `File` object or `null`. It represents the file to be previewed. If `file` is `null`, the component returns `null` and does not render anything.
2. `onRemove`: A function that is called when the "Remove" button is clicked. It is used to handle the removal of the file.

The component checks if the `file` prop is not `null`. If it is not `null`, it determines whether the file is an image based on its type. If the file is an image, it displays the image using the `next/image` component with the file's URL created using `URL.createObjectURL`. If the file is not an image, it displays a file icon along with the file name.

## External Libraries/Dependencies
- `next/image`: This library is used to display images efficiently in Next.js applications. It provides optimizations for image loading and rendering.

Overall, the `FilePreview` component is a simple component that provides a visual preview of a file, either as an image or with a file icon and name, along with a "Remove" button for user interaction.
  
  ## Component Code
  ```jsx
  'use client'
import React from "react";
import Image from "next/image";

interface FilePreviewProps {
  file: File | null;
  onRemove: () => void;
}

const FilePreview: React.FC<FilePreviewProps> = ({ file, onRemove }) => {
  if (!file) return null;

  const isImage = file.type.startsWith("image/");

  return (
    <div className="flex items-center gap-2 p-2 border rounded-lg bg-gray-100">
      {isImage ? (
        <Image
          src={URL.createObjectURL(file)}
          alt={file.name}
          width={500}
          height={500}
          className="h-16 w-16 object-cover rounded-lg"
        />
      ) : (
        <div className="flex items-center gap-2">
          <span className="icon-doc"></span>
          <span>{file.name}</span>
        </div>
      )}
      <button onClick={onRemove} className="text-red-600">
        Remove
      </button>
    </div>
  );
};

export default FilePreview;
  ```
  