# Lecture Title: Free AI Engineer Course | Episode 09: Prompt Chaining

## Overview
This lecture introduces **Prompt Chaining**, a strategic workflow used to handle **complex tasks** in Large Language Model (LLM) development. Instead of sending one massive prompt to an LLM, the process involves breaking the task into smaller, manageable **sub-tasks**. The session covers the fundamental differences between Prompt Chaining and the **ReAct** framework, the core benefits of chaining—such as **debugging**, **modularity**, and **cost-efficiency**—and provides a practical Python implementation using a **Resume Parsing** project.

---

## Main Topics

### Topic 1: ReAct (Reasoning and Action) Concept
*   **Definition:** **ReAct** is a concept where an LLM independently decides which tools to use, how to use them, and when to use them based on a prompt.
*   **Explanation:** In ReAct, the developer provides the tools and a prompt, and the LLM "thinks" (reasoning) and "acts" by selecting tools. It is not something you "implement" as a library, but rather the underlying logic of **AI Agents**.
*   **Why it is important:** It serves as the foundation for how AI agents function autonomously.
*   **Common Misconceptions:** Students often think ReAct needs to be manually implemented in code for every project, but it is actually the logic the LLM uses to handle tool selection.

### Topic 2: Prompt Chaining
*   **Definition:** **Prompt Chaining** is the process of breaking a complex task into multiple sub-prompts, where the output of one LLM call is passed as input to the next.
*   **Explanation:** Think of it like building a house. Instead of telling one person "Build me a house" (one big prompt), you break it down: buy land, create a blueprint, dig the foundation, and paint. Each step is a separate prompt with its own LLM call.
*   **Why it is important:** Complex tasks in a professional environment are prone to errors; chaining makes these tasks manageable and reliable.
*   **Step-by-step Process (Resume Matcher Example):**
    1.  **Step 1:** Extract skills from a candidate's resume.
    2.  **Step 2:** Extract required skills from a Job Description (JD).
    3.  **Step 3:** Pass both sets of skills to a third LLM call to match them and generate a score.
    4.  **Step 4:** Use logic (like If/Else) to decide whether to call the HR or send a rejection email.

### Topic 3: Advantages of Prompt Chaining
*   **Debugging:** If a system produces a wrong result (e.g., a good candidate gets a low score), you can check each step individually to find where the error occurred (extraction, matching, or scoring).
*   **Modularity:** You can fix or update one specific part of the chain (like the PDF reader) without rewriting the entire program.
*   **Different Models (Cost/Performance):** You can use **expensive, strong models** (like Claude 3.5 Sonnet) for complex extraction and **cheap/free models** (like GPT-4o-mini) for simple tasks like sending an email.
*   **Retrying Steps:** You can program the system to retry a specific step until it is perfect.

### Topic 4: Prompt Chaining vs. ReAct
*   **Key Concepts:**
    *   In **ReAct**, the **LLM** decides the steps and tool usage.
    *   In **Prompt Chaining**, the **Developer** decides the exact sequence and flow of steps.
*   **Tips from Instructor:** In a professional setting, chaining is often preferred because it gives the developer more control over the workflow.

---

## Important Definitions
*   **Prompt Chaining:** A workflow where a task is divided into sub-tasks, each handled by a separate prompt and LLM call.
*   **ReAct:** Standing for Reasoning and Action; the conceptual framework of how an LLM decides to interact with tools.
*   **Global Variable:** A variable defined outside of functions that can be accessed by any function within the code.
*   **f-strings (Formatted Strings):** A Python syntax (starting with `f"..."`) used to embed variables directly inside strings.
*   **Modularity:** A design principle where a system is divided into separate, independent parts.

---

## Important Formulas / Syntax / Rules
*   **Python f-string Syntax:** `f"Text {variable_name}"`. This is crucial for passing dynamic data (like resumes) into prompts.
*   **Time Sleep:** `time.sleep(2)` is used between multiple LLM calls to prevent overlapping or rate-limiting issues.
*   **General LLM Function Rule:** Always create a reusable function (e.g., `ask_llm`) that takes a `system_prompt` and `user_prompt` to keep the code clean.

---

## Tables

### Comparison: Prompt Chaining vs. ReAct
| Feature | Prompt Chaining | ReAct |
| :--- | :--- | :--- |
| **Decision Maker** | Developer/Human | LLM |
| **Workflow** | Pre-defined sequence | Dynamic/Autonomous |
| **Control** | High | Low (LLM decides) |
| **Use Case** | Structured business logic | Agentic tool use |

---

## Diagrams

### Prompt Chaining Architecture (Resume Example)
```text
[Input: Resume] -> [Prompt 1: Extract Skills] -> [Output: Skill List] 
                                                        |
                                                        v
[Input: JD]     -> [Prompt 2: Extract Skills] -> [Output: JD Skills]
                                                        |
                                                        v
[Output: Skill List] + [Output: JD Skills] -> [Prompt 3: Match & Score] -> [Final Score]
                                                                              |
                                                                              v
                                                                      [Conditional Logic]
                                                                      /               \
                                                           (Score > 60)              (Score < 60)
                                                                |                         |
                                                         [Call HR]                [Send Rejection Email]
```


---

## Key Takeaways
*   **Divide and Conquer:** Complex AI tasks should be broken into sub-tasks for better accuracy.
*   **Developer Control:** Chaining allows you to dictate exactly when and how the LLM processes data.
*   **Cost Efficiency:** Don't waste "expensive" tokens on simple tasks; use the right model for the right job.
*   **Debugging is Easier:** Modular code allows you to identify exactly which prompt or function is failing.

---

## Revision Notes
*   **Prompt Chaining** = Breaking 1 big task into small sub-tasks.
*   **Why?** Debugging, Modularity, Saving Money (different models), and Control.
*   **ReAct** = LLM decides what to do; **Chaining** = Developer decides.
*   **Coding Tip:** Use `f-strings` in Python to pass data into prompts; otherwise, the LLM won't see your variables.
*   **Workflow:** Prompt 1 Output -> Input for Prompt 2.

---

## Interview / Viva Questions
1.  **What is the core difference between ReAct and Prompt Chaining?**
    *   Answer: In ReAct, the LLM decides the tools and sequence; in Chaining, the developer defines the sequence.
2.  **Why is Prompt Chaining better for debugging?**
    *   Answer: You can check the output of each individual step/prompt to see exactly where the logic failed.
3.  **How does Prompt Chaining save money in production?**
    *   Answer: You can use cheaper models for simple tasks (like emails) and expensive ones only for complex reasoning.
4.  **What is a "sub-task" in the context of chaining?**
    *   Answer: A small, specific part of a larger project, like "extract skills" instead of "parse the whole resume".
5.  **What happens if you don't use f-strings in Python prompts?**
    *   Answer: The LLM receives the literal variable name as a string instead of the actual data inside the variable.
6.  **Can you use different LLMs in the same chain?**
    *   Answer: Yes, you can call different models for different steps based on their strength and cost.
7.  **What is the role of the developer in Prompt Chaining?**
    *   Answer: The developer acts as the architect, deciding the order of execution and logic between calls.
8.  **Is ReAct a library you import?**
    *   Answer: No, it is a concept of reasoning and action that AI agents follow.
9.  **Why should we use `time.sleep()` in chaining?**
    *   Answer: To prevent hitting rate limits when making multiple rapid calls to an API.
10. **What is modularity in AI workflows?**
    *   Answer: The ability to change or fix one specific function (like the skill extractor) without breaking the rest of the system.

---

## Practice Questions
### Easy
1. Define Prompt Chaining in your own words.
2. Name two benefits of using sub-tasks.
3. What does ReAct stand for?.
4. Why is a single giant prompt bad for complex tasks?.
5. How do you inject a variable into a Python string?.
6. What is the purpose of a `system_prompt`?.
7. Give an example of a simple task that doesn't need an expensive model.
8. What is a "Wordict" (Verdict) in the resume project?.
9. How do you handle a scenario where a candidate's score is below 60?.
10. What is a global variable?.

### Medium
1. Explain the "House Building" analogy for prompt chaining.
2. How would you debug a chain if the final output is "No Resume Provided"?.
3. Contrast how a developer spends their time on code vs. debugging in a company.
4. Design a 3-step chain for a weather-based travel recommender.
5. Why would an LLM hallucinate skills if not instructed otherwise?.
6. Explain why `Claude 3.5 Sonnet` might be used for Step 1 but `GPT-4o-mini` for Step 4.
7. How does the "Burbak Bachha" (slow student) analogy apply to LLM selection?.
8. What is the risk of letting the LLM decide the workflow (ReAct) in a strict business process?.
9. How can you ensure the LLM returns only a comma-separated list of skills?.
10. Describe the flow of data from Step 1 to Step 3 in the lecture's resume project.

### Challenging
1. Implement a retry logic where Step 1 is repeated if the skill list is empty.
2. How does prompt chaining solve the "black box" problem of single-prompt LLM calls?.
3. Create a comparison between "Modular Code" and "Spaghetti Code" based on the lecture's modularity points.
4. Discuss the financial implications for a startup choosing between ReAct agents and Prompt Chaining workflows.
5. Analyze the debugging process shown in the lecture: why did the instructor use `print(step1)`?.

---

## Flashcards
1. **Q: Prompt Chaining** -> **A:** Breaking a complex task into sub-prompts where outputs flow into inputs.
2. **Q: ReAct** -> **A:** Reasoning and Action; LLM-led tool selection and decision making.
3. **Q: Main benefit of Chaining** -> **A:** Easier debugging and modularity.
4. **Q: Who decides the steps in Chaining?** -> **A:** The Developer.
5. **Q: Who decides the steps in ReAct?** -> **A:** The LLM.
6. **Q: Cost-saving tip** -> **A:** Use cheap models for simple steps (emails) and expensive ones for complex steps.
7. **Q: Modular code** -> **A:** Code where you can fix one part without changing everything.
8. **Q: f-string purpose** -> **A:** To include variables inside string prompts.
9. **Q: Prompt Chaining step example** -> **A:** 1. Extract Resume Skills -> 2. Match with JD.
10. **Q: Debugging trick** -> **A:** Print the output of every intermediate LLM call.
11. **Q: Rate limiting fix** -> **A:** Use `time.sleep()` between calls.
12. **Q: Why break tasks?** -> **A:** Large prompts are hard to fix and prone to error.
13. **Q: Resume Project Step 3** -> **A:** Match candidate skills vs JD skills and score.
14. **Q: Conditional logic in Chaining** -> **A:** Using Python `if/else` on LLM outputs.
15. **Q: "Professional Assistant" role** -> **A:** Common persona given to LLMs in system prompts.
16. **Q: Output Formatting** -> **A:** Telling the LLM exactly how to return data (e.g., CSV or List).
17. **Q: LLM "Thinking"** -> **A:** The 'Reasoning' part of ReAct.
18. **Q: Chain of Responsibility** -> **A:** In chaining, the developer is responsible for the flow.
19. **Q: Complex Task** -> **A:** Tasks requiring multiple steps like resume parsing or home building.
20. **Q: LLM Call 1 output** -> **A:** Becomes the context for LLM Call 2.

---

## Cheat Sheet
*   **Prompt Chaining:** Task -> Sub-task 1 -> Sub-task 2 -> Final Result.
*   **Key Pros:** Debugging (find bugs faster), Modularity (fix parts easily), Cost (use cheap models for easy steps).
*   **Developer Rule:** Use `f-strings` for variables and `time.sleep()` for API stability.
*   **Concept:** ReAct = AI decides; Chaining = You decide.
*   **Resume Flow:** Extract Resume -> Extract JD -> Match -> Score -> Action (Email/Call).
*   **Tip:** If an LLM fails, don't just rewrite—check the intermediate outputs first!.