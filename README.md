# AI-Workshop

Section 1: (Frontend)

Step 1: Creating folder structure
ai-study-buddy/
└── frontend/
    ├── public/
    └── src/
        ├── App.js
        ├── components/
        │   └── ChatBox.js
        ├── index.js
        └── App.css

Step 2: Code Flow

Step 3: Add code to Files

frontend/src/public/index.html:

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <title>AI Study Buddy</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>


frontend/src/index.js:

import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./App.css";
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);


frontend/src/App.js:

import React, { useState } from "react";
import ChatBox from "./components/ChatBox_old";
import "./App.css";
function App() {
  return (
    <div className="App">
      //<h1>🎓 AI Study Buddy</h1>
      <ChatBox />
    </div>
  );
}
export default App;


frontend/src/components/ChatBox.js:

import React, { useState } from "react";
const ChatBox = () => {
  const [prompt, setPrompt] = useState("");
  const [response, setResponse] = useState("");
  const [loading, setLoading] = useState(false);
  const handleAsk = async () => {
    setLoading(true);
    setResponse("");
    try {
      const res = await fetch("http://localhost:5000/ask", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ prompt }),
      });
      const data = await res.json();
      if (data.response) {
        setResponse(data.response);
      } else {
        setResponse("Error: " + data.error);
      }
    } catch (err) {
      setResponse("Error connecting to server.");
    }
    setLoading(false);
  };
  return (
    <div className="chatbox">
      <textarea
        placeholder="Ask a question or paste your notes..."
        value={prompt}
        onChange={(e) => setPrompt(e.target.value)}
      />
      <button onClick={handleAsk} disabled={loading}>
        {loading ? "Asking..." : "Submit"}
      </button>
      <div className="response">
        <strong>Response:</strong>
        <p>{response}</p>
      </div>
    </div>
  );
};
export default ChatBox;


frontend/src/App.css:
.App {
  font-family: Arial, sans-serif;
  padding: 2rem;
  max-width: 700px;
  margin: auto;
  text-align: center;
}
.chatbox textarea {
  width: 100%;
  height: 100px;
  margin-bottom: 1rem;
  padding: 1rem;
  font-size: 1rem;
}
.chatbox button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  margin-bottom: 1rem;
}
.response {
  background: #f9f9f9;
  padding: 1rem;
  border-radius: 8px;
  text-align: left;
}


frontend/.gitignore:

# dependencies
/node_modules
/.pnp
.pnp.js

# testing
/coverage

# production
/build

# misc
.DS_Store
.env
.env.local
.env.development.local
.env.test.local
.env.production.local

# logs
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# IDE
.vscode/
.idea/
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?

# Mac system files
*.DS_Store



Execution Steps:

cd frontend
npm install
npm start






