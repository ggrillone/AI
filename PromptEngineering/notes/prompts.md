## Create Prompt Engineering Guide based on articles I have read and a rough draft of the guide I wrote

````
# Role and Objective
Serve as an experienced principal frontend engineer and expert AI mentor, focused on guiding frontend developers to advance their AI and prompt engineering skills progressively—from foundational to advanced—emphasizing hands-on, practical learning and curiosity-driven exploration. Help refine, organize, and consolidate a draft learning guide to create a seamless resource.

# Instructions
- Begin with a succinct checklist outlining the primary tasks before refining the provided learning guide.
- Use the draft content to develop a comprehensive, organized, and engaging interactive guide for AI and prompt engineering.
- Structure the guide to move logically from basic concepts to advanced techniques, ensuring each lesson builds on prior knowledge.
- Refine, organize, and eliminate redundancies in the draft content.
  - For example, integrate relevant content from Anthropic videos into specific sections such as zero-shot or few-shot learning, consolidating similar content as needed.
- Incorporate examples and hands-on exercises provided in the draft.
- Seamlessly integrate all relevant portions of the draft content.
  - For instance, when discussing self-reflection (tree of thought), merge associated content from sections like "Verification/Validation" mentioned in "Additional prompt elements I use."

## Sub-categories
- Tailor explanations and exercises to frontend development scenarios when relevant.
- For hands-on tasks, deliver clear, step-by-step instructions and sample solutions for all new techniques.

# Context
Draft content file: @promptEngineeringKnowledgeSharePart1Complete.md 

# Tone and Target Audience
- Ensure all material is accessible to those without prior AI experience, maintaining a welcoming and inclusive tone.
- Add pop-culture references sparingly for engagement, building on the existing Lord of the Rings and Spider-Man mentions, but avoid overuse.

# Constraints
- The guide must function as a complete and standalone resource, requiring no outside prerequisites or prior AI knowledge.
- Do not modify the draft content file `PromptEngineering/promptEngineeringKnowledgeSharePart1Complete.md`
- Do not try and write/output all content at once, break it into chunks to avoid max token output issues

# Reasoning Steps
- Internally assess and refine lesson order and depth to ensure clarity, logical flow, and skill development.
- Continuously evaluate and adapt lesson complexity based on anticipated learner understanding.

# Planning and Verification
- Draft a curriculum that progresses from fundamentals to advanced prompt engineering topics.
- Define clear, measurable lesson objectives and anticipated outcomes.
- Catalog all resources at the end of the guide, with in-guide citations as needed.
- Confirm integration and representation of all content from the draft.
- After drafting or modifying lessons, validate that each section follows the intended learning progression, includes all designated draft content, and meets the clarity and engagement standards. Self-correct and adjust if validation fails.
  - Briefly validate (in 1-2 lines) that the integration of draft content, logical progression, and pedagogical clarity are achieved; self-correct as necessary before moving forward.

# Output
- Break output into multiple chunks/files under `PromptEngineering/FinalizedGuide`
  - Introduction, curriculum overview, and foundational lessons
  - Intermediate lessons
  - Advanced lessons
  - Expert techniques and personal workflows
  - Summary tables and resources
- Present curriculum and lessons in Markdown with clear headings and hierarchical sectioning.
- Use `step-by-step` and tables for tutorials and checklists when applicable.
- Include diagrams and tables as visual aids when suitable.
- For each lesson, format as follows:
- **Lesson Title**
- **Objectives**: Specific, measurable goals
- **Explanation**: Practical overview and breakdown for complex ideas
- **Step-by-Step Tutorial**: Ordered instructions/methods
- **Examples & Exercises**: Hands-on activity with sample solution and validation criteria (manual self-check or provided answer)
- **Frontend Scenario Contextualization**: Connect the concept to relevant frontend development scenarios
- At the end, provide:
- A summary table of all lessons, with objectives and outcomes
- A comprehensive reference list

## Output Format
Output must be in Markdown and follow this format for each lesson:

```markdown
## Lesson: <Title>
### Objectives
- Objective 1
- Objective 2
### Explanation
- Key ideas with supporting detail.
### Step-by-Step Tutorial
1. Step 1
2. Step 2
### Examples & Exercises
- Example: <description/code>
- Exercise: <activity>
- Solution: <answer/walkthrough>
- Validation: <manual self-check or solution criteria>
### Frontend Contextualization
- Specific frontend application or example.
```

For overviews, summaries, or diagrams, use Markdown tables or diagrams. Always specify whether the learner should self-validate solutions or use provided criteria.

# Verbosity
- Provide concise, practical explanations with thorough detail for complex concepts.
- In code or prompt examples, prefer explicit and clear style for readability.

# Stop Conditions
- Completion occurs when the interactive guide thoroughly covers foundational to advanced skills with exercises and validation instructions, ensuring all original draft content is incorporated and learners are encouraged to explore further.
````

---

## Create plan for addressing all TODOs - items I want to expand on

```
# Purpose
Enhance the quality, completeness, and accuracy of prompt engineering documentation targeted at programmers—especially frontend developers. The documentation must remain accessible to those new to AI while providing substantial value for those with prior experience utilizing AI in coding workflows.

Begin with a concise checklist of what you will do.

# Instructions
- Review the provided documentation structure, focusing on all sections, notes, and TODO markers.
- Expand all sections marked with "TODO" to full, informative content.
- Ensure explanations are clear enough for AI newcomers, yet insightful for experienced users.
- Evaluate all listed resources for accuracy and applicability, flagging outdated or misleading materials.
- Identify content gaps and inaccuracies, but do not implement direct edits—only recommend corrections.
After each stage of review or analysis (e.g., after expanding TODOs or completing the resource review), validate your output in 1-2 lines: confirm the step's goals were met or explain what needs correction.

## Task Breakdown
1. Analyze the entire documentation and address all "TODO" markers by expanding them into detailed content.
2. Construct a comprehensive checklist that references each section or TODO marker, with actionable tasks and sub-tasks where appropriate.
3. Scrutinize the coverage of topics, compiling a list of necessary missing topics with explanations to clarify their importance.
4. Review the provided resource list. Summarize findings, verdicts on relevance or accuracy, and suggest critical additional resources if any are lacking.
5. Document all identified inaccuracies in existing content, specifying the section, issue, and recommending a correction. Do not modify the original documentation directly.

# Context
- I have created a brain dump of the knowledge share and all resources used in the promptEngineeringKnowledgeShareBrainDump.md file

# Output Format
Your response must follow this structure:
1. **Checklist**
- Markdown numbered list. Each item should include:
- The referenced section or TODO marker
- A concise task description
- (Optional) Sub-tasks, indented as sub-items
2. **Identified Gaps**
- Bulleted list. Each point describes a missing topic or gap, with a brief rationale
3. **Resource Review**
- Table with these columns: Resource Name/Link, Evaluation/Notes, Recommendations
4. **Accuracy Issues**

- Numbered list. For each, specify: Section, Description of the inaccuracy, and a Suggested Correction

Write all planning and checklist output to the file promptEngineeringKnowledgeShareRefinementPart1Log.md

# Constraints
- Do not modify the promptEngineeringKnowledgeShareBrainDump.md file
- Edits to the knowledge share content can go into the file called promptEngineeringKnowledgeShareRefinementPart1.md
```

---

## Execute plan created from previous prompt and update all TODO content

```
# Role and Objective
You are an expert software engineer with specialized writing skills tasked with updating knowledge share notes on prompt engineering.

Begin with a concise checklist of what you will do.

# Instructions
- Review the original notes in `promptEngineeringKnowledgeShareBrainDump.md`.
- Examine the changes to be implemented in `promptEngineeringKnowledgeShareRefinementPart1.md` and `promptEngineeringKnowledgeShareRefinementPart1Log.md`.
- Replace every 'TODO' in the original notes with the relevant update from the RefinementPart1 files.
- Apply updates in the sequential order they appear in `promptEngineeringKnowledgeShareRefinementPart1Log.md`. If multiple changes target overlapping or adjacent content, resolve them in the log order.
- If any referenced 'TODO' is not found in the source or update files, document an error under an Errors section in your output.
- After making the updates, confirm that no references to 'TODO' remain or were missed.
After each edit, validate that the replacement corresponds exactly to the intended update and that no 'TODO' instances remain. Proceed to the next edit or self-correct if validation fails.

# Context
- All relevant files live under the PromptEngineering folder
- The `promptEngineeringKnowledgeShare.md` file exists already, but is empty

# Constraints
- Update only the `promptEngineeringKnowledgeShare.md` file.
- Use only `promptEngineeringKnowledgeShareRefinementPart1.md` and `promptEngineeringKnowledgeShareRefinementPart1Log.md` to make updates; do not make any other changes.
- Do not alter formatting or text beyond what is necessary to apply the updates.

# Output
- Output the fully updated content for `promptEngineeringKnowledgeShare.md` in Markdown format.
```

---

## Review the guide and make sure nothing was missed from my original draft that I wrote

```
# Task Objective
Review the original draft content in `PromptEngineering/promptEngineeringKnowledgeSharePart1Complete.md` and compare it with the polished output files under the `PromptEngineering/FinalizedGuide` directory. Ensure that all essential information from the draft is preserved in the finalized guide.

Begin with a concise checklist of what you will do.

# Instructions
- Confirm that every key point and guidance from the draft is accurately reflected in the finalized guide.
- Thoroughly assess the finalized guide for:
  - Missing or inaccurate information
  - Content gaps
  - Unclear guidance
  - Redundancies   - Information consolidation opportunities
  - Spelling and grammar mistakes
  - Issues with flow and organization   - Any other issues

- Document your findings in detail and provide actionable suggestions for improvement.

After each comparison or content review step, validate whether essential information has been preserved and clearly note any discrepancies or omissions before proceeding.

# Output Requirements
- Write the summary to `PromptEngineering/finalReviewOutput.md` in **Markdown** format.
- Use the following section structure:
1. **Overview**: Succinctly state what you reviewed, including any missing or incomplete files.
2. **Findings**: For each issue:
- Type (e.g., Missing Information, Inaccuracy, Gap, Unclear Guidance, Redundancy, Spelling/Grammar, Flow)
- Location/Reference (section numbers or verbatim excerpts)
- Description of the issue
- Severity (Critical, Major, Minor)
3. **Suggestions**: Offer clear recommendations or resolutions for each finding.
4. **Summary Table**: (Optional) A table summarizing findings (Type / Location / Severity).
- List all findings in severity order from Critical to Minor.
- Reference and quote from draft/finalized content when supporting your findings.
- If either file is missing or incomplete, report this prominently in the Overview and skip detailed analysis.

# Additional Notes
- Ensure consistent and logical structure across the summary.
- Do not proceed to detailed analysis if required files are unavailable.
- Always preserve the original intent and details from both draft and finalized versions.

Attempt a first pass autonomously unless missing critical information; if required files are unavailable or content cannot be validated, stop and prominently report in the Overview before proceeding.
```

---

## Create a visual diagram - a visual to help determine what prompting techniques to follow based on your problem

```
# Objective
Create a visual thought process (such as a mind map) for building effective prompts, drawing exclusively from:
- `PromptEngineering/promptEngineeringKnowledgeSharePart1Complete.md`
- All `.md` files within `PromptEngineering/FinalizedGuide`

# Instructions
- Begin with a concise checklist of sub-tasks that will guide your approach before producing the final mind map or outline.
- Capture the sequence and logic of effective prompt construction as reflected in the referenced materials.
- Highlight key decision points as nodes/questions, including possible paths (e.g., Yes/No splits or alternatives).
- Incorporate guiding questions such as:
- "Do I have a specific solution in mind?" (Yes/No → next step)
- "Did the AI response include incorrect assumptions?" (Yes → What additional context can I provide? → ...)
- Reference the "When a prompt doesn't work ask questions like" section for relevant inquiry paths.
- Integrate various prompt engineering techniques (e.g., Chain-of-Thought, prompt chaining, etc.) into appropriate branches or nodes as you encounter them.
- Add any further steps or considerations uniquely present in the provided files.

# Context
- Structure your work entirely on the referenced markdown files. Do not introduce external concepts.
- Focus on actionable questions and decision pathways central to prompt engineering.
- Set reasoning_effort = medium to ensure well-developed structure without unnecessary verbosity.

# Output Format
- Generate an image if possible, otherwise output as a Markdown-based mind map—use Markdown to demonstrate nodes and branches if actual visuals are not possible.
- After presenting the outline or mind map, briefly validate that all major steps and techniques from the sources have been represented, and note if any referenced areas require clarification or are missing.  # Verification
- Verify all critical content is included
```
