# AI Document Generator — n8n LLM Chain
### Multi-Stage Document Generation with Quality Control

A production-ready n8n workflow that transforms a topic into a
polished, professional document through a multi-stage LLM pipeline
with automated quality control and conditional routing.

---

## Pipeline Architecture

```
Chat Input (topic)
        ↓
┌─────────────────────────────────────┐
│         GENERATE OUTLINE            │
│  Structured numbered sections       │
│  with subsections and descriptions  │
│  Output wrapped in <outline> tags   │
└──────────────┬──────────────────────┘
               ↓
┌─────────────────────────────────────┐
│       CHECK OUTLINE CRITERIA        │
│  Evaluates against 5 quality gates  │
│  Returns PASS or FAIL + explanation │
└──────────────┬──────────────────────┘
               ↓
        ┌──────┴──────┐
        │             │
      PASS           FAIL
        │             │
        ↓             ↓
┌────────────┐  ┌───────────────┐
│  EXPAND    │  │  EDIT FIELDS  │
│  OUTLINE   │  │  Return FAIL  │
│  SECTIONS  │  │  + output     │
└─────┬──────┘  └───────────────┘
      ↓
┌─────────────────────────────────────┐
│      REFINE AND POLISH DOCUMENT     │
│  Transitions, intro, conclusion     │
│  Professional academic tone         │
└──────────────┬──────────────────────┘
               ↓
     Final Polished Document
```

---

## Quality Gate — 5 Criteria

The workflow evaluates every outline against these requirements
before proceeding to document expansion:

1. Must have at least 3 main sections
2. Must include both benefits and challenges
3. Must address ethical considerations
4. Must include future perspectives
5. Must have clear logical flow between sections

If the outline fails any criterion the workflow stops and
returns a FAIL response with explanation — preventing
low-quality outlines from being expanded.

---

## Key Features

- Multi-stage LLM pipeline — outline, evaluate, expand, polish
- Automated quality gate with PASS/FAIL routing
- XML-structured prompts for reliable LLM parsing
- Conditional branching — only expands approved outlines
- OpenRouter model routing — swap models without rebuilding
- Three specialized LLM chains with focused system prompts
- Failure handling — returns failed output with explanation

---

## Tech Stack

| Layer | Technology |
|---|---|
| Workflow Engine | n8n |
| Model Routing | OpenRouter |
| LLM | GPT-4.1 (openai/gpt-4.1) |
| Chain Type | LangChain LLM Chain |
| Trigger | n8n Chat Trigger |

---

## Why This Architecture

**Single responsibility per node**
Each LLM chain does one focused task — generate, evaluate,
expand, or polish. This produces more consistent, higher
quality output than asking one LLM call to do everything.

**Quality gate before expansion**
Checking the outline before expanding prevents wasting tokens
on a poor structure. It mirrors professional document review
workflows where an outline is approved before writing begins.

**Conditional routing**
The If node routes PASS outlines to expansion and FAIL
outlines to a failure response — making the workflow
self-aware and reliable.

**XML tag delimiters**
Wrapping outline and criteria in XML tags gives the LLM
clear boundaries for what to evaluate — improving parsing
accuracy and evaluation consistency.

---

## Setup & Import

1. Install and run n8n:
```bash
npm install -g n8n
n8n start
```

2. Open n8n at `http://localhost:5678`

3. Import the workflow:
   - Click **Workflows** → **Import from file**
   - Upload `workflows/document_generator_v2.json`

4. Configure credentials:
   - Click **Credentials** → **Add Credential**
   - Select **OpenRouter API**
   - Add your OpenRouter API key
   - Get your key at openrouter.ai/keys

5. Activate the workflow and open the chat interface

---

## Usage

1. Open the n8n chat interface
2. Enter a topic — example:
```
AI in Healthcare: Benefits, Challenges, and Future Directions
```
3. The workflow will:
   - Generate a structured outline
   - Evaluate it against 5 criteria
   - If PASS — expand and polish into a full document
   - If FAIL — return the failure with explanation

---

## Example Output

**Input:** "AI in Healthcare"

**Stage 1 — Generated Outline:**
```
<outline>
1. Introduction to AI in Healthcare
   a. Definition and scope
   b. Current state of adoption
2. Benefits of AI in Clinical Practice
   a. Diagnostic accuracy improvements
   b. Operational efficiency gains
3. Challenges and Limitations
   a. Data privacy concerns
   b. Implementation barriers
4. Ethical Considerations
   a. Bias in AI systems
   b. Patient consent and transparency
5. Future Perspectives
   a. Emerging technologies
   b. Policy recommendations
</outline>
```

**Stage 2 — Quality Check:**
```
PASS — Outline meets all 5 criteria. Contains 5 main
sections, addresses benefits and challenges, includes
ethical considerations in section 4, covers future
perspectives in section 5, and maintains logical flow.
```

**Stage 3 — Final Document:**
A fully expanded, polished professional document with
introduction, detailed sections, smooth transitions,
and conclusion.

---

## Customization

**Change the target audience**
Update the Style Guide in the Generate Outline node:
```
Target audience: [your audience here]
```

**Change the quality criteria**
Update the criteria list in Check Outline Criteria node
to match your document requirements.

**Change the LLM model**
Update the OpenRouter Chat Model nodes to use any
model available on OpenRouter — no other changes needed.

**Add more quality criteria**
Add numbered items to the criteria section in the
Check Outline Criteria node.

---

## Files Included

| File | Description |
|---|---|
| [workflows/document_generator_v2.json](workflows/document_generator_v2.json) | Fixed XML tags and typos |
| [changelog.md](changelog.md) | Full version history |

---

## Related Repos

| Repo | Pattern | Framework |
|---|---|---|
| [ai-agent-team-supervisor-pattern](https://github.com/Paul-Orlando/ai-agent-team-supervisor-pattern) | Supervisor Pattern | Flowise AgentFlows V2/V3 |
| [ai-multi-agent-content-pipeline](https://github.com/Paul-Orlando/ai-multi-agent-content-pipeline) | Sequential Agents | Flowise Sequential |
| [data-analysis-agent-app](https://github.com/Paul-Orlando/data-analysis-agent-app) | Interactive Agent | Next.js + FastAPI |
| [deep-research-agent](https://github.com/Paul-Orlando/deep-research-agent) | Research App | Claude Code + Next.js |
| [ai-food-chatbot-agent](https://github.com/Paul-Orlando/ai-food-chatbot-agent) | Agentic RAG | Flowise + Postgres |

---

## Author

Paul Orlando
Creative Technologist | AI Agent Developer | Data Analytics
🌐 [paulforlando.com](https://www.paulforlando.com)
💼 [LinkedIn](https://www.linkedin.com/in/paul-orlando-7841b5154)
🐙 [GitHub](https://github.com/Paul-Orlando)

---

## License

MIT License
