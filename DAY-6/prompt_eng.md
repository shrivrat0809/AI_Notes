# Lecture Notes: Foundations of Prompt Engineering (Building Secure and Stable LLMs)

## Overview
This lecture demystifies **Prompt Engineering**, explaining that it is not a complex subject requiring a four-year degree but rather a set of practical techniques rooted in common sense. The primary goal is to transform vague prompts into "engineered" ones to ensure **Large Language Model (LLM)** outputs are stable, predictable, and secure for production use. By incorporating six specific elements—**Role, Task, Constraints, Output Format, Examples (Shotting), and Fallback**—developers can prevent LLMs from giving inconsistent answers or responding to inappropriate user queries. The lecture emphasizes that prompt engineering is essential because LLMs are **non-deterministic**, meaning they can provide different answers to the same question.

---

## Main Topics

### 1. Understanding Prompt Engineering
*   **Definition**: The process of refining prompts to be clear and specific so that the LLM provides high-quality, relevant results.
*   **Explanation**: It involves moving away from vague instructions (like "handle this") toward structured frameworks that guide the model's behavior.
*   **Why it is important**: Without it, LLM behavior is unpredictable, making it difficult to use in professional applications where a specific code module expects a specific type of answer.
*   **Key concepts**: Moving from **vague** to **structured** communication.
*   **Examples**: Improving a customer support bot so it doesn't try to solve a user's relationship problems or give out private employee information.

### 2. The Problem of Non-Determinism
*   **Definition**: A characteristic where an input does not always produce the exact same output every time it is processed.
*   **Explanation**: Unlike a calculator, where $2+2$ always equals $4$, an LLM might explain a concept differently across three different chat tabs even if the question is identical.
*   **Why it is important**: In production, code modules often depend on the LLM's output. If the format or content changes randomly, the downstream code will "break".
*   **Common Mistakes**: Assuming an LLM will always behave the same way just because it worked once during testing.

### 3. The 6 Techniques for Secure and Stable Prompts
To make a prompt "engineered," you must include these six elements:

#### **I. Role**
*   **Definition**: Telling the LLM "who" it is in the context of the task.
*   **Explanation**: You define a domain or a specific responsibility.
*   **Important Tip**: Assigning a role like "Senior Engineer" is good for context, but calling it a "Genius" does **not** actually increase the model's intelligence or capabilities.

#### **II. Task**
*   **Definition**: The specific action the LLM needs to perform.
*   **Explanation**: Providing a clear, unambiguous action verb, such as "classify," "summarize," or "solve".

#### **III. Constraints**
*   **Definition**: Setting boundaries for the LLM's response.
*   **Explanation**: Limiting the model to specific categories or rules. For example, telling a bot it can only classify issues into "Billing," "Technical," or "Return".
*   **Importance**: It prevents the model from "hallucinating" its own categories or dealing with issues it wasn't designed for.

#### **IV. Output Format**
*   **Definition**: Defining the structure of the final answer.
*   **Explanation**: Specifying if the result should be one word, a JSON object, or a bulleted list.
*   **Importance**: Ensures that the code receiving the LLM's answer can parse it without errors.

#### **V. Zero/One/Few Shot (Examples)**
*   **Definition**: Providing real-world examples within the prompt.
*   **Explanation**: 
    *   **Zero Shot**: No examples provided.
    *   **One Shot**: One example provided.
    *   **Few Shots**: Multiple examples provided.
*   **Importance**: LLMs learn patterns quickly; providing examples helps them mimic the desired style and accuracy.

#### **VI. Fallback**
*   **Definition**: A safety instruction for when the LLM encounters something outside its defined scope.
*   **Explanation**: Telling the LLM what to do if a query doesn't fit any category (e.g., "If the issue is unrelated, print 'Other'").
*   **Importance**: Protects the system from crashing when users ask irrelevant or malicious questions (e.g., asking a food bot for Python code).

---

## Important Definitions
*   **Deterministic**: An operation that always results in the same output for the same input (e.g., a calculator).
*   **Non-Deterministic**: An operation where the output varies even if the input remains the same (e.g., an LLM).
*   **Vague Prompt**: A prompt that is ambiguous or lacks clear instructions, leading to unstable results.
*   **Happy Path**: A scenario where everything goes exactly as planned in software execution.
*   **Murphy’s Law**: The adage that "anything that can go wrong, will go wrong," used here to emphasize the need for fallbacks in AI.

---

## Important Formulas / Syntax / Rules
*   **The 6-Step Framework Rule**: A secure prompt = Role + Task + Constraints + Output Format + Examples + Fallback.
*   **LLM Function Syntax (Python)**:
    ```python
    def llm_answer(prompt):
        message = {"role": "user", "content": prompt}
        response = client.chat.completions.create(
            model=model,
            messages=[message]
        )
        return response.choices.message.content
    ```

---

## Tables

### Comparison: Deterministic vs. Non-Deterministic Systems
| Feature | Deterministic (e.g., Calculator) | Non-Deterministic (e.g., LLM) |
| :--- | :--- | :--- |
| **Input: 2 + 2** | Always 4 | Usually 4, but the *way* it says it can change |
| **Consistency** | 100% predictable | Highly unpredictable/unstable |
| **Production Use** | Easy to integrate into code | Requires Prompt Engineering for stability |
| **User Interaction** | Rigid | Conversational and flexible |

---

## Diagrams

### The Prompt Engineering Process
```text
[Vague User Input] -> [LLM with BAD Prompt] -> [Unstable/Long Output]
                               |
                               v
[Vague User Input] -> [LLM with ENGINEERED Prompt] -> [Stable/Fixed Output]
                       (Role + Task + Constraints +
                        Format + Examples + Fallback)
```


---

## Key Takeaways
1.  **Prompt Engineering is Common Sense**: It is the art of being specific so the LLM doesn't have to guess.
2.  **Stability is Key for Production**: LLMs are non-deterministic; prompt engineering is the only way to make them stable enough for real apps.
3.  **Roles define Context, not Power**: Giving a model a role sets its "vibe" and domain but doesn't make it smarter than its underlying architecture.
4.  **Always have a Fallback**: Users will always try to "break" your bot; tell the model exactly how to handle out-of-scope questions.

---

## Revision Notes (One-Page)
*   **What is PE?**: Making prompts better for better results.
*   **Why PE?**: LLMs give different answers each time (non-deterministic). Production code needs stable, predictable results.
*   **Security**: Prevents bots (like Zomato or Domino’s) from answering inappropriate questions or leaking info.
*   **The 6 Pillars**:
    1.  **Role**: "You are a customer support agent".
    2.  **Task**: "Classify the user complaint".
    3.  **Constraints**: "Only use these 3 categories: Billing, Tech, Return".
    4.  **Format**: "Reply with only ONE word".
    5.  **Shotting**: Provide examples (One-shot, Few-shot).
    6.  **Fallback**: "If it doesn't fit, say 'Other'".
*   **Bad Prompts**: Vague instructions like "handle this" lead to "messy" responses.

---

## Interview / Viva Questions
1.  **What does it mean that an LLM is non-deterministic?** It means the model can produce different outputs for the same input every time it's run.
2.  **Why is a 'Role' important in a prompt?** It sets the domain and responsibility, helping the model adopt the right tone and context.
3.  **Does calling an LLM a 'Genius' make it perform better?** No, role-play doesn't increase the model's actual intelligence or capabilities.
4.  **What is the 'Happy Path' in software engineering?** It is the ideal scenario where the user provides the exact type of input the system expects.
5.  **How do constraints help in classification tasks?** They force the LLM to choose from a fixed list of categories, preventing it from inventing its own.
6.  **What is the difference between Zero-shot and One-shot prompting?** Zero-shot gives no examples; One-shot provides one example for the model to follow.
7.  **Why is a fallback necessary for production bots?** To handle unexpected or irrelevant user queries (like relationship advice for a food bot) safely.
8.  **What is a 'Bad Prompt'?** A prompt that is vague, lacks instructions, and results in unstable formatting.
9.  **Why can't we just use 'Role' to make a free model act like a paid one?** Because the role doesn't change the underlying model architecture or intelligence.
10. **How does output formatting affect downstream code?** If the format is consistent (e.g., one word), the code can easily use that word to route the issue to the correct team.

---

## Practice Questions

### Easy
1. Define Prompt Engineering in your own words.
2. List the 6 elements of an engineered prompt.
3. What happens if you ask a calculator $2+2$ ten times?
4. What happens if you ask an LLM the same question ten times?
5. Give an example of a "Role."
6. What is the "Task" in a classification prompt?
7. What is an example of an "Output Format"?
8. Why shouldn't a Zomato bot answer relationship questions?
9. Is Prompt Engineering a four-year degree course?
10. What is a "Vague" prompt?

### Medium
1. Explain how "Constraints" improve LLM stability.
2. Compare a calculator and an LLM using the term "deterministic."
3. Describe a scenario where a missing "Fallback" could cause a production issue.
4. Why does the instructor say "Role" does not increase intelligence?
5. Write a "One-shot" prompt for summarizing news.
6. How does "Output Format" prevent code from "breaking"?
7. Explain Murphy’s Law in the context of AI Agents.
8. What is the difference between "Domain" and "Responsibility" in a Role?
9. Why is simple common sense equated to Prompt Engineering?
10. How does a prompt change when you add a "Task" to a "Role"?

### Challenging
1. Design a prompt for a Banking Bot that includes all 6 techniques mentioned in the lecture.
2. Analyze why an LLM might classify "My girlfriend left me" as a "Billing" issue if no fallback is provided.
3. Create a Python function that demonstrates the transition from a "Bad Prompt" to an "Engineered Prompt."
4. How would you handle a user trying to get Python code from a restaurant's chatbot?
5. Explain the technical danger of "punctuation" and "extra stories" in an LLM's response when used in a software pipeline.

---

## Flashcards
1. **Q: Deterministic** -> **A:** Same input = Always same output.
2. **Q: Non-deterministic** -> **A:** Same input = Different potential outputs.
3. **Q: 6 Pillars of PE** -> **A:** Role, Task, Constraints, Format, Shotting, Fallback.
4. **Q: Role** -> **A:** Defines "Who" the LLM is (e.g., Support Assistant).
5. **Q: Task** -> **A:** Defines "What" the LLM should do (e.g., Classify).
6. **Q: Constraints** -> **A:** Boundaries for the LLM (e.g., "Use only 3 categories").
7. **Q: Output Format** -> **A:** Structure of the answer (e.g., "One word only").
8. **Q: Zero-shot** -> **A:** Providing no examples in the prompt.
9. **Q: One-shot** -> **A:** Providing one example in the prompt.
10. **Q: Few-shot** -> **A:** Providing multiple examples in the prompt.
11. **Q: Fallback** -> **A:** Instruction for handling out-of-scope inputs.
12. **Q: Bad Prompt** -> **A:** Vague, lacks structure, unstable output.
13. **Q: Production Issue** -> **A:** When LLM output breaks downstream code.
14. **Q: "Genius" Role** -> **A:** Does NOT increase model intelligence.
15. **Q: Classification** -> **A:** Assigning an input to a specific category.
16. **Q: Ambiguity** -> **A:** When a prompt is "vague" and open to interpretation.
17. **Q: Happy Path** -> **A:** The expected flow of a program.
18. **Q: Security Issue** -> **A:** e.g., A bot giving out an employee's phone number.
19. **Q: Prompt Engineering Goal** -> **A:** Stability and security.
20. **Q: Common Sense** -> **A:** The core of good prompt engineering.

---

## Cheat Sheet
*   **Goal**: Make LLMs predictable for production.
*   **Core Logic**: Be specific. Don't let the LLM guess.
*   **Non-Determinism**: LLMs $\neq$ Calculators. They vary.
*   **The Prompt Structure**:
    1.  **Role**: Domain + Responsibility.
    2.  **Task**: Clear Action.
    3.  **Constraints**: Boundaries/Categories.
    4.  **Format**: Exact Structure (e.g., JSON, 1-word).
    5.  **Examples**: Teach by showing.
    6.  **Fallback**: Handle the "unplanned".
*   **Security**: Use Fallbacks to prevent "misuse" (e.g., users asking for code from a support bot).
*   **Mantra**: Role $\neq$ Intelligence. Specificity = Stability.