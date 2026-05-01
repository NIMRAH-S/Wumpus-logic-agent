# 🤖 Wumpus Logic Agent

A **web-based Knowledge-Based Agent** that navigates a dynamic Wumpus World grid using **Propositional Logic** and **Resolution Refutation** to deduce safe cells — without any hardcoded rules or machine learning.

## 🔗 Links
- **Live Demo:** [[your-vercel-url.vercel.app](https://wumpus-logic-agent-eta.vercel.app/)](#)
- **LinkedIn Post:** [[linkedin.com/in/yourprofile](https://www.linkedin.com/posts/nimrah-shahid-b634b51ba_artificialintelligence-propositionallogic-activity-7456022535378272256-0VEL?utm_source=share&utm_medium=member_desktop&rcm=ACoAADL5szsB7C6m7cWEnz7OxXDimHtvTnBsyVg)](#)

---

## 🧠 How It Works

The agent operates using a real inference engine built from scratch:

1. **TELL** — When the agent visits a cell, it encodes percepts into CNF clauses and adds them to the Knowledge Base. For example, if there is no Breeze at (2,1), it adds `¬P_1_1 ∧ ¬P_2_2 ∧ ¬P_3_1` to the KB.

2. **ASK** — Before moving to any unvisited adjacent cell, the agent queries the KB: *"Is this cell safe?"* It does this via **Resolution Refutation** — it negates the goal (assumes there IS a pit), adds that clause, then repeatedly resolves clause pairs until it derives the empty clause `⊥` (contradiction), proving the cell is safe.

3. **Navigate** — The agent only moves to cells proven safe by the KB. If no safe move exists, it halts rather than risk death — rational behavior.

---

## 🗂️ Project Structure
wumpus-logic-agent/
├── index.html       # Complete single-file app (HTML + CSS + JS)
└── README.md

---

## ⚙️ Features

- **Dynamic Grid:** Configure any grid from 3×3 up to 7×7
- **Dynamic Hazards:** Pits and Wumpus are randomly placed each episode
- **Inference Engine:** Full CNF Resolution Refutation implemented in vanilla JS
- **Live KB Display:** Watch CNF clauses being added in real time
- **Metrics Dashboard:** Tracks inference steps, moves, safe cells, and KB size
- **Step / Auto Mode:** Step through the agent's decisions one at a time or watch it run automatically
- **Reveal Map:** Toggle to see ground truth (pit/wumpus locations)

---

## 🚀 How to Run Locally

Just open `index.html` in any modern browser. No installation needed.

```bash
git clone https://github.com/yourusername/wumpus-logic-agent.git
cd wumpus-logic-agent
open index.html
```

---

## 📐 Logic & CNF Conversion

The biconditional `B_r,c ⟺ (P_adj1 ∨ P_adj2 ∨ ...)` is converted to CNF as:

- `(¬B_r,c ∨ P_adj1 ∨ P_adj2 ∨ ...)` — if breeze then some adjacent pit
- `(¬P_adj1 ∨ B_r,c)`, `(¬P_adj2 ∨ B_r,c)` — if adjacent pit then breeze

The **Resolution Refutation loop** then works as follows:
1. Take all KB clauses + `¬query`
2. Pick any two clauses containing complementary literals
3. Resolve them → produce a new clause
4. If empty clause found → query is **entailed** ✅
5. If no new clauses can be produced → query is **not entailed** ❌

---

## 🏛️ Course

**AI 2002 – Artificial Intelligence** | Spring 2026  
National University of Computer & Emerging Sciences, Chiniot-Faisalabad Campus
