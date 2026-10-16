---
name: grill-developer-calibration
description: Evaluates user technical expertise through an adaptive multi-choice assessment to calibrate response complexity, explanations, and skill execution. Updates CONTEXT.md with the user's skill profile.
---

<what-to-do>

Conduct an adaptive assessment to establish the user's technical background and developer capability. 

Inform the user upfront:
- That you are going to do this assessment to establish their developer level and communication style so that in future you can always communicate with them in a context they will understand and a style they will relate to.
- They can type `skip` or `quit` at any time to start building immediately.
- The question are multiple choice but they are free to add as much detail as they desire.
- Answering at least 10 to 15 questions progressively fine-tunes the agent's communication style, code abstraction, and technical depth.
- Get their consent to proceed before moving onto the assessment.

Assessment procedure:
1. Ask questions strictly one at a time.
2. When the user answers a question, immediately write or update the `## Developer Context Profile` section in `CONTEXT.md` by using the answer to systematically evaluate developer metrics and assign a primary developer archetype.
3. Dynamically select the next question based on prior responses to drill into relevant domain nuances. 
4. Repeat steps 1-3 until the user says `quit` or `stop` or something similar to indicate that they have had enough. If the user has answered 10 or more questions, periodically remind them that they can stop at any time.

</what-to-do>

<supporting-info>

## Scope & File Resolution Order

Before starting or updating the profile, resolve the `CONTEXT.md` location in this exact order:

1. **Global Scope (Preferred)**: Check for global agent configuration directories in the home folder:
   - `~/.claude/CONTEXT.md`
   - `~/.pi/CONTEXT.md`
   - `~/.config/agent/CONTEXT.md`
   - Or the active agent's designated global configuration directory in `~/.config/` or `~/`
   
   *(If the global directory exists but `CONTEXT.md` does not, create it lazily there).*

2. **Local Scope (Fallback)**: If no global agent context directory is accessible, use or create `CONTEXT.md` in the current project root (`./CONTEXT.md`).

### Context Pre-Check
If a `## Developer Context Profile` section already exists at the resolved path, read it first:
- Briefly state the current saved profile to the user: *"I see you are currently profiled as [Archetype]."*
- Ask if they would like to re-calibrate, fine-tune, or proceed with their existing profile.

## Domain Awareness & Context Storage

```markdown
## Developer Context Profile

- **Assessed Archetype**: [Absolute Beginner | CMS / No-Code Specialist | Cross-Domain Specialist | HTML/CSS/JS Traditionalist | Modern Frontend Dev | Backend/Infra Specialist | Full-Stack Web Dev | Veteran Polyglot]
- **Specializations & Languages**: [e.g., Swift/iOS, Go/Microservices, WordPress/PHP, None]
- **Terminal & Tooling Comfort**: [None | Basic CLI | Advanced / Shell / Git / CI/CD]
- **Web Stack Technical Depth**: [0-10]
- **Communication Style**: [Analogy-driven | Structural Translation | Direct & Technical | Minimalist High-Velocity Code]
- **Questions Answered**: [X]
```

## How to Adapt Communication Based on Profile

When answering questions or building code across any skill or task, adapt output based on `Assessed Archetype`:

- **Absolute Beginner**: Use analogies, avoid raw CLI commands without step-by-step explanations, and describe file layouts visually.
- **CMS / No-Code Specialist**: Map concepts to visual UI controls they know (e.g., "Think of props as component settings in Webflow").
- **Cross-Domain Specialist**: Map web architectures directly to their native domain equivalents (e.g., for iOS developers: "JSX state works like `@State` in SwiftUI, and `useEffect` behaves like `.task`").
- **HTML/CSS/JS Traditionalist**: Highlight the shift from manual DOM manipulation to declarative state frameworks.
- **Modern Frontend / Backend / Full-Stack / Veteran Polyglot**: Provide direct code diffs, concise architecture notes, and eliminate step-by-step prose unless asked.

## Question Branching Guide

### Question 1: Macro Domain & Experience

*Purpose: Establish broad domain placement.*

> **Which of the following best describes your background with software and technology?**
>
> A) Completely new to coding or software development.
>
> B) Experience using site builders, CMS tools, or low-code platforms (e.g., WordPress, Webflow, Shopify, Airtable, Zapier).
>
> C) Experienced developer in non-web domains (e.g., native iOS/Android, C/C++, Embedded, Python Data Science, Machine Learning).
>
> D) Web developer with classic foundation skills (HTML, CSS, vanilla JavaScript, PHP, jQuery).
>
> E) Modern web developer using JavaScript/TypeScript component frameworks or modern backend services.
>
> F) Veteran developer / polyglot with 10+ years of broad multi-language software engineering experience across systems or applications.

### Question 2: LLM Code Explanation

*Purpose: Establish the desired level of understanding .*

> **When you're building something with an LLM, how do you like to work?**
>
> A) Tell it the goal, take the output, paste it in, run it, report errors. Fast and iterative.
>
> B) Ask it to explain the why behind non-obvious choices so I learn, not just ship.
>
> C) Want the code, but also a short structural note on how the pieces fit (architecture-level), not line-by-line prose. 

### Questions 3–6: Nuance & Specialization Expansion

*Branch for Option B (CMS / No-Code):*

> **How do you typically work with platforms like WordPress or Webflow?**
>
> A) Using existing visual themes, builders, and plugins without editing code.
>
> B) Customizing CSS and light HTML snippet modifications within theme editors.
>
> C) Writing custom PHP template files, hooks, or custom database queries.
>
> D) Building headless integrations using REST or GraphQL APIs into CMS backends.

*Branch for Option C (Cross-Domain Specialist):*

> **What is your primary development ecosystem or specialization?**
>
> A) Native iOS development (Swift, SwiftUI, UIKit, Xcode).
>
> B) Native Android development (Kotlin, Jetpack Compose, Android Studio).
>
> C) Systems programming / Game dev / Embedded (C, C++, Rust, Zig, Metal/OpenGL).
>
> D) Machine Learning, Data Engineering, or Scripting (Python, PyTorch, R, Bash).
>
> E) Enterprise backend or desktop applications (Java, C#/.NET, Go).

*Branch for Option D & E (Web Developers):*

> **Which stack or architectural patterns are you most comfortable with?**
>
> A) Classic server-rendered sites (PHP, Rails, Django, classic templates + jQuery).
>
> B) Single-Page Applications (SPAs) with modern frameworks (React, Vue, Svelte, Angular).
>
> C) Full-stack web frameworks (Next.js, Nuxt, Astro, Laravel, Remix).
>
> D) Backend microservices, REST/gRPC/GraphQL APIs, databases, and infrastructure (Node, Go, Python, Docker).

*Branch for Option F (Veteran Polyglot):*

> **How do you prefer to approach learning a new web framework or stack?**
>
> A) Show me an example of architectural mapping to standard patterns (MVC, state flow, lifecycle) and let me inspect the raw code/diffs directly.
>
> B) Provide minimal idiomatic boilerplate and focus on framework-specific quirks or paradigms.
>
> C) Walk through the ecosystem tooling (build steps, bundle options, modern routing) step-by-step.

### Questions 7–15+: Deep-Dive Calibration

* **Terminal/DevOps**: CLI comfort, Git workflows, package managers (`npm`, `pnpm`, `cargo`), environment management.
* **Async & APIs**: Promises, async/await, HTTP status codes, state management, CORS, authentication patterns.
* **Styling & Layout**: Native CSS (Flexbox/Grid), Tailwind, CSS Modules, utility-first styling vs. preprocessors.

## Dynamic Updating

Update the `Developer Context Profile` in `CONTEXT.md` whenever the user demonstrates elevated competence or requests adjustments to explanation depth.

</supporting-info>