---
  title: 'Input.tsx'
  description: 'component description'
  pubDate: 'July 23, 2024'
  author: 'Carlos P'
  ---
  
  
  
  # Input.tsx
  # Input Component

The `Input` component is a functional component in React that serves as a user interface for sending messages. It includes various input fields and buttons for sending text messages, attaching files, and toggling between text and voice modes.

## React Hooks Used
1. **useRef**: The `inputRef` is created using the `useRef` hook to reference the input element for focusing on it when a specific key combination is pressed.
   
2. **useEffect**: The `useEffect` hook is used to add and remove an event listener for a key combination (`ctrl/cmd + s`) to focus on the input field.

3. **useState**: The `useState` hook is used to manage the state of the message content and the file being attached.

## Helper Functions
1. **handleSubmit**: This function is triggered when the form is submitted. It prevents the default form submission behavior, checks if the app is in a loading state, sends the message along with any attached file, and clears the file input after sending the message.

2. **handleInputKeyDown**: This function is called when a key is pressed in the input field. It prevents the default behavior for the Enter key, checks if the app is in a loading state, and calls the `handleSubmit` function.

3. **handleFileChange**: This function is triggered when a file is selected using the file input field. It updates the state with the selected file.

4. **handleFileRemove**: This function clears the selected file.

## External Dependencies
1. **Heroicons React**: Icons like `PaperAirplaneIcon` and `PaperClipIcon` are imported from the Heroicons React library to display icons for sending messages and attaching files.

2. **ToggleSwitch Component**: The `ModeToggle` component is used to toggle between text and voice modes.

3. **AudioRecorder Component**: The `AudioRecorder` component is used to handle audio recording functionality.

4. **FilePreview Component**: The `FilePreview` component is used to display a preview of the attached file and provide an option to remove it.

## Props
- **placeholder**: A string prop that specifies the placeholder text for the input field. It defaults to "Type your message" if not provided.

Overall, the `Input` component provides a user-friendly interface for sending messages, attaching files, and toggling between different modes, enhancing the user experience within the messaging feature of the application.
  
  ## Component Code
  ```jsx
  import React, { useRef, useEffect, useState } from "react";
import { PaperAirplaneIcon, PaperClipIcon } from "@heroicons/react/24/outline";
import { useMessagesData } from "../Context/MessageDataContext";
import useMessageSender from "../Hooks/useMessageSender";
import ModeToggle from "./ToggleSwitch";
import { useTextOrVoice } from "../Context/TextOrVoiceContext";
import AudioRecorder from "./AudioRecorder";
import FilePreview from "./FilePreview";

export default function Input({ placeholder = "Type your message" }) {
  const { mode } = useTextOrVoice();
  const { message, setMessage, sendMessage, file, setFile } = useMessageSender(
    mode.apiUrl
  );
  const { isLoading } = useMessagesData();
  const inputRef = useRef<HTMLInputElement | null>(null);

  useEffect(() => {
    const handleKeyDown = (event: KeyboardEvent) => {
      if ((event.ctrlKey || event.metaKey) && event.key === "s") {
        event.preventDefault();
        if (inputRef.current) {
          inputRef.current.focus();
        }
      }
    };

    document.addEventListener("keydown", handleKeyDown);

    return () => {
      document.removeEventListener("keydown", handleKeyDown);
    };
  }, []);

  const handleSubmit = async (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    if (isLoading) return;

    await sendMessage(message, file ?? undefined);
    setFile(null); // Clear the file input after sending the message
  };

  const handleInputKeyDown = (event: React.KeyboardEvent<HTMLInputElement>) => {
    if (event.key === "Enter") {
      event.preventDefault();
      if (isLoading) return;
      handleSubmit(event as any);
    }
  };

  const handleFileChange = (event: React.ChangeEvent<HTMLInputElement>) => {
    if (event.target.files && event.target.files[0]) {
      setFile(event.target.files[0]);
    }
  };

  const handleFileRemove = () => {
    setFile(null);
  };

  return (
    <>
      <form
        className="flex gap-4 bg-base-100 border flex-wrap w-full sm:w-[70%] py-2 px-2 rounded-2xl items-center border border-primary/10 shadow-xl"
        onSubmit={handleSubmit}
      >
        {file && (
          <div className="w-full flex">
            <FilePreview file={file} onRemove={handleFileRemove} />{" "}
          </div>
        )}

        <div>
          <label className="flex items-center cursor-pointer">
            <PaperClipIcon className="w-6 text-base-content/60" />
            <input
              type="file"
              className="hidden"
              onChange={handleFileChange}
              disabled={isLoading}
            />
          </label>
        </div>
        <input
          ref={inputRef}
          className="flex flex-1 input min-w-8 ring-0 focus:ring-0 focus:outline-none"
          placeholder={placeholder}
          value={message}
          onChange={(e) => setMessage(e.target.value)}
          onKeyDown={handleInputKeyDown}
          disabled={isLoading}
        />
        <div className="flex gap-3 items-center">
          <AudioRecorder />
          <button type="submit" disabled={isLoading}>
            <PaperAirplaneIcon className="w-6 text-base-content/60" />
          </button>
        </div>
      </form>

      <div className="flex w-[70%] justify-between">
        <div className="hidden sm:block py-2 px-4">
          <kbd className="kbd kbd-xs">ctrl</kbd>+
          <kbd className="kbd kbd-xs">s</kbd>{" "}
          <span className="text-xs text-base-content/70"> Start Searching</span>
        </div>
        <ModeToggle />
      </div>
    </>
  );
}
  ```
  