# AI Roommate Matching

StayMate uses a sophisticated **Hybrid Matching Engine** that combines deterministic rules with probabilistic AI scoring to find the compatible roommates.

## 🧠 Hybrid Logic Explained

The matching process happens in two stages:

### Stage 1: Hard Filters (The "Must-Haves")
Before invoking the AI, the system filters out incompatible candidates to save resources and ensure basic compatibility.

-   **Location**: Must be within the target city/area (Fuzzy matching).
-   **Budget**: Budget ranges must overlap.
    -   *Logic*: `Candidate.max >= My.min` AND `Candidate.min <= My.max`
-   **Gender Preference**: Must match strict gender requirements (if set).

### Stage 2: AI Scoring (The "Vibe Check")
Candidates passing Stage 1 are sent to the **AI Engine** (Ollama).

The AI evaluates soft factors:
1.  **Lifestyle**: Smoking, Drinking, Pets, Guests.
2.  **Habits**: Cleanliness Levels, Sleep Schedules.
3.  **Personality**: Bio text analysis, Interests overlap.

## 📊 Match Score Algorithm

The final **Compatibility Score (0-100)** is a weighted aggregate:

| Component | Weight | Source |
|-----------|--------|--------|
| **Core Essentials** | 40% | Location & Budget overlap |
| **Lifestyle Habits** | 30% | Smoking, Pets, Alcohol, Guests |
| **Daily Routine** | 30% | Cleanliness, Sleep Schedule |

> **Note**: The AI also generates a *qualitative summary* (e.g., "You match well because you both are early risers and love pets") which is displayed on the frontend card.

## 🤖 Ollama Integration

We use **Llama 3** (via Ollama) running locally or on a dedicated inference server.

### Prompt Structure
The system constructs a structured prompt injecting two profiles:

```text
You are an expert roommate matcher. Analyze these profiles:

Profile A (Me): ... [Structured Data] ...
Profile B (Candidate): ... [Structured Data] ...

Output JSON ONLY:
{
  "score": number (0-100),
  "strengths": ["string"],
  "concerns": ["string"],
  "summary": "1 sentence explanation..."
}
```

### Safety & Fallbacks
-   **JSON Enforcement**: The prompt strictly requests JSON.
-   **Fallback Logic**: If AI fails or times out, the system falls back to a deterministic rule-based score (0-100) to ensure the UI never breaks.
