# Episode 08: ReAct Intro to AI Agents | Study Notes

## Overview
This lecture introduces the **ReAct** framework, which stands for **Reasoning and Action**. It explains how AI technology is evolving from simple Large Language Models (LLMs) that only answer questions into full-fledged **AI Agents** capable of performing real-world tasks like booking tickets or checking live weather. The core problem addressed is that LLMs are trained on **historical data** and lack real-time knowledge. ReAct solves this by allowing the LLM to "think" and "act" in a loop, using external **tools** and **APIs** to find current information and perform calculations. By the end of the lecture, a Python implementation is demonstrated to show how an LLM can use a calculator and a price-checking tool to solve a complex user query.

---

## Main Topics

### 1. From LLM to AI Agents
*   **Definition**: An **LLM** (Large Language Model) is a model you give a prompt to, and it returns an answer based on its training. An **AI Agent** is a full-fledged service that can perform actions like booking flights or hotels.
*   **Explanation**: The transition from LLM to AI Agent happens when we give the model the ability to interact with the world.
*   **Why it is important**: It makes AI useful for practical, real-time tasks rather than just answering general knowledge questions.
*   **Key Concepts**: The line between an LLM and an Agent is crossed using the **ReAct** framework.

### 2. The Problem: Historical Training Data
*   **Definition**: Training data is the massive amount of internet information used to teach the AI up until a certain "cutoff" date.
*   **Explanation**: If ChatGPT was trained until July 20th, 2026, it cannot know the temperature or news on July 25th, 2026.
*   **Why it is important**: LLMs cannot answer questions about the **present** or **real-time** events (e.g., today's hotel prices in Dubai) based solely on training.
*   **Examples**: Checking today's temperature in Bangalore or current flight prices.

### 3. The Solution: Tools and APIs
*   **Definition**: **Tools** are external functions (like a calculator) or **APIs** (Application Programming Interfaces) that provide the LLM with new information.
*   **Explanation**: Instead of relying on memory, the LLM is given access to tools. For example, it can use a weather API to get today's temperature.
*   **Why it is important**: It allows the AI to provide accurate, real-time data it wasn't originally trained on.
*   **Common Misconceptions**: People think LLMs calculate math like "5000 - 2000" from memory; in reality, complex math is better handled by a **calculator tool**.

### 4. The ReAct Framework (Reasoning + Action)
*   **Definition**: ReAct is a framework where the LLM follows a loop of **Reasoning** (thinking about what to do) and **Action** (using a tool).
*   **Explanation**: The process works in a loop:
    1.  **Thought**: The LLM analyzes the prompt and decides what it needs to know.
    2.  **Action**: It calls a specific tool (e.g., GetPrice).
    3.  **Observation**: It looks at the result returned by the tool.
    4.  **Repeat**: It uses that observation to decide the next thought/action until the task is complete.
*   **Example**: Buying an iPhone 17 with ₹5,000.
    *   *Step 1*: **Thought** - I need the price of iPhone 17. **Action** - Call GetPrice tool. **Observation** - ₹2,000.
    *   *Step 2*: **Thought** - I have ₹5,000 and the phone is ₹2,000. I need to subtract. **Action** - Call Calculator tool. **Observation** - ₹3,000.
    *   *Step 3*: **Final Answer** - You will have ₹3,000 left.

### 5. Implementation in Code
*   **Step-by-Step Process**:
    1.  **Define Tools**: Create Python functions (e.g., `get_product_price`, `calculator`).
    2.  **System Prompt**: Write a detailed instruction telling the LLM it is an assistant with specific tools and must follow the **Thought/Action/Observation** format.
    3.  **The Loop**: Run a loop (e.g., for 5 steps) where the LLM provides a "Thought" and "Action", the code executes the tool, and the "Observation" is fed back into the LLM's memory.
    4.  **Memory**: Use the **Assistant Role** to append the LLM's previous thoughts and tool results to the message history so it remembers what it has already done.

---

## Important Definitions
*   **ReAct**: A framework combining **Reasoning** and **Acting** for LLMs.
*   **AI Agent**: An AI system that uses tools to complete complex, multi-step tasks independently.
*   **API**: A way for the AI to "ask" another service for information (like asking MakeMyTrip for hotel prices).
*   **Reasoning**: The internal "thinking" process where an LLM decides which step to take next.
*   **Observation**: The data or result returned by a tool after an action is taken.
*   **System Prompt**: High-level instructions that define the AI's personality, tools, and rules.

---

## Important Rules & Syntax
1.  **One Tool at a Time**: The LLM should only call one tool per step to maintain logic.
2.  **Stop After Action**: After writing an "Action", the LLM must stop and wait for the code to provide the "Observation".
3.  **Never Invent Results**: The LLM must use the tool's result, not guess or hallucinate an answer (e.g., don't guess the price of an iPhone if the tool hasn't returned it).
4.  **Python `eval()`**: Used in the calculator tool to solve mathematical expressions string-converted to code.
5.  **Rate Limiting**: Use `time.sleep(5)` between LLM calls to avoid being blocked by the service provider.

---

## Tables

### LLM vs. AI Agent
| Feature | Simple LLM | AI Agent (with ReAct) |
| :--- | :--- | :--- |
| **Capability** | Answers questions from training data | Performs tasks/services (booking, searching) |
| **Data Source** | Static Historical Data | Real-time Tools & APIs |
| **Process** | One-shot Prompt & Answer | Iterative Reasoning + Action Loop |
| **Math/Logic** | May hallucinate or guess | Uses specific tools (Calculators) |

---

## Diagrams

### The ReAct Loop Flowchart
```text
User Input (Prompt) 
       |
       v
+--------------------------+
|  LLM Thought Process     | <----------+
| (Decide what to do next) |            |
+--------------------------+            |
       |                                |
       v                                |
+--------------------------+            |
|     Action Call          |            |
| (Select Tool & Argument) |            |
+--------------------------+            |
       |                                |
       v                                |
+--------------------------+            | Loop (e.g., 5 steps)
|   Tool Execution (Code)  |            |
| (API Call or Function)   |            |
+--------------------------+            |
       |                                |
       v                                |
+--------------------------+            |
|      Observation         |            |
| (Result from the Tool)   | -----------+
+--------------------------+
       |
       v
+--------------------------+
|     Final Answer         |
| (Task Complete)          |
+--------------------------+
```


---

## Key Takeaways
*   ReAct is the bridge that turns an **LLM into an AI Agent**.
*   LLMs are limited by their **training cutoff date**; tools provide them with "eyes and ears" for the present world.
*   The ReAct process is: **Thought -> Action -> Observation**.
*   A **System Prompt** is the most important part of implementation; you must explain the ReAct logic to the LLM clearly.
*   Memory is maintained by appending every thought and observation to the **messages history**.

---

## Revision Notes (One-Page)
*   **Concept**: ReAct = Reasoning + Action.
*   **Goal**: Solve tasks requiring real-time info or complex logic.
*   **Mechanism**:
    *   Input: User Prompt + Tool List + Instructions.
    *   Iteration: LLM writes "Thought" and "Action". Code runs "Action" and gets "Observation".
    *   Final: LLM uses all observations to give a "Final Answer".
*   **Implementation Tips**:
    *   Use **Regular Expressions (Regex)** to extract the Tool Name and Input from the LLM response.
    *   Always use `temperature=0` for consistent logical steps.
    *   Treat the LLM as a "very smart but literal" assistant; be extremely detailed in the system prompt.
    *   Include a "Final Answer" keyword so the code knows when to break the loop.

---

## Interview / Viva Questions
1.  **What does ReAct stand for?**
    *   Reasoning and Action.
2.  **Why can't an LLM tell you today's weather from its training data?**
    *   Because it is trained on historical data up to a specific cutoff date and cannot see the live world.
3.  **What is the difference between an Action and an Observation in ReAct?**
    *   Action is the LLM choosing a tool to call; Observation is the result returned by that tool.
4.  **How do you prevent an LLM from hallucinating math results?**
    *   By providing it with a calculator tool and instructing it to use it instead of guessing.
5.  **What role does the System Prompt play in ReAct?**
    *   It defines the tools, the syntax for calling them, and the reasoning steps the LLM must follow.
6.  **Why do we use a loop (like `range(5)`) in the ReAct code?**
    *   To allow the LLM to take multiple steps (e.g., check price, then calculate) to reach the final answer.
7.  **What is an AI Agent?**
    *   A system that uses an LLM as a "brain" to use tools and complete services.
8.  **How do you handle memory in a ReAct loop?**
    *   By appending the LLM's responses (Assistant role) and tool results back into the messages array.
9.  **What is the "Thought" part of the ReAct loop?**
    *   The LLM explaining its reasoning process before it takes an action.
10. **Why is `time.sleep()` used in the implementation?**
    *   To avoid hitting rate limits of the AI model provider during fast, repeated calls.

---

## Practice Questions

### Easy (10 Questions)
1. Define ReAct in your own words.
2. List three examples of tools an AI agent might use.
3. What is the cutoff date for training data?
4. True or False: ReAct requires a JavaScript library.
5. What are the three main steps in a ReAct iteration?
6. Why is a calculator useful for an LLM?
7. What is an API?
8. Name one advantage of an AI Agent over a simple LLM.
9. What happens if you don't give an LLM tools?
10. What does the "Observation" step represent?

### Medium (10 Questions)
1. Explain how the iPhone buying example uses two different tools.
2. Why is a simple `if-else` statement insufficient for choosing tools?
3. How does "Assistant Role" help the LLM in the next step of the loop?
4. Describe the purpose of using Regular Expressions in the Python code.
5. Why should an LLM stop immediately after writing an "Action"?
6. How does the complexity of a user prompt (like the Dubai trip example) affect the ReAct loop?
7. What is the consequence of a "loose" or poorly written system prompt?
8. Explain the "Chain" concept in tool usage (output of Tool A as input for Tool B).
9. Why is `temperature=0` recommended for ReAct agents?
10. How can an LLM decide which tool to use among 20,000 available tools?

### Challenging (5 Questions)
1. Design a ReAct flow for a user wanting to "Compare the stock price of Apple and Tesla and email the summary to me." What tools are needed?
2. Discuss the design decision of choosing the number of steps (e.g., 5 vs 20) in a ReAct loop.
3. How would you handle a situation where a tool (API) returns an error?
4. Compare "Good Models" vs "Bad Models" in the context of reasoning and tool usage.
5. Create a system prompt that forces an LLM to use a "Search" tool before answering any question about a person.

---

## Flashcards
1.  **Q**: ReAct Full Form? **A**: Reasoning + Action.
2.  **Q**: LLM vs Agent? **A**: LLM answers; Agent does tasks.
3.  **Q**: Training Data Limit? **A**: Knowledge stops at the cutoff date.
4.  **Q**: Tool for live data? **A**: API.
5.  **Q**: ReAct Step 1? **A**: Thought.
6.  **Q**: ReAct Step 2? **A**: Action.
7.  **Q**: ReAct Step 3? **A**: Observation.
8.  **Q**: Action -> Observation transition? **A**: LLM stops; Code runs tool.
9.  **Q**: Why no guessing? **A**: To prevent hallucinations.
10. **Q**: Python tool example? **A**: A function like `calculator(exp)`.
11. **Q**: System Prompt role? **A**: Instructions/Rules for the LLM.
12. **Q**: Loop range? **A**: Maximum steps allowed to solve a query.
13. **Q**: Memory storage? **A**: Messages array (history).
14. **Q**: Tool name extraction? **A**: Regex (Regular Expressions).
15. **Q**: AI "Thinking" visibility? **A**: Shown in Gemini as "Show Thinking" or in code as "Thought".
16. **Q**: Rate Limit solution? **A**: `time.sleep()`.
17. **Q**: User Language? **A**: General English/Natural Language.
18. **Q**: Is ReAct pre-built? **A**: No, it's a concept/loop you implement.
19. **Q**: iPhone 17 Example Tool 1? **A**: Get Product Price.
20. **Q**: iPhone 17 Example Tool 2? **A**: Calculator.

---

## Cheat Sheet
*   **ReAct Concept**: Thought -> Action -> Observation -> Final Answer.
*   **The Problem**: Training data is historical; tools provide current data.
*   **The Code**:
    *   **Tools**: Python functions.
    *   **Prompt**: Explain Thought/Action/Observation strictly.
    *   **Loop**: Use a `for` loop to iterate steps.
    *   **Memory**: Append every step to history.
    *   **Regex**: Use to find tool name and inputs.
*   **Core Rule**: Treat the LLM as a tool-user; tell it *what* tools exist and *how* to call them.