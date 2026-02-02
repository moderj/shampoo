# AGENTS.md - Space Super-gun Developer Training Wiki

## Project Overview

This is a **developer training wiki** designed to onboard and train developers to become "Space Super-gun Developers" - highly skilled full-stack developers with expertise in modern development workflows, Node.js, and software design principles.

The wiki follows a **modular learning path structure** where each topic is broken down into digestible modules with clear learning objectives, practical exercises, and estimated completion times.

### Project Structure

```
shampoo.wiki/
├── home.md                    # Landing page with welcome message
├── _sidebar.md               # Navigation index
├── Setup.md                  # Environment setup guide (WSL, VS Code, Docker)
├── Workflow/                 # Development workflow training
│   ├── Workflow.md          # Path introduction & overview
│   ├── Linux.md             # Self-learning module
│   └── Git.md               # Mentor-validated module with project
├── Node/                     # Node.js & JavaScript training
│   ├── Node.md              # Path introduction & overview
│   ├── Javascript.md        # Core JS concepts + exercises
│   ├── Asynchronous-Javascript.md  # Async patterns
│   ├── Call-Of-Duty.md      # Hands-on project
│   ├── TypeScript.md        # Type safety
│   └── Testing-Javascript.md # Testing practices
├── Frontend/                 # Frontend development training
│   ├── Frontend.md          # Path introduction & overview
│   ├── HTML.md              # Structure and semantics
│   ├── CSS.md               # Styling with Flexbox and Grid
│   └── javascript-vanilla.md # Browser-side interactivity
└── Code-Design/              # Software design principles
    └── Code-Design.md       # Curated video resources
```

### Key Characteristics

- **Self-directed learning**: Learners can choose their own resources (videos, docs, tutorials)
- **Progressive difficulty**: Topics range from beginner to expert levels
- **Practical focus**: Includes coding exercises, projects, and real-world scenarios
- **Mentor integration**: Some modules require mentor validation
- **Modular design**: Each path can be completed independently

---

## How to Write Exceptional Training Paths

### 1. Module Structure Template

Every training module should follow this structure:

```markdown
# [Topic Name]

> _Estimation time: X-Y Days_

---

Brief description of what this module covers and why it matters.

**_Learning objectives:_**

At the end of this module, you'll be able to:

- [Specific, measurable outcome 1]
- [Specific, measurable outcome 2]
- [Specific, measurable outcome 3]

---

_Send me back [home](home)_

[[_TOC_]]

---

## Prerequisites

List any required knowledge or completed modules before starting.

## Core Content Sections

### Section 1: [Concept Name]

Explanation + code examples + external resources

### Section 2: [Concept Name]

Continue pattern...

## Practical Exercises

### Exercise 1: [Name]

[Problem description]

// Code example or starter code

**Expected output:**

[What success looks like]

### Exercise 2: [Name]

[More challenging problem]

## Advanced Topics (Optional)

Concepts worth knowing but not required:

- [Advanced concept 1]
- [Advanced concept 2]

## Tools & Resources

- [Tool name](link) - Brief description
- [Resource name](link) - Brief description

## Next steps

[Clear call-to-action linking to next module]
```

### 2. Writing Rules for Exceptional Content

#### A. Learning Objectives (MUST)

- **Be specific and measurable**: "Understand async/await" → "Write async functions that handle multiple concurrent API calls"
- **Use action verbs**: Write, Create, Debug, Implement, Analyze
- **Limit to 3-5 objectives**: Focus on core competencies
- **Align with real-world tasks**: What will they actually do with this knowledge?

#### B. Time Estimates (MUST)

- **Be realistic**: Account for reading, practice, and exercises
- **Provide ranges**: "3-5 Days" acknowledges different learning speeds
- **Include all activities**: Reading + exercises + project work
- **Adjust for difficulty**: Complex topics need more time

#### C. Content Organization (MUST)

- **Progressive disclosure**: Basics → Intermediate → Advanced
- **Concept-then-practice**: Explain, then immediately exercise
- **Code-first examples**: Show working code before explaining theory
- **Multiple learning modalities**: Links to videos, docs, and interactive tutorials

#### D. Practical Exercises (MUST)

- **Start simple**: Build confidence with easy wins
- **Increase difficulty gradually**: Each exercise builds on the last
- **Include real scenarios**: Avoid abstract "foo bar" examples
- **Provide solutions**: Either inline or in a separate file
- **Add stretch goals**: Bonus challenges for fast learners

#### E. Navigation & UX (MUST)

- **Consistent headers**: Use the template structure
- **Table of contents**: Use `[[_TOC_]]` for automatic generation
- **Breadcrumb links**: Always include "Send me back [home](home)"
- **Clear next steps**: End with explicit guidance on what to do next
- **Cross-link related content**: Connect to other modules when relevant

#### F. External Resources (SHOULD)

- **Curate, don't dump**: 3-5 high-quality resources beat 20 mediocre ones
- **Diversify formats**: Mix videos, articles, documentation, and interactive sites
- **Annotate links**: Briefly explain what each resource covers
- **Prefer official docs**: MDN, Node.js docs, framework documentation
- **Include duration**: "(30 minutes)" helps learners plan

#### G. Code Examples (SHOULD)

- **Be copy-paste ready**: Working code that runs without modification
- **Use realistic variable names**: `userProfile` not `obj`
- **Include comments**: Explain the "why" not just the "what"
- **Show expected output**: Demonstrate what success looks like
- **Cover edge cases**: Show how to handle errors and unexpected input

### 3. Module Types

#### Type A: Self-Learning Module

**Characteristics:**
- Learner-driven exploration
- External resource heavy
- No mandatory deliverables
- Optional exercises

**Example:** `Workflow/Linux.md`

**Template additions:**
```markdown
**Learning approach:**
This is a self-learning module. Explore the resources below at your own pace.
There are no mandatory exercises, but we recommend trying the commands as you read.
```

#### Type B: Project-Based Module

**Characteristics:**
- Hands-on coding project
- Specific requirements and acceptance criteria
- Mentor validation required
- Builds portfolio piece

**Example:** `Node/Call-Of-Duty.md`

**Template additions:**
```markdown
## Project Requirements

### Functional Requirements
- [ ] Feature 1 description
- [ ] Feature 2 description

### Technical Requirements
- [ ] Use specific technology/pattern
- [ ] Follow specific convention

### Acceptance Criteria
1. [Specific testable criterion]
2. [Specific testable criterion]

## Submission

Submit your project to your mentor for review via [method].
```

#### Type C: Concept Module

**Characteristics:**
- Deep dive into specific technology/concept
- Mix of theory and practice
- Exercises with solutions
- May include quiz questions

**Example:** `Node/Javascript.md`

**Template additions:**
```markdown
## Concept Check

Test your understanding:

1. [Question about concept]
2. [Question about edge case]

<details>
<summary>Answers</summary>

1. [Explanation]
2. [Explanation]

</details>
```

#### Type D: Resource Collection

**Characteristics:**
- Curated list of external resources
- Organized by difficulty level
- Minimal original content
- Reference material

**Example:** `Code-Design/Code-Design.md`

**Template additions:**
```markdown
## Beginner

### [Topic]

- [Resource title](link) (duration)
  - Brief description of what this covers
  - Why it's valuable

## Intermediate

### [Topic]

[Continue pattern...]

## Expert

### [Topic]

[Continue pattern...]
```

### 4. Style Guidelines

#### Tone & Voice

- **Encouraging but realistic**: "This is challenging but achievable"
- **Professional but approachable**: Avoid overly academic language
- **Action-oriented**: Use imperative mood for instructions
- **Inclusive**: "you" not "the student", "we" not "the instructors"

#### Formatting

- **Headers**: Use sentence case ("Learning objectives" not "Learning Objectives")
- **Code blocks**: Always specify language for syntax highlighting
- **Lists**: Use bullet points for unordered, numbers for sequential steps
- **Emphasis**: Use **bold** for key terms, _italics_ for emphasis
- **Links**: Use descriptive text ("[Linux setup guide](Setup)" not "[click here](Setup)")

#### Visual Structure

- **Use horizontal rules** (`---`) to separate major sections
- **Limit line length**: ~80-100 characters for readability
- **Whitespace matters**: Separate sections with blank lines
- **Consistent indentation**: 2 spaces for nested lists

### 5. Quality Checklist

Before publishing any new module, verify:

- [ ] Estimation time provided and realistic
- [ ] Learning objectives are specific and measurable
- [ ] Prerequisites clearly stated
- [ ] Content follows progressive difficulty
- [ ] At least 2-3 practical exercises included
- [ ] Code examples are tested and working
- [ ] External resources are high-quality and diverse
- [ ] Navigation links work (home, sidebar, next steps)
- [ ] Table of contents renders correctly
- [ ] No broken links or references
- [ ] Tone is consistent with other modules
- [ ] Spell-checked and grammar-checked

### 6. Adding New Learning Paths

When creating entirely new training paths:

1. **Create path overview** (e.g., `NewTopic/NewTopic.md`)
   - Follow the introduction template
   - List all modules in the path
   - Set overall time estimate

2. **Create individual modules**
   - Follow module type template
   - Link back to path overview

3. **Update navigation**
   - Add to `_sidebar.md`
   - Ensure all cross-links work

4. **Update home.md**
   - If it's a major path, mention on home page

---

## Examples of Excellence

### Best Practice Examples in This Wiki

1. **Clear learning objectives**: `Node/Node.md` lines 26-32
2. **Progressive exercises**: `Node/Javascript.md` lines 97-256
3. **Good resource curation**: `Code-Design/Code-Design.md`
4. **Clear next steps**: `Workflow/Workflow.md` line 31
5. **Practical project setup**: `Node/Call-Of-Duty.md`

### Common Pitfalls to Avoid

1. **Vague objectives**: "Understand JavaScript" → "Write async functions"
2. **Missing time estimates**: Always provide realistic timelines
3. **Wall of text**: Break content into sections with headers
4. **No practical application**: Always include exercises
5. **Broken navigation**: Test all links before publishing
6. **Inconsistent formatting**: Follow the style guidelines
7. **Outdated resources**: Verify external links periodically

---

## Maintenance Guidelines

### Regular Reviews

- **Quarterly**: Check all external links for validity
- **Bi-annually**: Review and update time estimates based on learner feedback
- **Annually**: Assess if content aligns with current industry practices

### Version Control

- Track changes to training content
- Document major revisions in commit messages
- Tag stable versions of the curriculum

### Feedback Integration

- Collect learner feedback on difficulty and clarity
- Adjust time estimates based on actual completion times
- Add new resources based on emerging best practices

---

## Quick Reference

### Markdown Shortcuts Used

- `[[_TOC_]]` - Automatic table of contents
- `[text](file)` - Internal wiki links
- `[text](url)` - External links
- `` `code` `` - Inline code
- ` ```language ` - Code blocks with syntax highlighting
- `---` - Horizontal rule (section separator)
- `> ` - Blockquotes for callouts

### File Naming Convention

- Use kebab-case: `Asynchronous-Javascript.md`
- Match the link text in sidebar: `[Asynchronous in Javascript](Node/Asynchronous-Javascript)`
- Keep names descriptive but concise

### Link Patterns

- Home: `[home](home)`
- Sidebar: `[_sidebar](_sidebar)`
- Other modules: `[Module Name](Path/Module-File)`
- External: `[Descriptive Text](https://example.com)`

---

**Remember**: The goal is to create training content that empowers developers to learn effectively. Every module should leave the learner feeling capable and prepared for the next step in their journey.

*Last updated: 2026-02-02*
