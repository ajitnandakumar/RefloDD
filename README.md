# RefloDD (*Re*quirement *Flo*wdown *D*riven *D*evelopment) 
A method for systems thinkers building software with AI agents
  
Version 0.1 | Author: Ajit Nandakumar Mannargudi | [LinkedIn](https://www.linkedin.com/in/ajitnandakumar) | [email](mailto:ajitnandakumar.projects@gmail.com)

## Overview
### When is structured development needed?
How much structure a build with *coding agents* needs, depends on how complex it is. For a small app, a clear description of what you want is enough to build from. Vibe coding with incremental conversational prompts should get you to your goal, without a structured development method.

As a system grows, no one can hold all the context in perspective and together. For humans, engineering answered this long ago with *levels of abstraction*.
- *Requirements* state what the system must do.
- *Architecture* decides how it is divided.
- *Specifications* state what each part must do.
- *Code* implements them.

Two practices check what is built and hold the levels together.
- *Verification* demonstrates that what was built satisfies the requirements.
- *Traceability* links the levels.

Each level adds detail beyond the one above it, so depth increases *progressively* across levels. *Requirements* stay shallow but cover the whole system in scope, which is what lets it be seen as one system. *Specs* elaborate the requirements allocated to each part of the system, with enough detail for code to be written precisely. *Traceability* lets you zoom in or out across the levels.

> Progressive depth with clear traceability is what makes the complexity manageable. The structure exists for that reason, not just for the sake of process compliance.

### Agents face a similar issue to humans
An AI agent is bounded the same way. As scale and complexity grow, finding the right context and reasoning over it correctly becomes the hard part. Drift, hallucination and unintended actions by the coding agent add to it.

The result is that the developer has to be skilled at handling the agent, which works against the benefit AI is meant to bring.

So the same answer applies. *Requirements* flow down through the *architecture* into *specifications*, *code* is built against *specifications*, and a *trace* connects every level. The context the agent needs is structured, rather than being steered into place on every task. The skill that matters shifts from steering the agent task by task, to reasoning about requirements.

>RefloDD can be viewed as a systematic way to engineer software using AI agents, or as an additional harness layered over coding agents. Either way, RefloDD **leverages AI at every step**, and the goal is a development that stays *reliable, explainable, and maintainable*.

## Who this is for

RefloDD is built for **systems thinkers, architects and solo builders**, people who reason about what a system must do and why, and who find a detailed requirement useful rather than a burden.

It shifts effort away from writing code by hand toward *reasoning about requirements and governing architecture.* The ability to reason about requirements is the prerequisite, not fluency with development tools.

Beyond that, the human must have enough technical literacy to evaluate database schemas, critique architectural trade-offs, and judge whether code matches the spec it was built from. AI can help with the analysis, but the human must provide the judgement.

It is not for everyone. Developers who find requirement writing a chore will not enjoy this. No method survives being forced on someone who resents its first step.


## The Method

### *The Trio*
***Architect agent | Co-Architect agent | Human***  

1. An *Architect agent* proposes, a *Co-Architect agent* on a different model reviews, and the *human* decides. These three are referred to as "the Trio". Using different models is intended to reduce shared blind spots and widen perspective.
2. *The Trio* is convened wherever a decision needs judgement, including the conversion of each requirement into a spec, architecture decisions, plan reviews, and the code-versus-spec report.
3. The Co-Architect states what it examined before it agrees, and each objection names what is wrong, where, and why. It is a peer reviewer, not an adversary. 
4. When the debate between the Architect agent and the Co-Architect agent runs long or complex, a short structured summary is generated. It lets the human review quickly and drill down to the full exchange where needed.

### *Requirements and architecture*
***Requirements** -> Modular **Architecture** definition -> **Module** definition*  

5. *Requirements* are the root source of truth. Everything downstream derives from them. Downstream work can reveal the need to change the requirement, but only a human makes the change, and it is written back into the *requirement* file.
6. The requirement file holds the following for each requirement:
	- An **ID**
	- The **requirement**, written in EARS form (Easy Approach to Requirements Syntax)
	- Its **objective**
	- A **criticality tier**
7. *Requirements* for the system in scope are researched with AI, debated with AI using *the Trio*,  and finalized before any *spec* exists. 
8. The *architecture* is researched and debated with AI alongside the *requirements* using *the Trio*, and it determines the *modules* and their allocated *requirements*.
9. *Architecture Decision Records* (ADRs) are converted into *derived requirements* and are a part of the same requirement file. What an architecture obliges the system to do is recorded as a requirement.

### *Specs*
***Requirements** ->  **Specs** definition for each **module** in scope for the **phase***  

10. The *requirements* allocated to each *module* are converted into that module's *spec* through a structured review by *the Trio*, against the spec *template*. This conversion from *requirements* to *specs* is the most critical in the method, because it is where intent becomes something an agent will execute literally, and an omission there passes silently into code. 
11. A **phase** is an increment of the build.  It is tracked by a *project progress tracking file* defined for the *coding agent*. It is also a structural part of each *spec* file.  
12. Before the *specs* for a *phase* are written, the requirements in scope for it are reviewed by *the Trio* for contradiction and duplication. This is needed because two conflicting requirements can each pass traceability coverage, which checks one requirement at a time.
13. A ***spec*** is written against the *requirements* it covers. **It is organized by phase**, and *each phase* section carries:
	- **Phase number** 
	- **Acceptance criteria** state the behavior the module must exhibit. They are written in Given/When/Then form, each categorized and traced to the requirement it verifies. Categories are fixed: normal, boundary, error, adversarial, security, state transition, non-functional.
	- **Schema definitions** for the data the module owns.
	- **Architectural constraints and overrides** that apply to the module, each traced to a requirement.
14. A *spec* grows phase by phase *within the same file*. Each phase’s section *freezes once executed*, with one exception: an entry can be superseded. When a requirement changes after the phase that covered it has executed, *the Trio* decides which future phase carries the change. The frozen entry is replaced by a pointer to the section that supersedes it, and its original wording stays in version history.
15. Before each spec is executed, *the Trio* checks it **again** for completeness and accuracy against the requirements it covers, considering lessons from the execution of the previous phase.
 
### *The coding agent*
***Specs**  -> **Code***  

16. Deciding *what to build* and *building* it are separate concerns, held by separate actors.
17. The *coding agent* executes a *spec*. It has no role in defining *requirements*, *architecture* or *specs*.
18. The *coding agent* **plans** the implementation of the *spec* and submits the *plan* (like *plan mode* in Claude Code) to *the Trio* for review, before implementing it. The *plan* covers implementation only. A gap in the *spec* is reported there, not resolved there.
19. Where the *spec* does not cover a case, the *coding agent* reports it in its *plan*. The missing case is considered a defect in the *spec* and is resolved by *the Trio*.
20. Irreversible operations, such as database migrations and changes to production, are executed by the *human* and not the *coding agent*.

### *Verification*
***Specs**  -> **Test Cases***  
***Code** versus **Spec** check*  

21. A *requirement* is closed only when its *verification* demonstrates the behavior it demands. Test cases are written by the *coding agent* based on the *spec*, in a separate session and without reference to the code.
22. After implementation, a *separate agent* checks the code against the *spec* and reports any discrepancies. *The Trio* decides whether each is a defect in the spec or in the implementation.

### *Traceability*
***Requirement** -> **Spec** -> **Code** -> **Verification***  
***Code** -> **Spec** -> **Requirement***  

23. The *trace* (unique traceability ID) connecting *requirement* → *spec* → *code* → *verification* must be machine extractable for automated *traceability analysis*. 
24. *Traceability* is checked bi-directionally. Forward finds requirements with no implementation, backward finds code that traces to no requirement.


### *The human*
25. Rigor in *the Trio's* review is proportional to the *criticality* of the requirement. *Criticality* is decided once, at the requirement, and it determines where human attention is spent.
26. The human closes every decision and owns the risk in it.
27. The purpose of every human approval is *understanding*, *judgement* and *taste*, not just permission.

### *Retrospective*
28. After every phase *the Trio* holds a *retrospective* on how to improve the next phase. This helps avoid repeating mistakes and fine-tunes the user’s adaptation of RefloDD, so that it fits their situation and runs efficiently.


---


## Annexure: The obvious questions

### Is this waterfall?
It shares the *requirement flowdown* aspect of waterfall. It does not share the part that made waterfall fail. Flowdown appears in many lifecycle models, and is not exclusive to waterfall. What made waterfall fail was the single pass, with requirements settled once and user feedback arriving at the end.

*Requirements* and *architecture* are done upfront, to have a holistic view of the system in scope and architect it better. *Specs* then advance phase by phase, and a *phase* can be scoped to ship. When so scoped, feedback is iterative and flows back into the requirements through the human. A later phase can supersede what an earlier phase specified, so an upfront decision is not final.

AI has made coding cheaper and compressed the time to build. AI also understands natural language intent well, so it makes sense to focus on requirement flowdown. 


### If code is precise, why are requirements needed?

Some argue that *code* is more precise than a *requirement* written in natural language, so code is the source of truth. However, being more precise is not enough to make it the only source of truth.

*Code* is authoritative about what the system does. The *requirement* is authoritative about what it must do. The *spec* is authoritative about how requirements are to be implemented.

These are different things. Only the *requirement* can tell if the *spec* is correct, and only the *spec* can tell if the *code* is correct.

The question is not about which is more precise. **It is about how precision is reached.**

Someone who can hold a whole system in mind can go straight to code. That holds while the system is small.

Even when coding directly, the idea starts as a thought in the mind in natural language. So the choice is not between natural language and code. It is whether the intent is stated in its own right, or only implied by what was built from it.


### Does this not slow everything down?
Writing *requirements* and *specs* before any code is real work, but is simplified by using the *Trio*. When AI is able to write code well, what matters more is the thinking and structuring behind the input to it.

The structure also means the *coding agent* does not need steering on every task.

The aim is steady, sustainable progress on complex software, not the fastest possible first commit.


### How is this different from spec-driven development?

The author has not done a systematic comparison study, and this is not an argument that RefloDD is better. What follows is opinion formed from the documentation and demonstrations the author has looked at, and from the author’s own practice.

- **Shared roots:** Firstly the principles of SDD and RefloDD are directly or indirectly influenced by traditional requirement flowdown engineering. SDD does not claim them, RefloDD embraces them as they exist for the purpose of effectively managing large context and not just for documentation.

- **Generic method for ease of custom adaptation:** While methods exist for many SDDs, the demonstrations the author has seen use them as tools with a predefined framework such as feature by feature development flow. RefloDD focuses on the method, providing the basic constructs so that the user can adapt to their own situation, be it solo development, feature based, sprint scoped etc. It lets the user discover their workflow organically.

- **Single agent vs the Trio:** *The Trio* concept makes a big difference. It is central to leveraging AI for defining and building. The SDD methods pair a single AI agent with the human. In RefloDD, using a Co-Architect agent to review the Architect agent’s recommendations, significantly improves quality and reduces drift in discussions and artifacts. It can also help adapt the method to the user’s use case and guide them through the process.

- **Requirement driven:** RefloDD considers *requirements* as root source of truth and draws a clear distinction from specification. SDD methods do use artifacts like requirements but they are used interchangeably with specification. Even the name is Spec driven, and not requirement driven.

- **Traceability:** RefloDD requires a trace from requirement to verification that a machine can extract and check in both directions. This is important for reducing drift and for keeping the system explainable and maintainable over time.  The SDD tools the author has looked at do not provide this.

- **Audience:** SDD methods seem more suitable for developers, although they are claimed for non-coders too. RefloDD is more suitable for systems thinkers, architects and solo builders.


### Can it be used for PoC or quick prototype?
For most PoCs or for quickly prototyping a feature, RefloDD is not needed and vibe coding is likely to be enough. Even here, some concepts of RefloDD, like using *the Trio* to come up with requirements, will help you vibe code effectively.

However, when there is a need to build production-grade software that has to stay reliable, explainable and maintainable, RefloDD is suitable.


### Is this a tool? 
No. It is a method. How much of it is *automated* and the way it is *adapted* as a workflow is an implementation choice. 


### Is this in use? 
The author is building an enterprise search application using this method, in a predominantly manual workflow for now, in order to build a deep understanding of AI behavior. It is a work in progress. 

The implementation is deliberately left out in the method, since the idea is that the users can adapt what is best for their situation rather than rigid frameworks. The below is the author's implementation as of now. **This is only to give an idea and is not a recommendation.** 

1. *Requirements* - CSV file. Used deep research AI tools and the Trio
2. *The Trio* - One Claude.ai Chat session configured as Architect. Gemini AI chat configured as Co-Architect. Summarize when conversation is long for easy human judgement 
3. *Coding Agent* - Claude Code in VS Code in chat mode. Always start in Plan mode.
4. *Specs* - Split into modular specs with a separate .md file for each, in spec folder. Has version history. 
5. *Rules* - in rules folder. Separate file for each type of rules set.
6. *Claude.md* - Contains Project objective. User's (the person building) technical capability, pointers to rules, folder structure and specs
7. *Progress tracking* - Progress.md has phases and modules under it with check boxes, and version history.


### Where does RefloDD come from?
Much of the practice in RefloDD is drawn from established systems engineering *standards* and widely used *notations and practices*. RefloDD adapts that practice for agentic coding and presents it as a method.

- **ISO/IEC/IEEE 29148** for requirements engineering, derived requirements, and requirement consistency.
- **INCOSE Guide to Writing Requirements** for requirement attributes and rationale.
- **SWEBOK** for bi-directional verification traceability.
- **ISO/IEC/IEEE 15288** for the principle that architecture induces requirements.
- **EARS** (Mavin et al., Rolls-Royce, 2009) for requirement syntax.
- **Given/When/Then**, from behavior-driven development, for acceptance criteria.
- **Retrospective**, inspired by Scrum and Kaizen, for the review after each phase.

### Why publish this method?
So that more people can implement it in a way they deem fit and develop it further. Any critical feedback is always welcome.


> © 2026 Ajit Nandakumar Mannargudi. Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).