# PRD → HTML/CSS Prototype
## Step-by-Step Playbook with AI Prompt Templates

**Audience:** Product Managers
**Tools:** Claude.ai · v0.dev · GitHub Copilot · VS Code · Netlify

---

## Overview & Philosophy

This playbook converts a Product Requirements Document (PRD) into a clickable HTML/CSS prototype using free or widely available AI tools. It follows a 6-step workflow, with exact prompt templates at each stage.

**Key principle:** AI tools are most effective when given structured, specific input. Each step in this guide is designed to produce a clean handoff to the next step.

---

## Tool Summary

| Tool | Purpose & Where to Access |
|---|---|
| Claude.ai (free) | Parse PRD, extract screens/flows, generate full HTML pages |
| v0.dev by Vercel (free) | Fast UI generation from text — no setup required |
| GitHub Copilot | In-IDE code generation and iteration (VS Code) |
| VS Code (free) | Edit, assemble, and link prototype files locally |
| Netlify Drop (free) | One-click hosting to share prototype with stakeholders |
| Figma (free tier) | Optional: wireframe validation before coding |

> ⚠️ **Security:** Never paste customer data, real credentials, or proprietary architecture into public AI tools. Use placeholder/dummy data only.

---

## Step 1 — Extract & Structure Requirements from PRD
**Tool: Claude.ai or M365 Copilot Chat**

### Goal
Convert PRD narrative into a structured screen inventory. This becomes your master input for all subsequent steps.

### Instructions
- Open Claude.ai (claude.ai) or M365 Copilot Chat
- Upload your PRD as a PDF, or paste the relevant sections
- Run the prompts below in sequence

---

### 📝 Prompt 1.1 — Screen Inventory

```
You are a senior product manager analyzing a PRD. Extract and list every distinct 
UI screen or page mentioned or implied. For each screen, provide:
- Screen name
- Primary user goal for this screen
- Key UI components (e.g., form, table, modal, nav bar)
- Input actions the user can take
- Output/result shown to the user

Format as a numbered list. Be exhaustive — include empty states, error states, 
and confirmation screens if implied.
```

---

### 📝 Prompt 1.2 — User Flow Mapping

```
Based on the same PRD, map the primary user flow (happy path) as a numbered 
sequence of steps. Format:
Step 1: [Screen Name] → User action → [Next Screen Name]
Step 2: ...

Then list 2-3 critical edge cases or error flows that the prototype should cover.
```

---

### 📝 Prompt 1.3 — Scope Decision

```
Given the screen inventory and user flows above, recommend the minimal set of 
screens needed to validate the core value proposition of this product. 
Prioritize by: (1) user-facing, (2) critical path, (3) differentiating features. 
Output a shortlist of maximum 5 screens for the prototype.
```

**✅ Output from Step 1:** A numbered list of 3–5 screens with components and a clear user flow.

---

## Step 2 — Create a Prototype Brief
**Tool: Claude.ai or M365 Copilot**

### Goal
Produce a tight, AI-ready brief document that you will reuse across all subsequent code generation prompts. This prevents repetition and ensures consistency.

---

### 📝 Prompt 2.1 — Generate Prototype Brief

```
Using the screen inventory and user flow we defined, create a Prototype Brief 
in the following format:

PRODUCT NAME: [name]
ONE-LINE DESCRIPTION: [what it does]
TARGET USER: [persona]
DESIGN STYLE: Clean, professional SaaS UI. Use a blue/white color scheme. 
              No frameworks required beyond Bootstrap 5 CDN.

SCREENS IN SCOPE:
1. [Screen Name]: [2-sentence description of purpose and key components]
2. [Screen Name]: ...
(repeat for each screen)

PRIMARY USER FLOW:
[paste flow from Step 1]

GLOBAL COMPONENTS (appear on all screens):
- Top navigation bar with: logo, nav links [list them], user avatar
- Footer with: copyright

DUMMY DATA TO USE:
- Company name: Acme Corp
- User name: Alex Johnson
- [Add any other relevant dummy data]
```

> 📌 **Save this brief.** You will paste it at the start of every prompt in Steps 3 and 4.

---

## Step 3 — Generate HTML/CSS for Each Screen
**Tool: v0.dev (fastest) OR Claude.ai OR GitHub Copilot**

### Option A — v0.dev (Recommended for Speed, No Setup)
- Go to v0.dev in your browser
- Paste your Prototype Brief, then add the screen-specific prompt below
- v0.dev generates a React component — click 'Export' → copy the HTML output
- Repeat for each screen

### 📝 Prompt 3A — v0.dev Screen Generation

```
[PASTE YOUR FULL PROTOTYPE BRIEF HERE]

Now generate a complete, styled UI for SCREEN: [Screen Name].

Requirements:
- Clean, professional SaaS design
- Fully self-contained HTML with inline CSS or Tailwind classes
- Include realistic dummy data (no lorem ipsum)
- Show the primary user action clearly (e.g., a prominent CTA button)
- Include a visible navigation bar matching the global components above
- Mobile-responsive layout
```

---

### Option B — Claude.ai (Best for Full Single-File HTML)
- Start a new chat on Claude.ai
- Paste your brief, then the prompt below
- Claude will return a complete self-contained HTML file — copy and save as `[screen-name].html`

### 📝 Prompt 3B — Claude.ai Full HTML Page

```
[PASTE YOUR FULL PROTOTYPE BRIEF HERE]

Generate a complete, self-contained HTML file for SCREEN: [Screen Name].

Requirements:
- Single HTML file with all CSS in a <style> block in the <head>
- Use Bootstrap 5 via CDN for layout (no local files needed)
- Include realistic dummy data — no placeholder text
- Navigation bar must match the Global Components defined above
- All links between screens should use: href="[screen-name].html"
- The page should look like a real product, not a wireframe
- Add a subtle hover state on all interactive elements
- Include an empty state or loading state if this screen has a data table/list
```

---

### Option C — GitHub Copilot in VS Code
- Create a new file: `index.html` in VS Code
- Open Copilot Chat (`Ctrl+Shift+I`)
- Paste the prompt below into Copilot Chat

### 📝 Prompt 3C — GitHub Copilot Chat

```
I am building an HTML/CSS prototype. Here is the context:

[PASTE YOUR FULL PROTOTYPE BRIEF HERE]

Generate a complete HTML file for SCREEN: [Screen Name].
- Use Bootstrap 5 CDN
- All CSS inline in <style> tag
- Realistic dummy data
- Navigation links: href="[other-screen].html"
- Professional SaaS appearance
```

**✅ Output from Step 3:** One `.html` file per screen, saved locally.

---

## Step 4 — Assemble & Link Screens
**Tool: VS Code (free)**

### Goal
Combine individual screen files into a navigable multi-page prototype.

### Instructions
- Create a project folder, e.g.: `/my-prototype/`
- Place all `.html` files in this folder
- Rename your first/landing screen to `index.html`
- Ensure all navigation links in each file use consistent filenames

---

### 📝 Prompt 4.1 — Fix Navigation Links (Claude.ai or Copilot)

```
I have the following HTML prototype screens:
- index.html (Dashboard)
- screen2.html (User Profile)  
- screen3.html (Settings)
[adjust to match your files]

Review this HTML file and update all <a href> links in the navigation bar so they 
correctly link to the filenames above. Return the complete corrected file.

[PASTE HTML FILE CONTENT]
```

---

### 📝 Prompt 4.2 — Add Active State to Navigation

```
Update the navigation bar in this HTML file so the current page's nav link 
appears visually highlighted (active state). The current page is: [Screen Name].
Use Bootstrap's 'active' class. Return the updated nav bar HTML only.
```

**✅ Output from Step 4:** A local folder with linked `.html` files you can open in any browser.

---

## Step 5 — Polish & Iterate
**Tool: Claude.ai or GitHub Copilot**

### Goal
Refine visual quality, fix inconsistencies, and address gaps before sharing with stakeholders.

---

### 📝 Prompt 5.1 — Visual Consistency Check

```
Review these two HTML files and identify any visual inconsistencies:
- Different font sizes, colors, or spacing
- Navigation bar differences
- Button style variations
List the differences and provide corrected CSS for the inconsistent elements.

[PASTE FILE 1]
---
[PASTE FILE 2]
```

---

### 📝 Prompt 5.2 — Mobile Responsiveness

```
Review this HTML file and improve mobile responsiveness:
- Stack columns vertically on screens < 768px
- Make the navigation bar collapse into a hamburger menu on mobile (use Bootstrap)
- Ensure font sizes are readable on mobile (minimum 16px body text)
Return the complete updated file.

[PASTE HTML FILE]
```

---

### 📝 Prompt 5.3 — Add Micro-Interactions

```
Add the following micro-interactions to improve prototype realism:
- Hover effects on all buttons (slight color darkening)
- Hover on table rows (light blue highlight)
- Smooth fade-in on page load (CSS animation)
- Loading spinner placeholder on the data table
Use only CSS and vanilla JavaScript (no external libraries).

[PASTE HTML FILE]
```

---

### 📝 Prompt 5.4 — Accessibility Quick Check

```
Review this HTML for basic accessibility issues:
- Missing alt text on images
- Buttons without descriptive labels
- Low color contrast text
- Form inputs without labels
List issues found and provide the corrected HTML snippets.
```

---

## Step 6 — Host & Share with Stakeholders
**Tool: Netlify Drop or GitHub Pages (free)**

### Option A — Netlify Drop (Easiest, No Account Needed)
- Go to app.netlify.com/drop
- Drag and drop your entire prototype folder
- Get a shareable URL instantly (e.g., `https://random-name.netlify.app`)
- Share URL with stakeholders — no login required to view

### Option B — GitHub Pages (Recommended for Version Control)
- Create a new public GitHub repository
- Upload all `.html` files to the repo root
- Go to Settings → Pages → Source: Deploy from branch (main)
- URL will be: `https://[your-username].github.io/[repo-name]/`

> ⚠️ **Stakeholder Communication:** Set expectations clearly — this is a visual prototype for concept validation, not a production build. All data is dummy/synthetic.

---

### 📝 Prompt 6.1 — Generate Stakeholder Handoff Note (Claude.ai)

```
Write a brief 3-paragraph stakeholder note to accompany a prototype review. 
Include:
- What the prototype is and what it represents
- What feedback you are seeking (specific decisions to validate)
- What the prototype does NOT cover (out of scope, no real backend, etc.)

Context: [2-sentence description of your product and what stage you're at]
```

**✅ Output from Step 6:** A live URL ready to share for stakeholder review.

---

## Quick Reference: Full Workflow at a Glance

| Step | Action & Key Output |
|---|---|
| 1 — Extract Requirements | Use Claude.ai to extract screens, flows, and components from PRD → Screen Inventory |
| 2 — Create Brief | Generate a reusable Prototype Brief with dummy data and global components |
| 3 — Generate HTML | Use v0.dev or Claude.ai to create one `.html` file per screen |
| 4 — Assemble & Link | Organize files in VS Code, fix navigation links between screens |
| 5 — Polish | Fix inconsistencies, add responsiveness and micro-interactions |
| 6 — Host & Share | Deploy to Netlify Drop or GitHub Pages, share URL with stakeholders |

---

## Risk Register

| Risk | Mitigation |
|---|---|
| AI hallucinates UI components not in PRD | Always cross-check generated screens against your Step 1 screen inventory |
| Prototype mistaken for production-ready code | Add a visible 'PROTOTYPE' watermark and communicate scope in stakeholder note |
| Sensitive PRD content pasted into public AI tools | Sanitize PRD before pasting — replace real names, data, pricing with placeholders |
| Inconsistent styling across screens | Maintain a single shared CSS block — paste into each file or extract to `style.css` |
| Scope creep during iteration | Lock screen scope after Step 2 — defer new screens to v2 of the prototype |
| Stakeholder assumes full functionality | Always demo in context, explain what is clickable vs. decorative |

---

## Appendix: Prompt Cheat Sheet

| Step & Prompt ID | One-Line Summary |
|---|---|
| 1.1 — Screen Inventory | Extract all screens and components from PRD |
| 1.2 — User Flow Mapping | Map happy path and edge case flows |
| 1.3 — Scope Decision | Identify minimal 3–5 screen prototype scope |
| 2.1 — Prototype Brief | Generate reusable structured brief for all AI prompts |
| 3A — v0.dev Screen | Generate styled screen UI with brief context |
| 3B — Claude HTML Page | Generate full self-contained HTML file per screen |
| 3C — Copilot Chat | Generate HTML via GitHub Copilot Chat in VS Code |
| 4.1 — Fix Nav Links | Correct all href links to match actual filenames |
| 4.2 — Active Nav State | Highlight current page in navigation bar |
| 5.1 — Consistency Check | Compare two files and fix visual inconsistencies |
| 5.2 — Mobile Responsive | Add responsive layout and mobile nav |
| 5.3 — Micro-Interactions | Add hover effects, animations, loading states |
| 5.4 — Accessibility Check | Identify and fix basic a11y issues |
| 6.1 — Stakeholder Note | Generate context-setting note for prototype reviewers |

---

*Iteration is expected — prototype quality improves with each feedback cycle.*
