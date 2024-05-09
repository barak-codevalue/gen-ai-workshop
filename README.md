
# Generative AI Workshop: From Concept to Creation

## Workshop Description

### What You'll Learn
This is a 60 minute workshop that consists of a series of lab exercises that teach you how to build a production RAG (Retrieval Augmented Generation) based LLM application using OpenAI and Pinecone vector DB.

### Workshop Objectives
- Understand the fundamentals of Generative AI technology and its applications.
- Develop a Generative AI solution using Python or JavaScript.
- Experiment with various AI prompting techniques.
- Implement Retrieval Augmented Generation (RAG) to enhance AI responses with external data.
- Build a scalable AI agent capable of performing specific tasks.
- Learn to estimate and manage the computational costs associated with running AI solutions.

By completing this workshop, you'll gain the skills needed to tackle advanced development challenges in the field of Generative AI.

### Pre-Requisites
- Programming knowledge in Python or JavaScript.
- GitHub & Visual Studio Code
- OpenAI api key
- Pinecone api key

## Additional Resources
For more detailed information about the APIs used in this workshop, refer to the [OpenAI Platform Documentation](https://platform.openai.com/docs/overview).

## Dev Environment:
For this lab we will use [GitHub Codespaces](https://docs.github.com/en/codespaces) or VS Code.
- Fork the repo into your GitHub profile
- Click "Code" dropdown, select "Codespaces" tab
- Click "+" to create new codespace
- Verify you see 'Setting up your codespace' in new tab

## Scenario Story
You've recently joined the development team at NovelReads, a thriving online bookstore with a broad range of titles and a dedicated reader community. Despite the success in sales, customer inquiries regarding book recommendations, availability, and order status updates have surged, leading to a bottleneck in customer service responses.

The challenge lies in enhancing customer experience without compromising service quality. As the latest addition to the team, your mission is to design and implement a Generative AI customer support agent on the NovelReads platform. This AI should not only address common queries efficiently but also provide personalized book recommendations, thereby reducing the workload on human agents and ensuring customer satisfaction.

## Lab Description:
### Step 1: Create a Basic REST Endpoint
In this initial step, you will create a REST endpoint that serves as the foundation of your application. This endpoint will eventually interact with OpenAI's GPT model and Pinecone's vector database to handle RAG-based queries.

**Tasks Accomplished:**
- Create a basic REST API that listens to POST requests..
- Implement a simple route to test the server setup, using /chat as the endpoint.

<details>
<summary><strong>Python Code Example</strong></summary>

```python
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/chat', methods=['POST'])
def chat_endpoint():
    data = request.json
    return jsonify({"message": "Received", "yourData": data}), 200

if __name__ == '__main__':
    app.run(debug=True, port=5000)

```

</details>

<details>
<summary><strong>JavaScript Code Example</strong></summary>

```javascript
const express = require('express');
const app = express();
app.use(express.json());

app.post('/chat', (req, res) => {
    res.status(200).json({message: 'Received', yourData: req.body});
});

app.listen(3000, () => {
    console.log('Server is running on http://localhost:3000');
});

```

</details>


### Step 2: Integrate OpenAI Chat Completion
In this step, you'll enhance the /chat endpoint to interact with OpenAI's ChatGPT. The endpoint will take user input, send it to OpenAI for processing, and return the AI-generated response. This integration forms the basic system for handling user queries through your application.

**Tasks Accomplished:**
- Install necessary libraries for interacting with the OpenAI API.
- Set up environment variables for API key management.
- Modify the endpoint to send user input to OpenAI and respond with the AI's completion.

<details>
<summary><strong>Python Code Example</strong></summary>

```python
# New imports for OpenAI
import openai

# Configuration for OpenAI API
openai.api_key = 'your-openai-api-key'  # Replace with your actual API key

# Modified /chat endpoint to integrate OpenAI
@app.route('/chat', methods=['POST'])
def chat_endpoint():
    user_input = request.json.get('text')
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[
            {"role": "system", "content": "You are a helpful AI."},
            {"role": "user", "content": user_input}
        ]
    )
    return jsonify({"response": response.choices[0].message['content']}), 200

```

</details>

<details>
<summary><strong>JavaScript Code Example</strong></summary>

```javascript
// New imports for OpenAI
const { Configuration, OpenAIApi } = require('openai');

// Configuration for OpenAI API
const configuration = new Configuration({
    apiKey: 'your-openai-api-key',  // Replace with your actual API key
});
const openai = new OpenAIApi(configuration);

// Modified /chat endpoint to integrate OpenAI
app.post('/chat', async (req, res) => {
    const userInput = req.body.text;
    try {
        const response = await openai.createChatCompletion({
            model: "gpt-3.5-turbo",
            messages: [
                {role: "system", content: "You are a helpful AI."},
                {role: "user", content: userInput}
            ]
        });
        res.status(200).json({response: response.data.choices[0].message.content});
    } catch (error) {
        res.status(500).json({message: "Error processing your request"});
    }
});

```

</details>

### Step x: Chat Completion
desc

**Tasks Accomplished:**
- 1.
- 2.
- 3.

<details>
<summary><strong>Python Code Example</strong></summary>

```python

```

</details>

<details>
<summary><strong>JavaScript Code Example</strong></summary>

```javascript

```

</details>