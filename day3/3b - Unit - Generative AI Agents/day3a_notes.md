# 📘 Day 3: Agents

**Podcast:** [Whitepaper Companion Podcast - Agents | 5-Day Gen AI Intensive Course with Google](https://www.youtube.com/watch/D3Kaqz7VW28)   
**Part of:** 5-Day Generative AI Intensive  
**Author:** Rishabh Tiwari (rishtiwari98@gmail.com)  

---

## 🎯 Purpose of the Session

This deep dive covers the inner workings of **generative AI agents**. It explains:
- What an agent is and what it is made of.
- How agents combine generative models with reasoning, tool usage, and orchestration.
- The cognitive architecture that enables agents to operate independently.
- Detailed methods for connecting a language model with external tools and dynamic data.
- How these concepts can be applied to build innovative projects (even a winning Kaggle submission).

---

## 🧩 What Is a Generative AI Agent?

- **Definition:** An agent is a program that goes beyond a standard generative AI model.  
  - **Not limited to:** Just generating text or images.
  - **Adds:** Reasoning logic, decision-making, and the ability to access information beyond its internal training.
- **Key Capabilities:**
  - **Goal-Driven Behavior:** Given a goal, the agent can plan and execute steps to achieve it.
  - **Self-Reliance:** It can determine which steps to take without being given step-by-step instructions.
  - **External Interaction:** By accessing tools, APIs, or data sources, it can update its knowledge and act on external data.

---

## 🏗️ Core Components of an Agent’s Cognitive Architecture

The paper breaks down an agent into **three main parts**:

### 1. The Model (The Brain)
- **Language Model as the Core:**  
  - The generative model (or a combination of models) forms the "brain" of the agent.
  - It is responsible for making decisions and generating responses.
- **Instruction-Based Reasoning:**  
  - Must be capable of using reasoning frameworks such as:
    - **ReAct (Reason and Act):** Guides the model to think through problems step by step and then act.
    - **Chain of Thought (CoT):** Encourages a structured, step-by-step explanation of reasoning.
    - **Tree of Thoughts (ToT):** Explores multiple reasoning paths in parallel to determine the best action.
- **Flexibility:**  
  - The model can be general-purpose, multimodal, or fine-tuned for specific tasks depending on the agent’s needs.

### 2. Tools (The Hands)
- **Purpose of Tools:**  
  - Tools enable the agent to **interact with the external world**.
  - They allow the agent to access up-to-date information and execute actions that the model alone cannot perform.
- **Types of Tools:**
  - **Extensions:**
    - Provide a **standardized way to connect** to APIs.
    - Run on the agent side; they allow the agent to make API calls without handling low-level details.
    - *Example:* A pre-built extension for the Google Flights API.
  - **Functions:**
    - Are self-contained code units that perform specific tasks.
    - Executed on the client side (i.e., in the user's environment).
    - Offer greater control (e.g., for handling authentication or processing API responses).
    - *Example:* A function that simulates an API call when the actual API is not set up.
  - **Data Stores:**
    - Provide **dynamic, up-to-date information** from external sources.
    - Enable the agent to query and retrieve external data (like a continuously updated library).
    - *Example:* Using vector databases as a dynamic knowledge base for retrieval augmented generation (RAG).

### 3. The Orchestration Layer (The Control Center)
- **Role:**  
  - Manages the entire process:
    - **Ingesting information:** Receives and processes user input.
    - **Reasoning:** Determines the sequence of actions using cognitive frameworks.
    - **Acting:** Decides which tool to call or which function to execute.
- **Continuous Loop:**  
  - The orchestration layer cycles through:
    1. **Observation:** Taking in current input and past interaction history.
    2. **Reasoning:** Evaluating the best action based on internal logic and external data.
    3. **Action:** Executing a tool, calling a function, or making a decision.
  - This loop continues until the agent achieves its goal.
- **Analogy:**  
  - Comparable to a chef in a busy kitchen:
    - Receives an order.
    - Checks available ingredients (tools and external data).
    - Plans and executes the cooking process.
    - Adjusts continuously based on feedback (e.g., tasting, checking for errors).

---

## 🛠️ Detailed Reasoning Frameworks for Agents

### A. ReAct (Reason and Act)
- **Concept:**  
  - The model first **reasons through the problem** step by step.
  - It then **acts** by interacting with a tool or API.
- **Process:**  
  1. Receive a user query (e.g., "Book a flight").
  2. Ask clarifying questions (e.g., "Where are you flying from?").
  3. Decide to use a specific tool (e.g., flight API).
  4. Execute the action and receive feedback.
- **Benefit:**  
  - Provides transparency by showing the model’s thought process.

### B. Chain of Thought (CoT)
- **Concept:**  
  - The agent writes out a **step-by-step logical sequence** leading to an answer.
- **Method:**  
  - Instead of returning a direct answer, the agent explains each reasoning step.
- **Variations:**  
  - Self-consistency, active prompt, and even multimodal chain of thought variants.

### C. Tree of Thoughts (ToT)
- **Concept:**  
  - An advanced framework where the agent explores **multiple reasoning paths simultaneously**.
- **Analogy:**  
  - Similar to planning multiple moves in chess:
    - Instead of considering one linear chain, the agent branches out to explore several possible solutions.
- **Outcome:**  
  - Helps the agent select the most promising course of action after evaluating multiple alternatives.

---

## 🔄 How Agents Differ from Standalone Models

### Knowledge and Memory
- **Standalone Model:**
  - Limited to the training data and cannot access real-time or updated information.
- **Agent:**
  - Can access external tools and data stores to retrieve up-to-date information.
  - Supports **multi-turn interactions** and remembers previous interactions for context.

### Tool Integration
- **Standalone Model:**
  - Lacks built-in support for executing external actions.
- **Agent:**
  - Integrates with extensions, functions, and data stores to directly affect the outside world.

### Reasoning and Orchestration
- **Standalone Model:**
  - Typically returns a single prediction based solely on input.
- **Agent:**
  - Uses an orchestration layer to plan, reason, and execute a series of actions until the goal is reached.

---

## 📝 Walkthrough: Example of a Flight Booking Agent (Using ReAct)

1. **Initial Query:**
   - User asks: "I want to book a flight."
2. **Clarification:**
   - The agent asks: "Where are you flying from?"
3. **Reasoning:**
   - The agent internally decides the best way to retrieve flight information.
   - It determines that calling a flight API would be necessary.
4. **Action:**
   - The agent uses a tool (an extension) to call the Google Flights API.
   - It sends the user’s input (e.g., departure city) to the API.
5. **Feedback and Follow-Up:**
   - The API returns flight options.
   - The agent may then ask: "What are your preferred travel dates?"
6. **Iteration:**
   - The agent continues this cycle until it gathers all necessary details.
   - Once complete, it processes the information and finalizes the booking.

---

## 🛠️ In-Depth Look at Tools in Agents

### Extensions
- **Definition:**
  - Standardized modules that let the agent call APIs directly.
- **Characteristics:**
  - Executed on the agent side.
  - Simplify API usage by abstracting low-level details.
- **Example:**
  - A pre-built code interpreter extension that allows execution of Python code.

### Functions
- **Definition:**
  - Self-contained pieces of code that execute specific tasks.
- **Characteristics:**
  - Called by the model but executed on the client side.
  - Offer more control over security and error handling.
- **Example:**
  - In a flight booking scenario, the agent decides which function to use; then, the client application makes the actual API call.

### Data Stores
- **Definition:**
  - External repositories that hold dynamic, up-to-date information.
- **Characteristics:**
  - Allow agents to access and query large, external datasets.
  - Often implemented using vector databases for semantic search.
- **Example:**
  - A data store holding up-to-date company documents or web pages used for retrieval augmented generation (RAG).

---

## 🧠 Enhancing Agent Performance

### Three Approaches to Empower Agents:
1. **In-Context Learning:**
   - Provide the agent with a detailed recipe (prompt), ingredients (tools), and examples.
   - The agent learns from the prompt on how to handle the task.
2. **Retrieval-Based In-Context Learning:**
   - Augment the agent’s internal knowledge with external data retrieved in real time.
   - Works similarly to RAG by combining internal reasoning with external facts.
3. **Fine-Tuning Based Learning:**
   - Train the model further on a large, domain-specific dataset.
   - Specializes the model so it becomes an expert at using particular tools or handling specific tasks.

---

## 💡 Agent Quick Start with LangChain

- **Framework:**  
  - The paper shows how to build a simple yet functional agent using LangChain (and LangGraph).
- **Setup:**
  - Use the **Gemini 2.0 FL001** model.
  - Define two tools:
    1. One for **searching Google**.
    2. One for **retrieving information from the Google Places API**.
- **Example Query:**
  - "Who did the Texas Longhorns play in their last game and what's the address of the stadium?"
- **Flow:**
  1. The agent first searches for the opponent.
  2. Then, it uses that information to retrieve the stadium’s address.
- **Code Snippets:**
  - Snippet 8 shows how to set up API keys, define tools, and initialize the react agent.
  - Snippet 9 demonstrates the agent’s output by showing the step-by-step reasoning and tool usage.

---

## 🖥️ Production-Grade Agent Considerations

- **Vertex AI Agents:**
  - A managed platform from Google offering:
    - User interfaces for interacting with agents.
    - Tools for evaluating agent performance.
    - Systems for continuous improvement and model updates.
  - Provides a natural language interface to define tasks, select tools, and even give examples of desired behavior.
- **Key Benefit:**
  - Simplifies the entire process of building, deploying, and managing sophisticated agent applications.

---

## 🔄 Recap & Final Takeaways

- **Agents vs. Standalone Models:**
  - Agents combine a powerful language model with external tools and an orchestration layer.
  - They can access real-time data, remember past interactions, and execute multi-step processes.
- **Three Main Components:**
  1. **Model (Brain):** Makes decisions using reasoning frameworks.
  2. **Tools (Hands):** Enable external actions (extensions, functions, data stores).
  3. **Orchestration Layer (Control Center):** Manages multi-turn interactions, reasoning, and planning.
- **Reasoning Frameworks:**
  - **ReAct, Chain of Thought, and Tree of Thoughts** are critical for guiding agent behavior.
- **Tool Categories:**
  - **Extensions** for direct API control.
  - **Functions** for controlled, client-side execution.
  - **Data Stores** for dynamic, external knowledge.
- **Empowering Agents:**
  - Use in-context learning, retrieval augmentation, and fine-tuning to specialize agents.
- **Practical Application:**
  - LangChain examples demonstrate how to build a multi-step agent that answers complex queries.
- **Production:**
  - Platforms like Vertex AI provide the necessary infrastructure for real-world, scalable agent deployments.

---

*Prepared by: **Rishabh Tiwari***  
📧 *rishtiwari98@gmail.com*  
📅 *Day 3 – 5-Day Generative AI Intensive*
