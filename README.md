# Product QnA Agentic Chatbot

A product q&a agentic chatbot that answers questions about laptop products using LangChain and LangGraph.

## Overview

This project creates an intelligent product information chatbot that can answer questions about laptops sold by a company. It demonstrates the power of LLMs in creating interactive, context-aware agents that can retrieve and present information naturally.

Key features:
- Built using Llama 3 70B model via Groq API
- Uses BgE embeddings for document retrieval
- Maintains conversation context across multiple interactions
- Supports multi-user sessions with separate conversation histories

## Installation

```bash
# Clone the repository
git clone https://github.com/shaadclt/Product-QnA-Agentic-Chatbot.git
cd Product-QnA-Agentic-Chatbot
```

### Requirements

- Python 3.8+
- Google Colab (for easy setup)
- Groq API key

## Project Structure

- `product_qna_agentic_chatbot.ipynb`: Notebook with code 
- `Laptop pricing.csv`: Contains laptop pricing information
- `Laptop product descriptions.pdf`: Contains detailed product descriptions

## Setup

1. Upload the required CSV and PDF files to your Colab environment
2. Add your Groq API key to Colab secrets:
   ```python
   from google.colab import userdata
   userdata.set("GROQ_API_KEY", "your-groq-api-key-here")
   ```

## How It Works

The chatbot uses the ReAct (Reasoning and Acting) framework to process user queries through a systematic approach:

1. **Tool Integration**:
   - Price lookup tool that queries a CSV database
   - Product feature retrieval tool that searches a vector database of product documentation

2. **Conversation Flow**:
   - Maintains user session history between interactions
   - Supports multiple concurrent users with separate conversation threads

3. **LLM Integration**:
   - Uses Groq's fast API access to Llama 3 70B for high-quality responses
   - Open-source BGE embeddings for semantic search

## Usage Examples

```python
# Single user interaction
inputs = {"messages":[HumanMessage("What are the features and pricing for GammaAir?")]}
for stream in product_QnA_agent.stream(inputs, config, stream_mode="values"):
    message=stream["messages"][-1]
    if isinstance(message, tuple):
        print(message)
    else:
        message.pretty_print()

# Multi-user interaction
config_1 = {"configurable": {"thread_id": str(uuid.uuid4())}}
config_2 = {"configurable": {"thread_id": str(uuid.uuid4())}}

# User 1 asks about SpectraBook
execute_prompt("USER 1", config_1, "Tell me about the features of SpectraBook")

# User 2 asks about GammaAir
execute_prompt("USER 2", config_2, "Tell me about the features of GammaAir")

# Each user's context is maintained separately
execute_prompt("USER 1", config_1, "What is its price?") # Refers to SpectraBook
execute_prompt("USER 2", config_2, "What is its price?") # Refers to GammaAir
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE.txt) file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
