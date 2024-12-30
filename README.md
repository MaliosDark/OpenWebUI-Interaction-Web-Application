# **OpenWebUI Interaction Web Application**

---

## **Introduction**

This project serves as a robust web interface for connecting and interacting with an **OpenWebUI** API endpoint. Using this interface, users can send queries and receive AI-generated responses. It features customizable AI configurations, a dynamic UI, and a developer-friendly structure for easy integration and customization.

---

## **Features**

### **User Experience**
1. **Custom AI Configuration**:
   - Adjust **temperature** for response randomness.
   - Define **max tokens** to limit response length.
   - Add an optional **system prompt** to guide the AI.

2. **Interactive Messaging**:
   - Real-time query submission and response display.
   - Clean response extraction for readability.

3. **Smooth Animations**:
   - Animations powered by **AOS (Animate on Scroll)** for an enhanced user experience.

---

### **Developer Features**
1. **Ready-to-Use Fetch Integration**:
   - Plug-and-play connectivity to the OpenWebUI API.
2. **Dynamic Configuration**:
   - Accepts multiple user-defined configurations like temperature, tokens, and custom prompts.
3. **Modular and Extensible**:
   - Easily adaptable for different models, endpoints, and features.
4. **Error Handling**:
   - Built-in validation and error messages for failed API requests.

---

## **Getting Started**

### **Prerequisites**
1. **OpenWebUI Server**:
   - Ensure OpenWebUI is hosted and accessible. Example:
     ```
     https://sofia.aswss.com/api/chat/completions
     ```
2. **API Key**:
   - Obtain your API key and replace the placeholder in the code:
     ```
     Bearer sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
     ```

---

## **Setup and Integration**

### **Steps to Use the Web Application**

1. **Download and Open**:
   - Save the provided HTML file as `index.html`.
   - Open it in a browser that supports modern JavaScript.

2. **Configuration Options**:
   - Use the UI to set:
     - **Temperature**: Controls randomness.
     - **Max Tokens**: Sets response length.
     - **System Prompt**: Provides context for the AI.

3. **Send a Message**:
   - Type your query in the text box and click **Send**.

4. **View Response**:
   - The AI's clean response is displayed in the designated area.

---

### **Integration for Developers**

#### **API Connection Code**

```javascript
async function sendMessage() {
    const userMessage = document.getElementById('userMessage').value;
    const temperature = parseFloat(document.getElementById('temperature').value);
    const maxTokens = parseInt(document.getElementById('maxTokens').value);
    const systemPrompt = document.getElementById('systemPrompt').value;

    try {
        const response = await fetch('https://sofia.aswss.com/api/chat/completions', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': 'Bearer sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
            },
            body: JSON.stringify({
                model: 'llama3.2:latest',
                messages: [
                    { role: 'system', content: systemPrompt },
                    { role: 'user', content: userMessage }
                ],
                temperature: temperature,
                max_tokens: maxTokens
            })
        });

        if (!response.ok) {
            throw new Error(`Error: ${response.status} ${response.statusText}`);
        }

        const data = await response.json();
        const content = data.choices?.[0]?.message?.content || "No content received in the response.";
        console.log(content);
    } catch (error) {
        console.error(`Error communicating with the API: ${error.message}`);
    }
}
```

#### **What This Code Does**
1. **Collect User Inputs**:
   - Reads user-configured temperature, max tokens, system prompt, and query.

2. **API Request**:
   - Sends a `POST` request to the OpenWebUI endpoint with:
     - Model name (`llama3.2:latest`).
     - Configured parameters.
     - API Key for authentication.

3. **Error Handling**:
   - Validates the response and logs any issues.

4. **Response Handling**:
   - Extracts and logs only the `content` field from the AI’s response.

---

### **Customization**

1. **UI Configuration**:
   - Modify the `<style>` section for branding or theme changes.
   - Adjust **AOS animations** in the HTML for custom effects.

2. **API Endpoint**:
   - Replace the endpoint URL to match your server:
     ```
     https://sofia.aswss.com/api/chat/completions
     ```

3. **Supported Models**:
   - Update the `"model"` parameter in the `fetch()` call for different models.

4. **Advanced Features**:
   - Add fields like `top_p` or `frequency_penalty` for additional customization.

---

## **Detailed ReadMe for Developers**

1. **How the Website Works**:
   - Users configure settings via the UI.
   - A `POST` request is sent to OpenWebUI with all inputs.
   - The server responds with a JSON object.
   - The webpage extracts and displays the `content` field.

2. **Error Scenarios**:
   - **API Unreachable**: Displays an error message if the API is down.
   - **Invalid Inputs**: Provides user feedback for out-of-range values.

3. **Extending Functionality**:
   - **User Authentication**:
     - Replace the static API Key with a dynamic input field.
   - **Token Management**:
     - Implement JWT for secure user sessions.

4. **Example Payload**:

```json
{
    "model": "llama3.2:latest",
    "messages": [
        { "role": "system", "content": "Explain quantum mechanics in simple terms." },
        { "role": "user", "content": "What is Schrödinger's cat?" }
    ],
    "temperature": 0.7,
    "max_tokens": 150
}
```

---

## **Enhancements**

- **Dynamic API Key Input**:
  - Add a text input field to let users enter their own API keys securely.

- **Multiple Model Support**:
  - Provide a dropdown menu to let users select different models.

- **Advanced Parameters**:
  - Add sliders or dropdowns for fields like `top_p` or `frequency_penalty`.

---

## **Contribution**

If you find issues or have suggestions for improvement, feel free to fork the repository and create a pull request. Contributions are welcome!

---

## **License**

This project is licensed under the **MIT License**. Feel free to use, modify, and distribute it for personal or commercial projects. Ensure compliance with OpenWebUI's terms of service.
