path: src/context/store.tsx

```javascript
'use client';
import { createContext, useContext, Dispatch, SetStateAction, useState } from "react"

// Define the shape of the context
interface CONTEXT_PROPS {
    githubUrls: string[],
    setGithubUrls: Dispatch<SetStateAction<string[]>>,
    userId: string,
    setUserId: Dispatch<SetStateAction<string>>,
}

// Create the GlobalContext with initial values and empty functions
const GlobalContext = createContext<CONTEXT_PROPS>({
    githubUrls: [],
    setGithubUrls: () => {},
    userId: "",
    setUserId: () => {},
})

// Provider component that sets up the context provider with state management
export const GlobalContextProvide = ({ children }: { children: React.ReactNode }) => {
    // Initialize state for userId and githubUrls
    const [userId, setUserId] = useState("");
    const [githubUrls, setGithubUrls] = useState<string[]>([]);

    return (
        // Provide the state and functions to the context
        <GlobalContext.Provider value={{ userId, setUserId, githubUrls, setGithubUrls }}>
            {children}
        </GlobalContext.Provider>
    )
}

// Custom hook to access the GlobalContext values
export const useGlobalContext = () => useContext(GlobalContext);
```
