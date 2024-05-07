
## Revised Lab Description:

### Step 1: Chat Completion (Basic)
Set up a basic chat interface using the OpenAI API to send prompts and receive responses. This step establishes the foundation for building more complex AI interactions.

**Tasks Accomplished:**
- Set up API key configuration for OpenAI.
- Send a basic user prompt to the model.
- Receive and display the model's response.

<details>
<summary><strong>Python Code Example</strong></summary>

```python
import openai

# Set your OpenAI API key
openai.api_key = 'your-api-key'

response = openai.ChatCompletion.create(
  model="gpt-3.5-turbo",
  messages=[
      {"role": "system", "content": "You are a helpful AI."},
      {"role": "user", "content": "I'm looking for a book recommendation."}
  ]
)

print(response['choices'][0]['message']['content'])
```

</details>

<details>
<summary><strong>JavaScript Code Example</strong></summary>

```javascript
const { Configuration, OpenAIApi } = require("openai");

const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
});
const openai = new OpenAIApi(configuration);

async function chatCompletion() {
  try {
    const response = await openai.createChatCompletion({
      model: "gpt-3.5-turbo",
      messages: [
        { role: "system", content: "You are a helpful AI." },
        { role: "user", content: "I'm looking for a book recommendation." }
      ]
    });
    console.log(response.data.choices[0].message.content);
  } catch (error) {
    console.error(error);
  }
}

chatCompletion();
```

</details>

### Step 2: Scrape and Vectorize Data
This step involves scraping web content and creating a vector database from the content. You will scrape paragraphs from a website and vectorize each paragraph to create a searchable vector database.

**Tasks Accomplished:**
- Fetch and parse HTML content from a URL.
- Extract paragraphs as text from the HTML content.
- Convert each paragraph into a vector using OpenAI's embedding API.
- Store each paragraph and its vector in a structured format.

<details>
<summary><strong>Python Code Example</strong></summary>

```python
import requests
from bs4 import BeautifulSoup
import openai

# Scrape content from a URL
def scrape_content(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    paragraphs = [p.text for p in soup.find_all('p')]
    return paragraphs

# Send paragraphs to OpenAI for vectorization and store them in the desired format
def vectorize_paragraphs(paragraphs):
    vector_data = []
    for paragraph in paragraphs:
        vector_response = openai.Embedding.create(
            input=paragraph,
            model="text-embedding-ada-002"
        )
        vector = vector_response['data'][0]['embedding']
        vector_data.append({'paragraph': paragraph, 'embedding': vector})
    return vector_data

# Example URL
url = "https://www.novelreads.com/latest-releases"
paragraphs = scrape_content(url)
vector_data = vectorize_paragraphs(paragraphs)
```

</details>

<details>
<summary><strong>JavaScript Code Example</strong></summary>

```javascript
const axios = require('axios');
const cheerio = require('cheerio');

async function scrapeContent(url) {
  const { data } = await axios.get(url);
  const $ = cheerio.load(data);
  const paragraphs = $('p').map((i, el) => $(el).text()).get();
  return paragraphs;
}

async function vectorizeParagraphs(paragraphs) {
  const vectorData = [];
  for (let paragraph of paragraphs) {
    // Simulate vectorization (actual API call needed)
    const vector = { paragraph: paragraph, embedding: "vector_placeholder" };
    vectorData.push(vector);
  }
  return vectorData;
}

const url = "https://www.novelreads.com/latest-releases";
scrapeContent(url).then(paragraphs => {
  vectorizeParagraphs(paragraphs).then(vectorData => {
    console.log(vectorData);
  });
});

```

</details>

### Step 3: Connect To Your Data (Advanced)
In this step, use the previously created vector database to enhance the AI’s responses. The AI will query the vector database for context relevant to the user’s queries, dynamically adjusting its responses accordingly.

**Tasks Accomplished:**
- Query the vector database for the most relevant paragraph based on the user's input.
- Utilize the retrieved paragraph to inform and contextualize the AI’s response.

<details>
<summary><strong>Python Code Example</strong></summary>

```python
import openai

# Function to fetch relevant context from vector database
def get_relevant_context(query, vector_data):
    # Example function that simulates fetching the most relevant paragraph
    return vector_data[0]['paragraph']  # Simplified example

# Retrieve relevant data to add context
relevant_context = get_relevant_context("latest bestsellers", vector_data)

response = openai.ChatCompletion.create(
  model="gpt-3.5-turbo",
  messages=[
      {"role": "system", "content": f"You are a helpful AI. {relevant_context}"},
      {"role": "user", "content": "Tell me about the latest bestsellers."}
  ]
)

print(response['choices'][0]['message']['content'])
```
</details>

<details>
<summary><strong>JavaScript Code Example</strong></summary>

```javascript
async function getRelevantContext(query, vectorData) {
  // Simulated function to fetch most relevant paragraph
  return vectorData[0].paragraph; // Simplified example
}

// Assume 'vectorData' is available and has the structure [{paragraph: 'text', embedding: [vector]}]
const relevantContext = getRelevantContext("latest bestsellers", vectorData);

// Simulate response from AI with the relevant context
console.log(`AI Response: You asked about ${relevantContext}`);
```

</details>