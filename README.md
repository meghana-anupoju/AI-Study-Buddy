AI Study Buddy – Multi-Agent AI Tutor (Google ADK + Gemini)

AI Study Buddy is a multi-agent AI tutor built using Google ADK and Gemini.
It helps students learn programming and computer science concepts through clear explanations, quizzes, feedback, and study guidance — all inside a Google Colab notebook.

This project demonstrates how multiple specialized agents can collaborate to create a personalized, interactive learning experience.

 1. Problem

Students learning computer science often face challenges such as:

Difficulty understanding core concepts (e.g., recursion, Big-O notation)

Lack of personalized explanations based on their level

No integrated quizzes or instant feedback

Insufficient guidance on what to study next

No system that remembers their session progress

Learning becomes fragmented and inefficient, causing confusion and slow progress.

AI Study Buddy aims to solve these challenges using a structured, multi-agent approach.

 2. Solution

AI Study Buddy provides an end-to-end learning experience by combining four coordinated agents:

1. Concept Tutor Agent

Explains CS/programming concepts step-by-step, using examples and analogies.
Automatically generates short summaries that can be saved.

2. Quiz Agent

Creates quizzes on demand and evaluates the student’s answers.
Gives scores, explanations, and corrective feedback.

3. Study Coach Agent

Acts like a mentor.
Offers learning strategies, motivation, and next recommended topics.

4. Orchestrator Agent (AI Study Buddy)

The central controller.
Interprets user intent and routes tasks to the correct agent via AgentTools.
Uses a custom tool to save notes for later review.

Custom Tool — save_note(topic, summary)

Stores summarized notes in a Python dictionary for easy review at the end of the session.

Session Memory

The system uses InMemorySessionService to remember conversation progress within a study session.

This creates a complete learning cycle:
Explain → Quiz → Evaluate → Guide → Save Notes

 3. Architecture
System Diagram
User
  ↓
AI Study Buddy (Orchestrator Agent)
    ↓ Intent detection
    ├── Concept Tutor Agent
    ├── Quiz Agent
    ├── Study Coach Agent
    └── save_note() custom tool
         ↓
    study_notes dictionary

Conversation Memory:
 InMemorySessionService → preserves session context
  
Model:
 Gemini (gemini-2.5-flash-lite)

Key Components

Root Agent (ai_study_buddy)
Manages conversation flow and agent routing.

Three Sub-Agents
Each handles a specific part of the learning experience.

Custom Tool
Stores topic summaries for revision.

Session Service
Maintains memory for the entire study session.

⚙️ 4. Setup Instructions
Step 1 — Open the Notebook

Upload ai_tutor_app.ipynb to Google Colab
or click “Open in Colab” if the badge is added.

Step 2 — Add Your Gemini API Key

In Colab:

Runtime → RunTime Secrets → Add new secret


Secret name: GOOGLE_API_KEY
Secret value: your Gemini API key from Google AI Studio.

The notebook loads it via:

os.environ["GOOGLE_API_KEY"] = userdata.get("GOOGLE_API_KEY")

Step 3 — Install Dependencies

Run the first install cell:

!pip install -q -U google-adk google-genai

Step 4 — Run the Notebook

Execute cells sequentially to:

Load the model

Initialize all agents

Configure memory

Start interacting with the tutor

 5. Usage
Start a conversation
await chat("Explain Big O notation with an example.")

Ask for a quiz
await chat("Quiz me on Big O notation.")

Evaluate answers
await chat("My answers: 1) B 2) A 3) C.")

Get study guidance
await chat("What should I study next?")

Review saved notes
study_notes

6. Diagrams and Images


Architecture diagram

                         ┌─────────────────────────────┐
                         │         User Input          │
                         └──────────────┬──────────────┘
                                        │
                                        ▼
                       ┌──────────────────────────────────────┐
                       │      AI Study Buddy (Orchestrator)   │
                       │  - Detects intent                    │
                       │  - Routes to correct agent           │
                       │  - Manages conversation flow         │
                       └───────┬──────────────┬──────────────┘
                               │              │
                               │              │
         ┌─────────────────────┘              └──────────────────────┐
         ▼                                                            ▼
┌───────────────────────┐                                 ┌────────────────────────┐
│   Concept Tutor Agent │                                 │     Quiz Agent        │
│ - Step-by-step expl.  │                                 │ - Generates quizzes   │
│ - Examples & analogies│                                 │ - Evaluates answers   │
│ - Creates summaries   │                                 │ - Feedback + scoring  │
└───────────┬───────────┘                                 └───────────┬────────────┘
            │                                                          │
            ▼                                                          ▼
┌────────────────────────────┐                           ┌────────────────────────────┐
│  save_note() Custom Tool   │                           │    Study Coach Agent       │
│ - Stores topic summaries   │                           │ - Motivation & guidance    │
│ - Maintains study notes    │                           │ - Recommends next topics   │
└───────────┬───────────────┘                           └────────────┬──────────────┘
            │                                                          │
            └──────────────┬──────────────────────────────────────────┘
                           ▼
            ┌────────────────────────────────────┐
            │     InMemorySessionService         │
            │ - Session memory + context         │
            │ - Stores conversation events       │
            └────────────────────────────────────┘


 7. Key Features Highlight

Multi-agent orchestration using Google ADK

Custom tool integration for saving notes

Session memory via InMemorySessionService

Interactive tutoring flow

Clear, modular, reproducible code

Lightweight and fast using Gemini flash models

Runs entirely in Colab (zero deployment needed)

 8. Future Enhancements

Deploy using Vertex AI Agent Engine

Add long-term memory using vector storage

Build a web UI (Gradio / Streamlit)

Add voice-mode tutoring

Integrate syllabus-based RAG

Convert into a Telegram/WhatsApp tutor

 9. License

This project can be shared and modified freely under the MIT License.


 10. Contributions

Open to suggestions, improvements, or extensions!
Feel free to open a pull request or create an issue.
