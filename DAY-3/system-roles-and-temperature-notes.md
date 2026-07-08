# Ep 03: System Role and Temperature Settings | Free AI Engineer Course

## Overview

This lecture from the **Free AI Engineer Course** explores two fundamental parameters in Large Language Models (LLMs): **System Roles** and **Temperature** [3, 4]. The instructor uses real-world, humorous analogies—such as expressing romantic feelings to different individuals or asking various friends for exam advice—to explain how these parameters alter an LLM's responses [1, 2]. The lesson covers the theoretical significance of these concepts, their practical implementation in Python using the **Groq API** and the **UV package manager**, and how they are applied in corporate settings [10, 11, 19, 20]. By the end of the lecture, students understand how to customize an AI's professional persona and control its creative randomness [10, 11, 17, 18].

---

## Main Topics

### 1. The Core Concept: How Context and Personality Shape Responses
* **Definition**: An introductory concept demonstrating that a single input can yield vastly different outputs depending on either the **recipient's role** (relationship context) or the **recipient's personality** (nature/disposition) [1, 2].
* **Explanation**: In human communication, context dictates behavior. The lecturer explains this using two distinct scenarios:
  1. **The Role/Relationship Scenario**: If you say "I love you" to your girlfriend, you expect an affectionate response ("I love you too") [1]. However, saying the exact same phrase to an office manager, colleague, or teacher can lead to severe professional consequences, such as a **POSH** (Prevention of Sexual Harassment) complaint, official warnings, or a police FIR (First Information Report) [1, 25]. The message is identical, but the outcome depends entirely on the relationship roles [1, 3].
  2. **The Personality Scenario**: If you ask different friends "How do I get good marks in exams?", their answers will vary based on who they are [2]. A straightforward, safe-playing friend will say "study hard" [2, 3]. A mischievous or playful ("chulbaaz") friend might say "make cheat sheets and cheat" [2]. A highly reckless, chaotic friend might say "kidnap the examiner and demand marks" [2]. The question is identical, but the advice is shaped by their core personality and willingness to take risks [2, 3].
* **Why it is Important**: This concept directly maps to how LLMs process information [4]. The first scenario maps to **System Roles** (defining the AI's relationship to the user) [4]. The second scenario maps to **Temperature** (defining the AI's core personality and creative riskiness) [4].
* **Key Concepts**:
  * **Role-based context**: The social/professional boundaries of a conversation [3].
  * **Personality-based variation**: The level of creativity or risk an individual (or AI) takes when generating an answer [3, 4].
* **Examples Mentioned**:
  * Saying "I love you" to a girlfriend vs. a manager/teacher [1].
  * Asking a studious friend vs. a mischievous friend vs. a reckless friend for exam tips [2].
* **Common Mistakes or Misconceptions**:
  * *Misconception*: People often think that if they send the same message to an LLM, it will always respond in the same way, or that LLMs cannot adapt to professional contexts. In reality, setting roles and adjusting parameters completely changes the output behavior [1, 6, 7].

---

### 2. System Role
* **Definition**: A configuration parameter that defines the specific **persona**, **post**, or **relationship context** that the LLM must adopt when interacting with the user [4, 5, 11].
* **Explanation**: In LLM message structures, messages are categorized by "roles" [4]. While the **User Role** represents the prompt written by you, and the **Assistant Role** represents the AI's response, the **System Role** provides overarching rules or instructions to the model [4, 5]. By sending a system message before the user message, we hardcode the AI's identity [6]. For example, telling it "You are my girlfriend" makes it respond affectionately, while "You are my manager" forces it to maintain strict corporate boundaries [6, 7, 24, 25].
* **Why it is Important**: Without a system role, the LLM will give a generic, uncustomized response [5, 6, 9]. In the real world, system roles allow companies to deploy specialised **AI agents** with different job functions (e.g., developers, architects, testers) using the exact same underlying LLM [8, 10, 11].
* **Key Concepts**:
  * **Message Roles**: Three types: **User** (default user input), **Assistant** (the AI's output), and **System** (instructions on how to behave) [4, 5].
  * **Hardcoding Identity**: Overriding generic behavior to enforce a specific persona [6].
  * **Multi-Agent Systems**: Deploying multiple clients of the same LLM, each assigned a different organizational post [10, 11].
* **Step-by-Step Process (Usage in Python)**:
  1. Define a system message dictionary: `message_system = {"role": "system", "content": "Your Persona Here"}` [24].
  2. Define a user message dictionary: `message_user = {"role": "user", "content": "Your Prompt Here"}` [24].
  3. Arrange them in a list, placing the system message **first**: `messages = [message_system, message_user]` [24].
  4. Pass this list to the LLM's chat completion API [23, 26].
* **Examples Mentioned**:
  * **Personal**: Changing the system persona from "You are my loving girlfriend" to "You are my strict office colleague who also happens to be my manager" [24, 25].
  * **Corporate**: An SDE (Software Development Engineer) at a tech company like Akamai using an LLM subscription (such as Anthropic's Claude) [7, 8]. The company creates three agents using system roles [11]:
    * **Senior Level Architect**: Focuses on high-level system design, security, maintainability, reliability, and partition tolerance [8, 10].
    * **Junior Developer**: Focuses on writing code, solving specific bugs (like off-by-one array indexing causing segmentation faults) [8, 10].
    * **Tester**: Focuses strictly on testing the software [11].
* **Advantages and Disadvantages**:
  * *Advantages*: Standardises response behavior, ensures professional compliance, and enables division of labor among multiple AI agents [7, 11].
  * *Disadvantages*: If not set correctly or if instructions are passed in the wrong order (e.g., user message before system message), the AI will fail to adopt the persona properly [24].
* **Common Mistakes or Misconceptions**:
  * *Mistake*: Placing the system role message *after* the user message in the list. The AI will read the user's message without context, violating the intended flow [24].
* **Tips Shared by the Instructor**: Always pass the system message first in your Python message list so the LLM is fully aware of its identity before reading your question [24].

---

### 3. Temperature
* **Definition**: A hyperparameter that controls the **randomness**, **creativity**, and **predictability** of an LLM's generated output [11, 12, 17].
* **Explanation**: LLMs are not "truth-telling machines" that fetch direct databases (like Google Search) [12, 13]. Instead, they are **prediction machines** that guess the next most logical word based on patterns they have learned [12, 13].
  * *Analogy*: A toddler who only knows the days of the week [13]. When you say "Sunday, Monday", she predicts "Tuesday" because she has memorised the sequence, not because she "understands" time [13].
  * **Temperature = 0** tells the model to play safe and choose the highest-probability, most obvious word (giving "Tuesday") [12, 14].
  * **As Temperature increases (up to 2)**, the model starts taking creative risks [12, 14]. The toddler might suggest a rhyming word like "Andey" (Hindi for eggs) instead of the obvious "Tuesday" [14].
* **Why it is Important**: Different real-world applications require different levels of creativity [17]. A medical diagnostic assistant must be strictly factual (Temperature near 0), whereas a creative writer or brand-name generator needs random, अतरंगा (eccentric/catchy) suggestions (Temperature closer to 2) [17, 18].
* **Key Concepts**:
  * **Prediction Engine**: How LLMs generate tokens based on probabilities [12, 13].
  * **Degree of Randomness**: Controlling how far the model strays from the safest mathematical prediction [12, 17].
  * **Creative Range**: Standard APIs (like Groq) support values from `0` to `2`, where `0` is highly predictable and `2` is highly creative/random [12].
* **Examples Mentioned**:
  * **Naming a Food Delivery App**:
    * `t = 0` (Safe/Obvious): "Khana Khajana", "Mantu ka Dhaba" [15].
    * `t = 1` (Creative/Balanced): "Zomato" (made up, but rhymes with "Tomato") [15, 16].
    * `t = 2` (Highly Random/Catchy): "Swiggy" (completely random word with no dictionary meaning) [15, 16].
  * **Naming a Clothing Brand**:
    * `t = 0` (Safe): "Westra" (derived from the Hindi word "Vastra") [28].
    * `t = 2` (Creative): "Westo" (a play on the English word "vest") [28].
  * **Use Cases**:
    * **Doctor AI Agent**: Requires a temperature of `0` to ensure strict, safe, and factual diagnoses of symptoms [17].
    * **Media Story Teller AI**: Requires a high temperature to generate interesting and unique horror stories [17, 18].
* **Advantages and Disadvantages**:
  * *Advantages*: Allows developers to tune the AI for either factual precision or creative brainstorming [17, 18].
  * *Disadvantages*: Setting the temperature too high can lead to nonsensical outputs; setting it too low can make creative outputs boring and repetitive [14, 18].
* **Common Mistakes or Misconceptions**:
  * *Mistake*: Setting temperature to `3` or higher. This will raise an API validation error [27].
  * *Misconception*: Believing that high temperature makes the AI "smarter" or "criminal" [12]. It simply increases the mathematical randomness of word choices [17].
* **Tips Shared by the Instructor**: Keep your temperature values strictly within the `0.0` to `2.0` range when working with modern LLM APIs to avoid errors [27].

---

### 4. Technical Environment Setup and Dependency Management
* **Definition**: The practical workflow of setting up a clean Python workspace, managing virtual environments, and installing packages using the modern **UV** tool [19, 20].
* **Explanation**: The instructor stresses the importance of isolating project dependencies [19, 20]. Instead of using standard `pip`, he utilizes `uv` (a fast Python package installer and resolver) [19, 22].
* **Why it is Important**: Keeps production code modular and prevents package version conflicts between different project days [19, 20].
* **Key Concepts**:
  * **UV Package Manager**: A blazingly fast alternative to `pip` [22].
  * **Virtual Environment (venv)**: An isolated folder containing its own Python binary and packages [19, 20].
* **Step-by-Step Process (Terminal Workflow)**:
  1. Navigate back to the week folder [19]:
     ```bash
     cd ..
     ```
     *(Note: Spoken as "cd dash dash" in the Hindi video transcript [19])*
  2. Initialise a new Day 2 project [19]:
     ```bash
     uv init day2
     ```
     This automatically creates a folder called `day2` with basic project files [19].
  3. Copy your `.env` configuration file from the previous day's folder and paste it into the new `day2` folder (using GUI right-click or a standard file copy command) [19, 20].
  4. Create a virtual environment using Python 3.11 [20]:
     ```bash
     uv venv --python 3.11
     ```
     *(Crucial: Ensure you use the double dashes `--` before "python" to avoid syntax errors [20]).*
  5. Activate the virtual environment [20].
  6. Add the required dependencies to the project [21]:
     ```bash
     uv add python-dotenv
     uv add groq
     ```
* **Common Mistakes**:
  * Forgetting the double dashes `--` when specifying Python version in `uv venv` [20].
  * Writing the same package name twice in a single command, causing syntax/resolution failures [21].
  * Attempting to run the script before adding `groq` and `python-dotenv` packages, resulting in `No module named groq` [23].
* **Tips Shared by the Instructor**: 90% of development errors are simple **human errors** [22]. Do not panic when an installation fails—read the terminal logs carefully and verify your command syntax [22].

---

## Important Definitions

* **System Role**: A parameter that instructs an LLM on its identity, background context, professional post, and behavioral rules for the duration of a chat session [4, 5, 11].
* **User Role**: The default message role representing instructions, queries, or prompts sent directly by the human developer [4, 5].
* **Assistant Role**: The message role representing the generated outputs and answers returned by the AI model [5].
* **Temperature**: A numerical setting (ranging from `0` to `2`) that controls how predictable or creatively random the model's next-token predictions are [11, 12].
* **Prediction Machine**: A term describing LLMs, indicating that they do not dynamically "know" facts but mathematically predict high-probability sequences of text based on training data [12, 13].
* **UV**: A modern, high-performance package and environment manager for Python used to initialise projects, create virtual environments, and add dependencies rapidly [19, 20, 22].
* **Virtual Environment (venv)**: An isolated environment that allows developers to install specific libraries for a project without affecting the global Python system [19, 20].
* **POSH**: Prevention of Sexual Harassment. Mentioned in the lecture as a corporate regulatory framework that would be violated if one expressed romantic sentiments inappropriately in a workspace [1, 25].

---

## Important Formulas / Syntax / Rules

### 1. System Role Message Structure (JSON/Dict)
```python
message_system = {
    "role": "system",
    "content": "You are a Senior Level Architect"
}
```
* **Rule**: The system dictionary must be declared and appended to the messages array **before** the user dictionary [24].

### 2. Message List Sequencing
```python
messages = [message_system, message_user]
```
* **Rule**: Correct chronological order is mandatory: System context $\rightarrow$ User query [24].

### 3. API Call Syntax with Temperature
```python
response = client.chat.completions.create(
    model="llama3-8b-8192",  # Or any specified Groq model [23]
    messages=messages,
    temperature=1.0          # Accepts values from 0.0 to 2.0 [26, 27]
)
```
* **Rule**: `temperature` must be a float/integer between `0` and `2`. Passing values greater than `2` (e.g., `3`) causes an API validation error [27].

### 4. UV Project & Env Commands
* Initialise project:
  ```bash
  uv init day2
  ```
* Create Virtual Environment:
  ```bash
  uv venv --python 3.11
  ```
* Add packages:
  ```bash
  uv add python-dotenv groq
  ```

---

## Tables

### Comparison: System Role vs. Temperature

| Feature | System Role | Temperature |
| :--- | :--- | :--- |
| **Core Function** | Defines **who** the AI is (identity, relationship, post, background rules) [4, 5, 11]. | Determines **how** creatively or randomly the AI speaks (personality, predictability) [11, 12]. |
| **Analogy** | **Who** you are talking to: your Girlfriend, Manager, Teacher, or Daughter [1, 3]. | **What type** of friend you ask: conservative (safe) vs. chaotic (risky/unpredictable) [2]. |
| **Parameter Type** | Message Object with role `system` and custom string content [5, 6]. | Floating-point numerical parameter passed directly in the API creation call [26]. |
| **Standard Range** | Any descriptive text prompt instructing behavior [6]. | Typically `0.0` to `2.0` (where `0` is safest and `2` is most random) [11, 12]. |
| **Real-World Use Case** | Deploying specialised agents (Architect vs. Junior Developer vs. Tester) [10, 11]. | Matching domain style: Doctor AI Agent (t=0) vs. Horror Story Writer (t=2) [17]. |
| **Error Triggers** | Sending it after user messages, causing context mismatch [24]. | Passing values outside the supported model range (e.g., `temperature=3`) [27]. |

---

## Diagrams

### 1. Conceptual Flow: Context & Personality
```
                       [ USER PROMPT: "I Love You" ] [1, 5]
                                     |
                +--------------------+--------------------+
                |                                         |
       [ SOCIAL ROLE ] [4]                           [ PERSONALITY ] [4]
       (System Role)                                  (Temperature)
                |                                         |
     +----------+----------+                   +----------+----------+
     |                     |                   |                     |
[ Girlfriend ] [6]    [ Manager ] [7]       [ Safe (t=0) ] [12] [ Creative (t=2) ] [12]
     |                     |                   |                     |
 "I love you too" [6] "HR/POSH Violation" [7]  "Safe/Predictable" [12] "Wild/Unpredictable" [12]
```

### 2. File and Virtual Environment Setup Flow
```
week1/ [19]
├── day1/ (Previous Workspace) [19]
└── day2/ (Created via 'uv init day2') [19]
    ├── .env (Copied manually from day1) [19, 20]
    ├── system_temperature.py (Main Script) [20]
    └── .venv/ (Created via 'uv venv --python 3.11') [20]
        ├── bin/ [20]
        └── lib/ (Contains isolated 'groq' and 'python-dotenv' libraries) [21, 23]
```

### 3. API Execution Sequence
```
[ message_system ] + [ message_user ]  --->  Pass to client.chat.completions.create(..., temperature=X) [23, 24, 26]
       (Index 0)            (Index 1)
                                                       |
                                                       v
                                            [ Groq Inference Engine ] [23]
                                                       |
                                                       v
                                            [ Output Text Generation ] [23]
```

---

## Key Takeaways

1. **LLMs are Context-Driven**: The identical user prompt will yield fundamentally different responses depending on the social boundaries established by the **System Role** [1, 7].
2. **System Roles Enable Multi-Agent Workflows**: By programmatically defining system instructions, developers can create distinct worker profiles (Architects, Developers, Testers) out of a single general-purpose AI model [10, 11].
3. **LLMs are Prediction Machines, Not Databases**: A language model generates text by predicting high-probability words in a sequence, much like a toddler reciting memorised days of the week [12, 13].
4. **Temperature Tunes Risk-Taking**: Low temperature ($0$) enforces factual, conservative, and predictable text, while high temperature ($2$) allows creative, erratic, and uniquely named outputs [12, 14].
5. **Errors are Mostly Human**: In software engineering and AI scripting, 90% of issues stem from syntax, typos, or missing virtual environment installations rather than system bugs [22].

---

## Revision Notes

### 1. Social Context & System Roles
* **The Analogy**: Saying "I love you" works for a girlfriend but gets you fired by a manager [1]. Context is everything [3].
* **System Role**: Defined using `{"role": "system", "content": "..."}` [6]. It must be placed at the beginning of the messages array [24].
* **Corporate Value**: Assigns corporate posts to LLM clients, ensuring that a "Senior Architect" agent discusses security and partition tolerance while a "Junior Developer" solves specific code bugs [10, 11].

### 2. Creativity & Temperature Settings
* **Prediction Nature**: LLMs mathematically guess the next word [12, 13]. They do not query static facts like search engines [12].
* **Temperature Parameters**: Standard models accept values between `0` and `2` [11, 12].
* **Low Temp ($t=0$)**: Predictable, safe [12]. Best for doctors, factual lookup engines, and strict debuggers [17].
* **High Temp ($t=2$)**: Highly random, creative [12, 18]. Best for brainstorming, fiction writing, and brand naming [17, 18].
* **Application Example**: Asking for food brand names gives "Khana Khajana" at $t=0$, "Zomato" at $t=1$, and "Swiggy" at $t=2$ [15, 16].

### 3. Quick CLI Commands (UV Ecosystem)
* Run `uv init <project_name>` to create a new folder structure [19].
* Ensure double dashes in `uv venv --python 3.11` to set up Python correctly [20].
* Always add dependencies (`uv add groq python-dotenv`) inside the active virtual environment before running code to prevent "No module named" errors [21, 23].

---

## Interview / Viva Questions

### Q1: What is the main structural difference between System, User, and Assistant roles in an LLM API?
**Answer**: The **User** role represents messages sent by the human developer [4, 5]. The **Assistant** role represents response messages generated by the LLM itself [5]. The **System** role represents top-level developer instructions that hardcode the LLM's identity, behavior, and professional guidelines for the session [4, 5, 11].

### Q2: Why must the System message be appended before the User message in the API message list?
**Answer**: Appending the system message first ensures that the LLM processes its assigned identity and behavioral constraints *before* it reads and responds to the user's query [24]. Passing it afterward violates conversation flow and fails to set the identity [24].

### Q3: Explain why LLMs are termed "prediction machines" rather than "truth-telling machines" using the lecturer's days of the week analogy.
**Answer**: Unlike search engines that lookup and retrieve exact facts, LLMs use mathematical probabilities to guess the next logical word [12, 13]. Just like a young child who is taught "Sunday, Monday" and predicts "Tuesday" without actually understanding calendars, LLMs generate text based on sequence likelihood rather than genuine comprehension of truth [13].

### Q4: What happens if you pass a temperature value of 3.0 to a standard LLM API like Groq?
**Answer**: Modern LLM APIs generally accept temperature parameters strictly in the range of `0.0` to `2.0` [12]. Passing a value of `3.0` will violate validation rules and trigger an API validation error, halting execution [27].

### Q5: In a corporate scenario, how does the System Role solve the issue of "generalised LLM responses" when a company purchases a subscription?
**Answer**: It allows the company to assign realistic organizational posts to different LLM instances [11]. Instead of a generic engine, the company can create an "Architect Client" that evaluates security, a "Developer Client" that resolves bugs, and a "Tester Client" focused on quality assurance [10, 11].

### Q6: If you are building an AI diagnostic tool for a medical clinic, what temperature would you select and why?
**Answer**: You should select a temperature of `0.0` [17]. Medical assistants require high precision, factual consistency, and zero creative risk-taking or guesswork when evaluating symptoms and identifying illnesses [17].

### Q7: Explain how the brand name "Swiggy" represents a high temperature output compared to "Khana Khajana".
**Answer**: "Khana Khajana" is a literal, predictable name with direct dictionary references to food, typical of a temperature `0` setting [15, 16]. "Swiggy" is a completely random, abstract word with no direct meaning, demonstrating the extreme creative risk and out-of-the-box generation characteristic of temperature `2` [15, 16].

### Q8: What error will occur if you run a script importing `groq` inside a freshly created UV project without installing dependencies?
**Answer**: Python will raise a `ModuleNotFoundError: No module named 'groq'` [23]. To resolve this, you must run `uv add groq` while inside the active virtual environment [23].

### Q9: How can you verify in your terminal that your UV virtual environment has been activated successfully?
**Answer**: Once activated, the name of your project folder (e.g., `(day2)`) will appear as a prefix at the far left of your terminal prompt line [20].

### Q10: What is the instructor's general advice regarding encountering errors during code setup?
**Answer**: 90% of development errors are human errors, such as typos or syntax oversights [22]. Developers must maintain patience, read the error tracebacks carefully, and examine exactly what commands they executed instead of assuming the system is broken [22].

---

## Practice Questions

### Easy Questions (10)
1. Write down the command to initialise a new Python project named `day2` using UV [19].
2. Name the three primary message roles used in LLM completions [4, 5].
3. What is the default role of the message containing a human user's prompt [4, 5]?
4. What is the default role under which ChatGPT or Claude returns its answers [5]?
5. True or False: Setting a System Role allows you to make an LLM simulate a specific persona [6].
6. What is the standard range of temperature settings used in the Groq API [12]?
7. What is the default temperature setting of an LLM when no value is explicitly passed [12, 26]?
8. Name the file that contains API keys and environment variables that must be copied between project directories [19, 20].
9. How do you navigate back one directory level in the terminal [19]?
10. True or False: LLMs check a live, factual database of truth for every query, much like Google [12].

### Medium Questions (10)
11. Write a Python dictionary representing a System Role instructing an AI to act as a professional accountant [24].
12. Explain what a "segmentation fault" bug is, and which LLM role (Architect or Junior Developer) would typically handle it in the instructor's corporate example [10].
13. Describe the output differences when asking an LLM for clothing brand names at temperature `0` vs. temperature `2` [28].
14. Explain what happens to the mathematical predictability of token selection as the temperature parameter increases from `0` to `2` [12].
15. Why does the instructor comment out the raw response print statement (`print(response)`) during testing [23]?
16. How does a virtual environment (`.venv`) help prevent library conflicts in a multi-stage software project [19, 20]?
17. Correct the syntax error in the following shell command: `uv venv python 3.11` [20].
18. Detail the girlfriend vs. manager analogy and connect it to LLM development [1, 24, 25].
19. Why does temperature `1` suggest "Zomato" as a food app name instead of "Khana Khajana" or "Swiggy" [15, 16]?
20. Why does the lecturer suggest that a company like Akamai cannot function with a single, general-purpose LLM without system roles [7, 9, 10]?

### Challenging Questions (5)
21. Write a complete Python script that initialises a Groq client, loads environment variables, defines a system role of a "Strict Editor," sets a user prompt of "Review my article," and uses a temperature of `0.5` to generate a response [23, 24, 26].
22. Suppose an LLM's system role is set to "You are a professional chef," but the messages list is written as:
    `messages = [{"role": "user", "content": "How do I boil eggs?"}, {"role": "system", "content": "You are a professional chef"}]`
    Analyze why the output may not be presented in a professional chef's persona [24].
23. Contrast the system requirements of a "Senior Level Architect" and a "Junior Developer" as explained in the lecture. What structural properties does the architect care about that the developer does not [8, 10]?
24. Using the toddler "Days of Week" analogy, explain how an LLM handles an out-of-distribution input (like "January, February") under both low and high temperature configurations [13, 14].
25. You are designing an AI agent to write engaging, highly suspenseful horror fiction. Formulate a system role and select a specific temperature value, justifying your choices using arguments from the lecture [17, 18].

---

## Flashcards

**FC 1**
* **Question**: What are the three standard roles in an LLM chat exchange [4, 5]?
* **Answer**: User, Assistant, and System.

**FC 2**
* **Question**: What is the primary purpose of the System Role [4, 5]?
* **Answer**: To establish the AI's identity, professional post, behavioral guidelines, and conversational context.

**FC 3**
* **Question**: What range of values does the temperature parameter accept in modern APIs [12]?
* **Answer**: `0.0` to `2.0`.

**FC 4**
* **Question**: What setting represents the default "safe play" temperature [12, 26]?
* **Answer**: Temperature `0.0`.

**FC 5**
* **Question**: How does an LLM behave at temperature `0.0` [12]?
* **Answer**: It behaves predictably, choosing the highest probability token/prediction and avoiding creative risk-taking.

**FC 6**
* **Question**: How does an LLM behave at temperature `2.0` [12, 14]?
* **Answer**: It becomes highly creative, unpredictable, and random in its word choices.

**FC 7**
* **Question**: Why are LLMs compared to prediction machines rather than database search engines [12]?
* **Answer**: Because they use statistical probabilities to guess the next word in a sequence instead of looking up verified factual databases.

**FC 8**
* **Question**: What command is used to initialise a new workspace folder in the UV ecosystem [19]?
* **Answer**: `uv init <folder_name>`.

**FC 9**
* **Question**: What command sets up an isolated Python virtual environment using Python 3.11 [20]?
* **Answer**: `uv venv --python 3.11`.

**FC 10**
* **Question**: What command adds the `groq` SDK package to your current virtual environment [23]?
* **Answer**: `uv add groq`.

**FC 11**
* **Question**: In the days of the week analogy, what does the toddler predict after hearing "Sunday, Monday" [13]?
* **Answer**: She predicts "Tuesday" based on memorised sequence probability, not actual comprehension.

**FC 12**
* **Question**: In the clothing brand demo, what names were suggested at temperature `0` vs. `2` [28]?
* **Answer**: "Westra" at temperature `0` (safe, Hindi wordplay) and "Westo" at temperature `2` (creative, English wordplay).

**FC 13**
* **Question**: In the food delivery brand demo, what was the temperature `1` suggestion [15]?
* **Answer**: "Zomato" (creative but balanced, as it rhymes with "Tomato").

**FC 14**
* **Question**: What temperature setting is appropriate for a Medical Diagnosis AI agent [17]?
* **Answer**: Temperature `0.0`, as it requires factual precision and no random guesswork.

**FC 15**
* **Question**: What temperature setting is appropriate for a Media Storyteller AI agent [17]?
* **Answer**: A high temperature (approaching `2.0`), as creative randomness is necessary to construct unique narratives.

**FC 16**
* **Question**: If you forget to place double dashes in the UV virtual environment setup, what command was typed [20]?
* **Answer**: `uv venv python 3.11` (which is a syntax error).

**FC 17**
* **Question**: How can you tell if your terminal is currently using your virtual environment [20]?
* **Answer**: The name of the environment folder (e.g. `(day2)`) will be displayed at the start of your command line.

**FC 18**
* **Question**: What happens to your program if you try to run it without installing packages first [23]?
* **Answer**: It throws a `ModuleNotFoundError` because the isolated environment lacks those libraries.

**FC 19**
* **Question**: What is the corporate risk of exposing a general-purpose LLM without System Roles [9]?
* **Answer**: The AI provides general-purpose, non-specialised answers that lack professional boundaries, guidelines, or targeted roles.

**FC 20**
* **Question**: According to the lecturer, what percentage of programming errors are human-caused [22]?
* **Answer**: Approximately 90% of errors are human mistakes, like typos or syntax oversights.

---

## Cheat Sheet

### Essential Cheat Sheet

* **System Role**: Defines "Who" the AI is [4, 5]. Must be passed as the **first** element in the message list [24].
  * *Girlfriend Role*: Affectionate response [6].
  * *Manager Role*: Strict corporate response (prevents HR/POSH complaints) [7, 25].
  * *Architect Role*: High-level system layout, security, maintainability, reliability, partition tolerance [8, 10].
  * *Developer Role*: Direct code bug-solving [8, 10].

* **Temperature**: Adjusts "How" the AI responds (predictability & creative risk) [11, 12].
  * **Range**: `0.0` to `2.0` [12].
  * **Value = 0**: Safe, factual, highly predictable [12, 17].
  * **Value = 1**: Moderately creative, balances patterns [15, 16].
  * **Value = 2**: Wildly creative, highly random, 어तरंगा (eccentric) [15, 18].
  * **Value = 3**: Triggers model API validation error [27].

* **Quick Terminal Workflow** [19, 20, 23]:
  ```bash
  cd ..                         # Go to parent folder [19]
  uv init day2                  # Initialise project [19]
  # Copy .env into day2 folder manually [19, 20]
  uv venv --python 3.11         # Setup virtual environment [20]
  source .venv/bin/activate     # Activate environment [20]
  uv add python-dotenv groq     # Add dependencies [21, 23]
  python system_temperature.py  # Run script [20]
  ```
