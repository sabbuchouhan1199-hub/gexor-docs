GEXOR
Product Requirements Document
Version 1.0-MVP
Consolidated Sections 1–8
Status: Consolidated PRD document

Contents
1. Section 1 — Product Foundation
2. Section 2 — Target Users, Personas, Jobs to Be Done, and Core Use Cases
3. Section 3 — MVP Scope, Product Capabilities, Exclusions, and Release Boundaries
4. Section 4 — Product Experience, User Journeys, Interaction Requirements, and User States
5. Section 5 — Business Model, Commercial Strategy, Product Metrics, Validation, and Growth
6. Section 6 — Product Assumptions, Constraints, Dependencies, Risks, and Mitigation Strategy
7. Section 7 — Release Strategy, Product Roadmap, Milestones, and Launch Readiness
8. Section 8 — Product Governance, Requirement Traceability, Decision Control, Glossary, Approval, and Handoff
All original PRD section wording has been preserved and merged into this single document.

PRODUCT REQUIREMENTS DOCUMENT
Working Product Name
AI Runtime Chat Platform
Note: This is a temporary working name. The final brand name can be selected later without changing the core product specification.

1. Document Overview
1.1 Document Purpose
This Product Requirements Document defines the product vision, user problems, target users, value proposition, scope, requirements, constraints, success criteria, risks, and planned evolution of the AI Runtime Chat Platform.
This document will serve as the primary product reference for:
Product planning
User-experience design
Technical architecture
Database design
API design
AI engine design
Development prioritization
Testing and acceptance
Security planning
Deployment planning
Launch preparation
Future product decisions
The PRD defines what must be built and why it must be built.
Detailed technical implementation will be defined separately in architecture, database, API, engine, security, testing, and deployment documents.

1.2 Document Status
Document type: Product Requirements Document
Product stage: Pre-development
Current status: Initial baseline
Intended release: MVP
Document owner: Founder/Product Owner
Primary readers:
Founder
Product manager
UI/UX designer
Frontend developer
Backend developer
AI engineer
Database engineer
Security reviewer
QA engineer
Future team members

1.3 Source of Truth
This PRD will act as the product-level source of truth.
When a product requirement changes:
1. The proposed change must be evaluated.
2. The relevant PRD section must be updated.
3. Dependent technical documents must be reviewed.
4. Implementation tasks must be updated.
5. Test cases must be updated.
6. The change must be recorded in the document history.
Developers must not independently invent product behaviour that conflicts with this document.
When technical constraints require a product change, the decision must first be documented and approved.

1.4 Document Principles
This PRD follows these principles:
MVP scope must remain focused.
Product requirements must be measurable.
User control must be preserved.
AI behaviour must remain transparent.
User data must remain isolated and protected.
Provider independence must be maintained.
Memory must improve results without becoming unsafe or intrusive.
Cost optimisation must not silently reduce answer quality.
Complex internal processing must appear simple to the user.
Future features must not unnecessarily delay the MVP.
Every major feature must solve a defined user problem.

2. Executive Summary
The AI Runtime Chat Platform is a provider-independent AI workspace that sits between the user and external AI models.
The platform does not train or provide its own foundation model.
Users connect their own supported AI provider accounts or API keys and interact with those models through a familiar chat interface.
The platform improves the interaction by adding an intelligent runtime layer containing:
Prompt enhancement
Intent and task classification
Relevant memory retrieval
Structured long-term memory
Context management
Model selection support
Provider routing
Token and cost optimisation
Response processing
Background memory extraction
Workspace-level continuity
A user can write a simple or incomplete message without manually engineering a complex prompt.
Before the message reaches the selected AI model, the platform determines:
What the user is trying to accomplish
Whether the prompt requires enhancement
Which previous memories are relevant
Which project or workspace context should be included
How much context should be added
Which model is suitable
Whether a cheaper model can complete the task
Which instructions and output structure should be applied
The selected AI provider generates the response.
The response is streamed to the user immediately to preserve speed.
After or during response delivery, background processing evaluates the conversation and extracts useful information such as:
Confirmed user preferences
Project facts
Decisions
Instructions
Constraints
Important entities
Long-term knowledge
Temporary context
Potential memory conflicts
On future requests, only relevant and permitted memories are retrieved and added to the runtime context.
The intended result is that a connected AI model feels more consistent, personalised, context-aware, structured, and useful than it would through a basic direct chat interface.

3. Product Vision
3.1 Vision Statement
Create a provider-independent AI workspace where users can connect different AI models while retaining their own memory, context, projects, preferences, and working continuity.
The AI provider should be replaceable.
The user’s context, memory, knowledge, and workspace should remain portable and persistent.

3.2 Long-Term Vision
The long-term product will become an intelligent runtime environment for interacting with multiple AI providers.
It will manage the complete interaction lifecycle:
1. Understand the user’s intent.
2. Retrieve relevant context.
3. Improve the prompt.
4. Select or recommend an appropriate model.
5. control token and cost usage.
6. Execute the provider request.
7. Stream the response.
8. Process the output.
9. Extract useful memories and knowledge.
10. Preserve project continuity.
11. Support tools, workflows, and agents.
12. Allow users to switch providers without losing context.
The platform should eventually support individuals, professionals, teams, and organisations.

3.3 MVP Vision
The MVP will prove one central product hypothesis:
A provider-independent chat workspace with reliable structured memory and intelligent prompt construction can produce more relevant and continuous AI interactions than a basic direct-provider chat interface.
The MVP will focus on:
User authentication
Personal workspaces
Provider API-key connection
Familiar AI chat
Prompt enhancement
Structured memory
Relevant memory retrieval
Conversation continuity
Basic model selection
Token and cost visibility
User-controlled memory management
Secure data handling
The MVP will not attempt to build the entire long-term platform.

4. Product Thesis
4.1 Core Thesis
AI models are already powerful, but the quality of the user experience is limited by the interaction layer around them.
Users often receive weaker results because:
Their prompts are incomplete.
Relevant context is missing.
Past decisions are forgotten.
Long chat histories become inefficient.
The wrong model is selected.
The user does not know how to structure instructions.
Context must be repeated across conversations.
Provider switching breaks continuity.
Raw history is used instead of relevant structured memory.
Users cannot clearly see how much context or cost was used.
The product thesis is that a dedicated runtime layer can improve these interactions without building a new foundation model.

4.2 User Experience Thesis
The user should feel:
“I do not have to explain everything again.”
“This AI understands my current project.”
“My rough request becomes a high-quality instruction.”
“The system remembers the right information.”
“I can correct or delete anything it remembers.”
“I can change AI providers without losing continuity.”
“I understand which model and memories were used.”
“I can control my API cost.”
“The platform feels smarter than a normal chat interface.”

4.3 Technical Thesis
The product can create better AI interactions by combining:
Structured memory instead of complete raw-history injection
Relevance-based context retrieval
Task-aware prompt construction
Provider-specific prompt adaptation
Context-budget management
Model capability and cost awareness
Background memory processing
User confirmation and correction
Transparent runtime decisions
Provider-independent data storage

4.4 Business Thesis
Users may pay for the intelligence and continuity layer even when they separately pay their selected AI provider.
The platform’s commercial value will come from:
Saving the user time
Reducing repeated explanations
Improving first-response usefulness
Preserving project continuity
Supporting multiple providers
Giving users control over memory
Improving model and token selection
Organising AI work into persistent workspaces
Reducing dependence on a single AI provider
The initial commercial model will be software-as-a-service with Bring Your Own Key support.

5. Problem Statement
5.1 Primary Problem
Current AI chat applications usually connect users directly to a single model or provider.
The model may be capable, but the surrounding interaction system often fails to manage long-term context, memory quality, prompt structure, provider portability, and cost efficiency.
As a result, users repeatedly perform work that the system should manage automatically.

5.2 User Problems
Users commonly experience the following problems:
Repeated Context
Users must repeatedly explain:
Who they are
What they are working on
Their goals
Their preferences
Previous decisions
Project constraints
Required formats
Technical choices
Current progress
Weak Prompt Construction
Many users know what they want but do not know how to write an effective AI prompt.
Their request may be:
Too short
Ambiguous
Missing constraints
Missing context
Missing expected output format
Poorly structured
Written in informal language
Unsuitable for the selected model
Lost Continuity
Context is often trapped inside one conversation or one provider.
When the user:
Starts a new chat
Changes provider
Changes model
Returns after several days
Opens a related project
Moves to another device
the useful context may not follow them.
Uncontrolled Memory
Existing memory systems may be:
Limited
Hidden
Provider-specific
Difficult to edit
Difficult to inspect
Based on unclear rules
Mixed with temporary conversation details
Unable to separate personal and project context
Token Waste
Applications may repeatedly send:
Entire conversation histories
Irrelevant messages
Duplicate instructions
Large user profiles
Unnecessary project information
This may increase cost and reduce model focus.
Model Selection Difficulty
Users may not understand:
Which model is best for a task
Which model is faster
Which model is cheaper
Which model supports larger context
Which provider is currently available
Whether a premium model is necessary
Provider Lock-In
A user’s history, memory, preferences, and project knowledge may remain tied to one AI provider.
Switching providers may require starting again.
Lack of Transparency
Users may not know:
What prompt was sent
Which memories were included
Why a model was selected
How many tokens were used
How much the request cost
What information was stored
Why something was remembered

5.3 Business and Professional Problems
Professionals using AI for long-running work face additional problems:
Project decisions are scattered across chats.
Requirements become inconsistent.
AI responses conflict with previous decisions.
Different models receive different context.
Team members do not share the same project understanding.
Important information is buried in conversation history.
AI-assisted work lacks traceability.
Usage costs are difficult to understand.
Switching providers creates operational friction.

5.4 Existing Solution Gaps
Existing AI platforms may provide some combination of:
Basic chat history
Manual custom instructions
Limited memory
Project folders
Model selection
File uploads
Provider-specific assistants
However, the product opportunity exists in combining the following into one provider-independent system:
Automatic but controlled prompt enhancement
Structured and inspectable memory
Relevant context retrieval
Cross-provider continuity
User-owned provider connections
Cost-aware model selection
Workspace-specific intelligence
Transparent prompt and memory usage
Portable user data

6. Proposed Solution
The product will provide a familiar chat interface powered by an intelligent runtime layer.
The runtime layer will process each request through a controlled sequence:
1. Receive the user message.
2. Identify intent and task complexity.
3. Determine whether prompt enhancement is necessary.
4. Retrieve relevant confirmed memories.
5. Retrieve workspace and conversation context.
6. Apply a context-token budget.
7. Construct the provider-ready prompt.
8. Select or recommend a suitable model.
9. Send the request using the user’s connected provider.
10. Stream the provider response to the user.
11. Record token and cost information.
12. Process the response in the background.
13. Extract possible memories, decisions, and knowledge.
14. Deduplicate and classify memory candidates.
15. Save, suggest, reject, or expire memories according to policy.
The user will retain control over:
Connected providers
Selected models
Prompt-enhancement level
Memory mode
Saved memories
Workspace context
Cost limits
Data export
Data deletion
Conversation exclusions

7. Core Value Proposition
7.1 Primary Value Proposition
The product makes connected AI models more useful by automatically supplying the right instructions, context, and memory without forcing the user to repeatedly manage those elements manually.

7.2 User-Facing Promise
Bring your own AI provider, keep your memory and context, and receive more relevant answers through an intelligent runtime layer.

7.3 Primary Benefits
Better-structured requests
More relevant responses
Less repeated explanation
Persistent project continuity
Cross-provider memory
User-controlled personalisation
Reduced irrelevant context
Greater cost visibility
Flexible model choice
Lower provider lock-in
Transparent memory usage
Organised AI workspaces

7.4 Differentiation
The initial product will differentiate through the combined use of:
Provider-independent architecture
Bring Your Own API Key
Structured memory
Cross-provider continuity
Automatic prompt enhancement
Relevant-context retrieval
User-visible memory controls
Model and cost transparency
Workspace-specific context
Portable data
No single feature should be treated as the complete competitive advantage.
The advantage is the coordinated runtime system.

8. Product Principles
8.1 Provider Independence
The platform must not depend on one AI provider for its core identity.
Users should be able to connect, remove, and switch supported providers.

8.2 User Ownership
Users must retain control over:
Their provider credentials
Conversations
Memories
Workspace information
Uploaded knowledge
Usage records
Exported data
Account deletion

8.3 Structured Memory Over Raw History
The platform should not treat the complete conversation history as permanent memory.
It should extract and store useful structured information.

8.4 Relevant Context Over Maximum Context
More context is not always better.
The system should include the smallest amount of relevant context required to complete the task effectively.

8.5 Transparency Over Hidden Automation
Automation should not remove user control.
Users should be able to understand:
Which model was used
Which memories were used
Why the model was selected
What information was stored
What prompt was sent
What the request cost

8.6 Speed-Preserving Intelligence
Background processing should not unnecessarily delay the visible response.
Where possible:
Provider responses should stream immediately.
Memory extraction should run after response delivery.
Non-critical processing should run asynchronously.
Extra model calls should be avoided for simple requests.

8.7 Cost Awareness
Every additional engine action must justify its token and infrastructure cost.
The platform must avoid increasing cost merely to appear intelligent.

8.8 Privacy by Default
The product should collect and retain only information required for its functions.
Sensitive information must receive stronger controls.
Credentials must never be stored in plain text.

8.9 Reversible Automation
Actions such as memory creation, memory consolidation, model selection, and prompt enhancement should be inspectable and reversible where practical.

8.10 MVP Discipline
The MVP must prove the core value proposition before introducing:
Advanced agents
External actions
Complex team collaboration
Large integration ecosystems
Native mobile applications
Autonomous workflows
Enterprise administration

Gexor — Product Requirements Document
Section 2: Target Users, Personas, Jobs to Be Done, and Core Use Cases

9. Target User Definition
9.1 Primary Target Market
Gexor will initially target individuals who use AI repeatedly for professional, technical, creative, analytical, or project-based work.
These users receive value from AI but experience recurring problems with:
Repeating project context
Writing effective prompts
Maintaining continuity across conversations
Switching between AI providers
Managing long-running work
Controlling model and token costs
Reviewing or correcting remembered information
Organising AI-assisted work into persistent workspaces
The initial target market is not defined only by occupation.
A suitable early Gexor user has the following behavioural characteristics:
Uses AI several times per week
Works on tasks that continue across multiple sessions
Has important preferences, decisions, or project context
Wants better answers without manually writing complex prompts
Is willing to connect an external AI provider
Values control over memory and data
May use or compare multiple AI models
Understands that provider API usage is billed separately
Is comfortable using a web-based productivity application

9.2 Primary User Groups
The initial primary user groups are:
Startup Founders
Founders who use AI for:
Product planning
Market research
Strategy
Documentation
Hiring
Customer communication
Technical decisions
Business analysis
Fundraising preparation
Operational planning
Their main need is continuity across many connected decisions and workstreams.

Freelancers
Freelancers who use AI for:
Client proposals
Research
Content creation
Development assistance
Design briefs
Project planning
Client communication
Reporting
Repetitive deliverables
Administrative work
Their main need is maintaining separate client contexts and producing consistent work efficiently.

Consultants
Consultants who use AI for:
Client analysis
Meeting preparation
Research synthesis
Recommendations
Reports
Frameworks
Presentations
Decision support
Stakeholder communication
Engagement documentation
Their main need is structured client-specific context, traceability, and reliable output quality.

Independent Builders
Independent builders include:
Solo developers
No-code creators
Product builders
Indie hackers
Automation specialists
Technical entrepreneurs
They use AI across product ideation, architecture, implementation, debugging, documentation, and launch.
Their main need is project continuity and the ability to use different models without rebuilding context.

AI Power Users
AI power users regularly use more than one AI platform or model.
They may compare providers according to:
Reasoning capability
Coding performance
Speed
Cost
Context window
Writing quality
Tool support
Reliability
Their main need is a provider-independent workspace that preserves context while allowing model flexibility.

Knowledge Professionals
Knowledge professionals include:
Analysts
Researchers
Product managers
Writers
Marketers
Operations professionals
Educators
Business managers
They use AI to create, analyse, organise, and communicate information.
Their main need is reliable context, structured outputs, and less repetitive prompting.

9.3 Secondary User Groups
Secondary users may be supported after the initial product has demonstrated reliability.
These groups include:
Students working on long-term learning goals
Content creators managing multiple brands
Small agencies
Researchers managing large knowledge collections
Teams requiring shared AI context
Organisations requiring administration and governance
Users operating local or self-hosted models
Non-technical consumers seeking simpler AI interaction
Secondary groups must not expand the MVP scope unless their requirements directly overlap with the primary users.

9.4 Users Not Prioritised in the MVP
The MVP will not be designed primarily for:
Users seeking a completely free AI model
Users unwilling to connect a provider account or API key
Large enterprises requiring formal compliance certifications
Organisations requiring on-premise deployment
Users requiring autonomous agents to perform external actions
Users requiring regulated clinical, legal, or financial decision systems
Users requiring advanced team administration
Users requiring native mobile-only usage
Users seeking image, video, or audio creation as the core product
Users who only ask occasional one-off questions
These users may still access the product where applicable, but their needs will not drive initial development.

10. Early Adopter Profile
10.1 Ideal Early Adopter
The ideal early adopter:
Uses ChatGPT, Claude, Gemini, or another AI provider regularly
Maintains one or more long-running projects
Frequently repeats context to AI
Has experienced inconsistent answers across conversations
Understands basic AI model differences
Is comfortable creating or using an API key
Wants to retain control over provider selection
Cares about privacy and memory visibility
Is willing to test an early-stage product
Can provide detailed product feedback

10.2 Early-Adopter Qualification Signals
A potential user is strongly qualified when they say:
“I keep explaining the same project again.”
“My important decisions are spread across many chats.”
“I use different models for different tasks.”
“I want the AI to remember the right things.”
“Long conversations become slow or expensive.”
“I do not trust hidden memory.”
“I want to see the prompt and context sent to the model.”
“I need separate context for different clients or projects.”
“I want to switch providers without starting again.”
“I spend too much time improving prompts manually.”

10.3 Weak Early-Adopter Signals
A potential user is weakly qualified when:
They use AI less than once per week.
They only ask isolated general-knowledge questions.
They do not work on continuing tasks.
They are unwilling to configure an AI provider.
They do not care whether information is remembered.
They expect unlimited model usage to be included for free.
They require a fully autonomous assistant at launch.

11. User Segmentation
Gexor users will initially be segmented according to behaviour and requirements rather than only profession.
11.1 Continuity-Driven Users
These users work on ongoing projects and need AI to remember:
Goals
Requirements
Constraints
Decisions
Progress
Preferred methods
Current open questions
Primary product value:
Persistent project continuity.

11.2 Quality-Driven Users
These users want stronger outputs but may not know how to create advanced prompts.
Primary product value:
Automatic prompt and context improvement.

11.3 Provider-Flexible Users
These users switch models based on task, cost, or capability.
Primary product value:
Cross-provider context and memory portability.

11.4 Cost-Conscious Users
These users use provider APIs directly and want visibility into:
Input tokens
Output tokens
Selected models
Context overhead
Estimated cost
Avoidable context
Expensive requests
Primary product value:
Cost-aware AI interaction.

11.5 Control-Driven Users
These users care strongly about:
What the system remembers
Why information was saved
Which memories were used
What was sent to providers
How data can be exported or deleted
Primary product value:
Transparent and reversible AI personalisation.

11.6 Multi-Project Users
These users manage:
Multiple clients
Multiple products
Multiple research topics
Multiple content brands
Multiple development projects
Primary product value:
Isolated workspace-specific intelligence.

12. Primary User Personas
12.1 Persona A — Solo Startup Founder
Profile
Runs or is planning an early-stage startup
Uses AI for product, business, research, and technical tasks
Works across many topics in the same project
Often returns to previous decisions after several days
Current Behaviour
Uses multiple AI chats
Stores some decisions in notes
Repeats project descriptions
Manually copies context between tools
Loses track of which decision was final
Main Problems
Fragmented project context
Contradictory AI recommendations
Repeated explanations
Long and expensive chat histories
Difficulty preserving a single source of project truth
Desired Outcome
The founder wants AI to understand the current product state, previous decisions, constraints, and next priorities without requiring complete re-explanation.
Gexor Value
Project workspace
Decision memory
Requirement memory
Prompt enhancement
Cross-model continuity
Context visibility
Project summaries

12.2 Persona B — Multi-Client Freelancer
Profile
Works independently for several clients
Produces repeated deliverables
Needs different tone, context, and rules for each client
Current Behaviour
Creates separate chats per client
Maintains notes outside the AI platform
Reuses manual prompt templates
Risks mixing client context
Repeats client preferences frequently
Main Problems
Client context is scattered
Tone and formatting become inconsistent
Important client instructions are forgotten
Switching between projects creates errors
Manual prompting consumes time
Desired Outcome
The freelancer wants each client workspace to remember the correct brand, preferences, requirements, and previous decisions.
Gexor Value
Isolated client workspaces
Client-specific memory
Reusable instructions
Output-format preferences
Provider flexibility
Memory traceability

12.3 Persona C — Independent Builder
Profile
Builds software or no-code products independently
Uses AI for planning, coding, debugging, and documentation
May use different models for different technical tasks
Current Behaviour
Uses one model for architecture
Uses another model for coding
Copies technical context manually
Maintains project files separately
Encounters contradictions between sessions
Main Problems
Technical decisions are not consistently remembered
Models receive incomplete architecture context
Context transfer between providers is inefficient
Large code-related chats consume many tokens
Project progress is difficult to summarise
Desired Outcome
The builder wants every connected model to understand the project architecture, stack, decisions, constraints, and current implementation status.
Gexor Value
Technical project memory
Provider-independent context
Model recommendation
Token-aware summaries
Decision tracking
Prompt structuring

12.4 Persona D — Consultant or Analyst
Profile
Works with structured information and professional deliverables
Requires clarity, consistency, and traceability
May manage several engagements simultaneously
Current Behaviour
Uploads information repeatedly
Uses AI to draft and refine reports
Maintains external notes
Verifies outputs manually
Recreates client context for each session
Main Problems
Context fragmentation
Unsupported or inconsistent outputs
Difficulty tracing the basis of a response
Repeated document and client setup
Sensitive information concerns
Desired Outcome
The consultant wants a controlled AI workspace that maintains engagement context and clearly identifies which information influenced an output.
Gexor Value
Engagement workspaces
Source-linked memory
Prompt transparency
Context controls
Structured outputs
Data deletion and export

12.5 Persona E — AI Power User
Profile
Regularly compares and uses multiple AI providers
Understands model strengths and weaknesses
Is sensitive to cost, latency, and model capability
Current Behaviour
Maintains accounts with several providers
Manually switches platforms
Copies prompts and context
Tracks costs separately
Loses continuity when changing models
Main Problems
Provider lock-in
Repeated context migration
No unified memory
Fragmented usage visibility
No consistent prompt layer
Desired Outcome
The power user wants one intelligent workspace for multiple providers with portable memory, transparent prompts, and cost-aware model recommendations.
Gexor Value
Multi-provider connection
Cross-provider memory
Unified usage records
Model selection support
Prompt adaptation
Provider fallback

13. Jobs to Be Done
13.1 Primary Functional Job
When I work with AI on an ongoing task or project, I want the system to automatically supply the right context and instructions so that I receive relevant answers without repeatedly explaining everything.

13.2 Supporting Functional Jobs
Users want Gexor to help them:
Convert rough requests into clear AI instructions
Continue work from previous sessions
Preserve important project decisions
Separate different projects or clients
Select a suitable model
Change providers without losing continuity
Avoid sending irrelevant conversation history
Inspect and correct remembered information
Understand provider usage and cost
Organise AI-assisted work in one place
Reuse stable preferences and instructions
Identify contradictions in stored context
Export or delete their information

13.3 Emotional Jobs
Users want to feel:
Confident that the AI understands the task
In control of what is remembered
Less frustrated by repeated explanations
Safe when switching projects
Comfortable changing providers
Clear about what the system is doing
Confident that important decisions will not be lost
Less dependent on prompt-engineering knowledge

13.4 Social and Professional Jobs
Users want to:
Produce more consistent professional work
Appear organised and responsive
Reduce avoidable mistakes
Complete tasks faster
Maintain client or project standards
Demonstrate traceable decision-making
Use AI without appearing careless or inconsistent

14. Core MVP Use Cases
14.1 Start a New Workspace
The user creates a workspace for:
A startup
A client
A software project
A research topic
A professional engagement
A personal long-term goal
The workspace contains isolated conversations, memories, instructions, and provider preferences.

14.2 Connect an AI Provider
The user:
1. Selects a supported provider.
2. Enters an API key.
3. Receives a clear security explanation.
4. Tests the connection.
5. Selects a default model.
6. Sets a cost-quality preference.
Expected result:
The user can safely use the provider through Gexor.

14.3 Send a Rough Prompt
The user writes a natural, incomplete, or informal request.
Example:
“Make a launch plan for this app.”
Gexor:
1. Detects the current workspace.
2. Retrieves relevant project information.
3. Identifies the task as planning.
4. Applies the selected prompt-enhancement mode.
5. Adds relevant constraints and output structure.
6. Sends the constructed request to the selected provider.
Expected result:
The response is more project-specific and actionable than a context-free response.

14.4 Continue a Project in a New Conversation
The user starts a new chat inside an existing workspace.
Gexor retrieves:
Important project facts
Confirmed decisions
Active constraints
Relevant preferences
Recent project status
Current task-related memories
Expected result:
The user can continue work without pasting the entire previous chat.

14.5 Save an Explicit Memory
The user says:
“Remember that the MVP will support only two providers.”
Gexor:
1. Identifies an explicit memory instruction.
2. Creates a structured project memory.
3. Records its source.
4. Displays confirmation.
5. Makes the memory editable and deletable.
Expected result:
The decision can be reused in future relevant requests.

14.6 Suggest a Memory
The user provides information that may be useful later but does not explicitly ask to save it.
Gexor:
1. Extracts a memory candidate.
2. Classifies the memory.
3. Determines confidence and sensitivity.
4. Suggests the memory for confirmation when required.
Expected result:
Useful information is preserved without silently storing uncertain or sensitive assumptions.

14.7 Automatically Save a Confirmed Memory
Gexor automatically saves a memory when the information is:
Clearly confirmed
Stable
Non-sensitive
Important for workspace continuity
Supported by a reliable source message
Expected result:
The product reduces manual memory management while retaining user control.

14.8 Inspect Used Memory
The user opens the context details for a response.
Gexor displays:
Memories used
Workspace instructions used
Conversation summary used
Selected model
Prompt-enhancement mode
Estimated usage and cost
Expected result:
The user can understand why the response was generated in a particular way.

14.9 Correct or Delete Memory
The user identifies incorrect or outdated memory.
The user can:
Edit it
Delete it
Mark it temporary
Change its workspace
Disable it
Replace it with a newer fact
Expected result:
Incorrect memory does not continue influencing future answers.

14.10 Switch AI Models
The user changes the selected model within the same provider or to another connected provider.
Gexor preserves:
Workspace context
Relevant memories
Conversation objective
Prompt structure
Expected result:
The user receives continuity without manually moving context.

14.11 Review Token and Cost Usage
The user reviews:
Model used
Input tokens
Output tokens
Estimated provider cost
Gexor-added context
Prompt-enhancement overhead
Monthly usage
Expected result:
The user can make informed cost and model decisions.

14.12 Exclude a Conversation from Memory
The user starts or marks a conversation as private or temporary.
Gexor must not:
Extract long-term memories
Use the conversation in unrelated contexts
Include it in workspace summaries unless explicitly permitted
Expected result:
The user can conduct temporary conversations without affecting persistent context.

14.13 Export or Delete Data
The user can:
Export conversations
Export memories
Export workspace data
Delete a conversation
Clear workspace memory
Delete a workspace
Delete their account
Expected result:
The user retains ownership and control over stored information.

15. Future Use Cases
The following use cases are part of the longer-term vision but are not required for the initial MVP:
Uploading and retrieving knowledge from files
Shared team workspaces
Shared and private team memories
Advanced multi-model comparison
Automatic provider fallback
External tool integrations
Scheduled workflows
Agent-based task execution
Email and calendar actions
Browser automation
Local-model execution
Organisation administration
Enterprise audit controls
Public API access
Browser extension
Mobile applications
Voice interaction
Managed AI credits
Future use cases must not be allowed to destabilise the MVP scope.

16. User Goals and Expected Outcomes
16.1 User Goals
Users should be able to:
Start productive AI conversations quickly
Avoid repeatedly explaining stable context
Receive answers aligned with project decisions
Maintain separate contexts for separate projects
Switch models without losing continuity
Control memory behaviour
Understand what information influenced a response
Monitor provider usage
Reduce unnecessary token usage
Export or delete their data

16.2 Expected Product Outcomes
Gexor should produce measurable improvements in:
First-response relevance
Continuity across sessions
Consistency with previous decisions
User confidence in remembered information
Time required to prepare prompts
Context repetition
Provider flexibility
Cost visibility
Workspace organisation
User retention

17. Adoption Barriers
17.1 API-Key Complexity
Some users may not understand:
What an API key is
Where to create it
How provider billing works
Whether the key is safe
How to set usage limits
Required product response:
Provider-specific setup instructions
Connection testing
Clear billing disclosure
Security explanation
Error troubleshooting
Key removal controls

17.2 Memory Trust
Users may fear that Gexor will:
Save incorrect information
Store private information
Use memories in the wrong workspace
Make hidden assumptions
Become difficult to correct
Required product response:
Suggested-memory confirmation
Source traceability
Edit and delete controls
Memory-use explanations
Workspace isolation
Sensitive-memory restrictions

17.3 Cost Uncertainty
Users may not understand the combined effect of:
Provider input tokens
Provider output tokens
Context added by Gexor
Prompt-enhancement calls
Background memory processing
Required product response:
Clear estimated costs
Cost modes
Spending limits
Per-request usage details
Honest disclosure that Gexor does not guarantee lower cost for every request

17.4 Direct-Provider Convenience
Users may prefer existing AI applications because:
They are familiar
They require no API setup
They may include subscription-based usage
They provide native applications
They offer integrated tools
Required product response:
Gexor must provide clear additional value through:
Better continuity
Cross-provider memory
Workspace intelligence
Transparent context
Provider flexibility
User-controlled memory

17.5 Privacy Concerns
Users may hesitate to store:
Business information
Client information
Project decisions
Personal preferences
Provider credentials
Required product response:
Strong workspace isolation
Encrypted credential handling
Minimal data collection
Data export and deletion
Clear privacy documentation
Private-conversation mode

18. User Prioritisation Rules
When product requirements conflict, the MVP will prioritise:
1. Active professional and project-based users
2. Long-running workspace continuity
3. Correct and controllable memory
4. Reliable prompt and context construction
5. Secure provider connection
6. Clear model and cost visibility
7. Ease of use
8. Additional providers
9. Advanced automation
10. Broad consumer features
A feature should receive higher priority when it:
Solves a repeated user problem
Improves the primary product promise
Benefits multiple primary personas
Reduces trust or security risk
Improves measurable answer quality
Supports repeated usage
Can be implemented without excessive complexity
A feature should receive lower priority when it:
Mainly creates visual novelty
Serves a secondary user group
Duplicates provider functionality
Adds major operating cost
Introduces external-action risk
Requires enterprise infrastructure
Does not support the core product hypothesis

19. Section 2 Acceptance Criteria
This section will be considered complete when:
Primary users are clearly defined.
Secondary and excluded users are identified.
Early-adopter characteristics are documented.
User segments are based on meaningful needs.
Primary personas represent the intended market.
Core jobs to be done are defined.
MVP use cases cover the primary product flow.
Future use cases are separated from MVP scope.
Adoption barriers and required responses are documented.
User-prioritisation rules are established.

Gexor — Product Requirements Document
Section 3: MVP Scope, Product Capabilities, Exclusions, and Release Boundaries

20. MVP Objective
20.1 Primary Objective
The objective of the Gexor MVP is to validate whether users receive meaningful value from a provider-independent AI workspace that combines:
Intelligent prompt enhancement
Structured project memory
Relevant context retrieval
Cross-conversation continuity
Model recommendation
Provider flexibility
Token and cost visibility
Transparent user controls
The MVP must prove that Gexor can improve ongoing AI-assisted project work without creating unacceptable increases in:
Response latency
Provider cost
User complexity
Memory errors
Privacy risk
Operational cost

20.2 Core MVP Hypothesis
The central hypothesis is:
Users working on long-running projects will prefer Gexor-enhanced AI interactions because Gexor reduces repeated context, preserves important decisions, and constructs more relevant provider requests.

20.3 Supporting Hypotheses
The MVP will also test whether:
1. Users are willing to connect their own provider API keys.
2. Users trust structured memory when it is visible and controllable.
3. Users value continuity across different conversations.
4. Users value continuity across different AI providers.
5. Prompt enhancement improves perceived answer quality.
6. Users want visibility into the final provider prompt.
7. Users value per-request token and cost information.
8. Project and client workspaces improve organisation.
9. Users will return repeatedly to continue ongoing work.
10. Users are willing to pay separately for Gexor’s intelligence layer.

21. MVP Product Definition
The MVP is a secure web-based AI workspace in which a user can:
1. Create an account.
2. Create a project or client workspace.
3. Connect a supported external AI provider.
4. Select or receive a recommendation for a model.
5. Start and manage conversations.
6. Send natural-language prompts.
7. Allow Gexor to enhance those prompts.
8. Retrieve relevant workspace memories.
9. Receive a streamed AI response.
10. Review the runtime context used.
11. Save, inspect, edit, or delete memories.
12. review token and estimated cost usage.
13. use private chat when persistent memory is not wanted.
14. export or delete their stored data.
The MVP will be delivered initially as a responsive web application.

22. MVP Capability Groups
The MVP will contain the following capability groups:
1. Identity and account management
2. Workspace management
3. Provider connection management
4. Model selection and recommendation
5. Conversation and message management
6. Prompt enhancement
7. Context construction
8. Structured memory
9. Runtime orchestration
10. Response streaming and processing
11. Usage and cost visibility
12. Privacy and data controls
13. Product feedback and basic administration

23. Identity and Account Management
23.1 Required Capabilities
The user must be able to:
Register an account
Sign in
Sign out
Verify their email where required
Reset their password
Maintain a secure session
View basic account settings
Export account data
Delete their account

23.2 Authentication Methods
The MVP should support:
Email and password authentication
Google authentication, where implementation cost remains reasonable
Additional authentication providers are outside the initial scope.

23.3 Account States
Supported account states should include:
Unverified
Active
Suspended
Scheduled for deletion
Deleted
The detailed lifecycle will be defined in the Functional Requirements.

23.4 Account Requirements
Account implementation must provide:
Unique user identity
Secure password handling
Session expiration
Protection against unauthorised access
User-specific data isolation
Complete account-deletion workflow

24. Workspace Management
24.1 Workspace Types
The MVP will support:
Project workspace
Client workspace
A workspace type helps initialise labels and suggested fields but should not create rigid technical limitations.

24.2 Workspace Capabilities
The user must be able to:
Create a workspace
Name a workspace
Select its type
Add a description
Define its objective
Add workspace instructions
Select a default provider
Select a default model
Select a cost-quality preference
Rename a workspace
Archive a workspace
Delete a workspace
Export workspace data

24.3 Workspace Isolation
Each workspace must maintain isolated:
Conversations
Messages
Memories
Instructions
Summaries
Provider preferences
Usage statistics
Runtime records
Information from one workspace must not influence another workspace unless the user explicitly copies or moves it.

24.4 Workspace Overview
Each workspace should display:
Workspace name
Workspace description
Active conversations
Recent conversations
Important memories
Current instructions
Default provider and model
Recent usage
Quick-start chat action
Advanced project-management dashboards are outside the MVP.

25. Provider Connection Management
25.1 Initial Provider Count
The MVP will support two AI providers.
The exact providers will be selected during architecture and implementation planning.
The preferred candidates are:
Google Gemini
OpenAI
Anthropic Claude
The final pair must be selected according to:
API accessibility
Streaming support
Model availability
Structured-output support
Pricing
Documentation quality
Reliability
Target-user demand
Development complexity

25.2 Provider Connection Capabilities
The user must be able to:
Select a provider
Enter an API key
Test the connection
Receive success or failure feedback
View the connection status
Replace the API key
Remove the connection
Select an available model
View provider-billing guidance

25.3 Credential Handling
Provider credentials must:
Never be displayed in full after submission
Never be stored in plain text
Be accessible only through authorised server-side operations
Remain isolated by user
Be removable by the user
Never be included in logs
Never be sent to another provider
Exact encryption and secret-storage requirements will be defined in the Security Documentation.

25.4 Provider Responsibility Disclosure
Gexor must clearly disclose that:
The user’s provider account is separate from Gexor.
Provider usage may generate charges.
Gexor does not control provider pricing.
Provider policies and availability may change.
The user is responsible for provider billing limits.
Gexor cost estimates may not exactly match final provider billing.

26. Model Selection and Recommendation
26.1 Manual Selection
The user must be able to manually select a supported model before sending a request.

26.2 Model Recommendation
Gexor may recommend a model according to:
Task category
Task complexity
Context size
Expected output size
Speed preference
Cost preference
Quality preference
Model availability
Provider capability

26.3 User Control
The user must be able to:
Accept the recommendation
Choose another model
Set a workspace default
Disable recommendations
Select Economy, Balanced, or Best Quality preference
Gexor must not silently route every request to a different model during the MVP without user-visible indication.

26.4 Recommendation Transparency
Where a recommendation is shown, Gexor should provide a short reason such as:
Lower estimated cost
Better suited for coding
Better suited for complex reasoning
Faster expected response
Required context capacity
Preferred workspace model unavailable

27. Conversation Management
27.1 Required Capabilities
The user must be able to:
Start a conversation
View conversation history
Rename a conversation
Delete a conversation
Archive a conversation
Search conversations
Continue a previous conversation
Start a private conversation
View the conversation’s provider and model

27.2 Message Capabilities
The user must be able to:
Send a text message
Receive a streamed response
Stop response generation
Copy a response
Regenerate a response
Edit and resend a previous user message
Provide positive or negative feedback
View runtime details for a response

27.3 Supported Content
The first MVP release will support:
Plain text
Markdown-formatted responses
Code blocks
Basic tables
Links returned by providers
Initial file uploads, image input, voice input, and audio input are outside the first release unless they are added without affecting core delivery.

27.4 Conversation Branching
Full visual conversation branching is not required for the first MVP.
When a user edits and resends an earlier message, the system may:
Create a new continuation
Mark subsequent messages as superseded
Create a new conversation copy
The exact behaviour will be defined in Functional Requirements and UX documentation.

28. Prompt Enhancement
28.1 Enhancement Modes
The MVP will provide:
Off
Auto
Strong

28.2 Off Mode
In Off mode:
Gexor must preserve the user’s semantic request.
Gexor may still attach required security instructions.
Gexor may attach explicitly selected workspace instructions.
Automatic stylistic or structural rewriting should not occur.
Relevant memory usage should be separately configurable or clearly indicated.

28.3 Auto Mode
In Auto mode, Gexor will determine whether the request requires:
No enhancement
Basic clarification
Improved structure
Relevant workspace memory
Output-format instructions
Conversation-summary context
Model recommendation
Simple conversational prompts should not receive unnecessary expansion.

28.4 Strong Mode
Strong mode may add:
Explicit objective
Required context
Constraints
Assumptions
Detailed output structure
Quality requirements
Provider-specific instructions
Relevant confirmed memories
Workspace-specific terminology
Strong mode must not change the user’s underlying intent.

28.5 Prompt Transparency
The user must be able to view:
Original user message
Final provider-ready prompt
Prompt-enhancement mode
Memories included
Workspace instructions included
Model selected

28.6 Prompt-Engine Limitations
The MVP prompt engine will not attempt to:
Guarantee factual accuracy
Circumvent provider safety systems
Automatically execute external actions
Generate hidden autonomous objectives
Expand every prompt into a large template
Replace necessary user clarification in all circumstances

29. Context Construction
29.1 Context Sources
The MVP context engine may use:
Current user message
Recent conversation messages
Conversation summary
Workspace instructions
Relevant workspace memories
User-selected context
Provider and model requirements

29.2 Context Rules
The context engine must:
Use workspace-isolated information
Prefer confirmed memories
Avoid unnecessary context
Remove obvious duplication
Respect private-chat restrictions
Respect disabled memories
Respect context-token limits
Preserve the current user request as the highest-priority task input

29.3 Context Budgeting
The system must maintain a configurable context budget based on:
Model context limit
Expected response length
Required system instructions
Recent messages
Memory relevance
Workspace instructions
Cost preference
The MVP does not need to achieve perfect token optimisation, but it must avoid blindly sending complete history.

29.4 Context Transparency
The runtime-details view should identify:
Recent conversation context used
Summary used
Memories used
Workspace instructions used
Approximate added tokens
Excluded context where relevant

30. Structured Memory
30.1 Memory Categories
The MVP should support the following memory categories:
Project fact
Client fact
Decision
Requirement
Constraint
Preference
Instruction
Entity
Current status
Temporary context
Custom note

30.2 Memory Creation Methods
Memories may be created through:
Explicit user instruction
Automatic extraction
Suggested extraction requiring confirmation
Manual memory entry
Editing an existing memory

30.3 Memory Attributes
Each memory record should include:
Memory content
Memory category
Workspace
Source conversation
Source message
Creation method
Confidence
Confirmation status
Sensitivity level
Creation date
Last updated date
Last used date
Usage count
Active or disabled status
Optional expiry date

30.4 Memory Controls
The user must be able to:
View memories
Search memories
Filter memories
Add a memory
Edit a memory
Delete a memory
Disable a memory
Confirm a suggested memory
Reject a suggested memory
View a memory’s source
See when a memory was last used
Clear workspace memories

30.5 Memory Retrieval
Memory retrieval must consider:
Workspace match
Task relevance
Memory status
Confirmation status
Confidence
Recency
Importance
Category
User restrictions
Token budget
The MVP may initially use structured filtering and text-based relevance before introducing advanced vector retrieval.

30.6 Memory Conflict Handling
When a new memory conflicts with an active memory, the system should:
Avoid silently treating both as true
Identify the conflict
Prefer explicit recent user confirmation
Ask the user to resolve important conflicts
Preserve source history where practical
Mark outdated memory as replaced rather than immediately destroying audit history
Unresolved conflict fallback:
If the user continues chatting without selecting a conflict-resolution option, the prompt generation pipeline must not block, fail, or crash.
For active prompt injection only, the Context Engine must treat the chronologically most recent user statement as authoritatively true.
The older conflicting memory must remain stored and marked as part of an unresolved conflict rather than being silently deleted or overwritten.
The unresolved conflict flag must remain visible in the database and workspace UI until the user explicitly resolves or clears it.
The fallback decision and the memory sources used must remain traceable in runtime details and logs.

31. Private and Temporary Chat
31.1 Private Chat Requirement
The user must be able to start a conversation in private mode.
Private mode must be visibly indicated.

31.2 Private Mode Behaviour
In private mode:
Persistent memory extraction is disabled.
Existing workspace memories may be disabled by default.
The user may explicitly choose whether existing memory can be read.
The conversation must not update workspace summaries.
The conversation must not create project decisions.
The conversation must not influence unrelated future requests.

31.3 Persistence Options
The MVP may support:
Private but saved conversation
Temporary non-persistent conversation
If temporary non-persistent conversations cannot be securely delivered in the first release, private-but-saved mode will be the minimum launch requirement.

32. Runtime Orchestration
32.1 MVP Runtime Responsibilities
The runtime orchestrator will coordinate:
1. Authentication and workspace validation
2. User-message acceptance
3. Private-mode checks
4. Intent and complexity classification
5. Prompt-enhancement selection
6. Memory retrieval
7. Context construction
8. Model recommendation or selection
9. Provider request execution
10. Response streaming
11. Token and usage recording
12. Background memory processing
13. Error and retry handling

32.2 Execution Strategy
The MVP will prioritise single-provider-call execution.
Additional model calls should only be used when justified for:
Memory extraction
Task classification
Prompt enhancement
Response processing
The MVP will not use complex multi-agent plans by default.

32.3 Background Processing
Background processing may perform:
Memory-candidate extraction
Conversation-summary updates
Usage aggregation
Feedback processing
Runtime logging
Memory deduplication
Conflict detection
Background failures must not erase or invalidate an already delivered provider response.

32.4 Snapshot Lock for Rapid-Fire Messages
The runtime orchestrator must not block the active chat pipeline when background processing from the immediately preceding message is still incomplete.
If the user sends Message B while the background worker is still extracting memories, updating summaries, or processing data from Message A, Gexor must apply a Snapshot Lock to the context used for Message B.
Under the Snapshot Lock:
Message B must be accepted and sent without waiting for Message A background processing to complete.
The Context Engine must use the pre-existing active workspace memories, summaries, and instructions available at the exact moment the Message B context snapshot is created.
Background processing must not mutate the already assembled context snapshot for Message B.
Any newly extracted memories or summary updates from Message A must become active only after their background transaction completes successfully.
The newly committed information from Message A becomes eligible for retrieval beginning with the subsequent prompt, Message C.
The runtime should record the context snapshot or version used for each request so the behaviour remains traceable and testable.
This rule intentionally accepts that Message B may not include memory extracted from Message A in exchange for preserving chat responsiveness and deterministic context behaviour.

33. Response Streaming and Processing
33.1 Streaming
Provider responses should be streamed when supported.
The user should see the response begin without waiting for background memory extraction.

33.2 Response Presentation
Gexor should support:
Markdown
Lists
Headings
Code blocks
Tables
Copy actions
Regeneration
Runtime details
User feedback

33.3 Response Processing
The MVP may process provider responses for:
Safe rendering
Usage recording
Memory-candidate extraction
Decision extraction
Summary updates
Basic formatting normalisation
Gexor must not silently alter the provider’s substantive answer after it has been generated unless the transformation is disclosed.

34. Usage and Cost Visibility
34.1 Per-Request Information
Where provider data is available, Gexor should display:
Provider
Model
Input tokens
Output tokens
Total tokens
Estimated provider cost
Response latency
Prompt-enhancement mode
Approximate Gexor context overhead

34.2 Usage Dashboard
The MVP usage dashboard should provide:
Requests by provider
Requests by model
Token totals
Estimated cost totals
Workspace usage
Current-month usage
Recent expensive requests

34.3 Cost Preferences
The user should be able to select:
Economy
Balanced
Best Quality
The user may also set:
Preferred provider
Preferred model
Optional warning threshold
Optional maximum estimated request cost
Hard provider-side spending limits remain the responsibility of the provider unless Gexor can reliably enforce a local limit before execution.

35. Privacy and Data Controls
35.1 User Controls
The user must be able to:
Delete a conversation
Delete a memory
Clear workspace memory
Delete a workspace
Remove a provider connection
Export workspace data
Export account data
Delete the account
Start a private conversation

35.2 Data Deletion
Deletion behaviour must clearly distinguish:
Immediate removal from the user interface
Background deletion processing
Backup retention
Audit or legal retention
Provider-side data retention
When a user requests account or workspace deletion, all associated data must be soft-deleted immediately, making it unavailable in the application interface and normal runtime processing.
Gexor must permanently hard-purge all associated rows, assets, metadata, cached background queues, and copies contained in Gexor-controlled system backups within exactly 30 days of the deletion request.
The deletion workflow must record the request timestamp, immediate soft-deletion status, hard-purge deadline, and final purge-completion timestamp.
The 30-day time bound applies to data controlled by Gexor. Data previously transmitted to an external AI provider remains subject to that provider’s independent retention and deletion policies.

35.3 Data Export
The MVP should export common data in machine-readable and human-readable formats where practical.
Exportable data should include:
Workspace information
Conversations
Messages
Memories
User-created instructions
Usage history
Provider API keys must never be included in exports.

36. Feedback and Basic Administration
36.1 User Feedback
Users should be able to report:
Helpful response
Unhelpful response
Incorrect memory
Irrelevant memory
Prompt-enhancement problem
Provider error
Cost concern
General product feedback

36.2 Basic Administration
Internal administration must support:
Viewing system-health information
Reviewing provider failures
Reviewing reported issues
Suspending abusive accounts
Monitoring aggregate usage
Monitoring infrastructure cost
Investigating security incidents
Administrative access must not permit casual unrestricted inspection of private user content.

37. Explicit MVP Exclusions
The following capabilities are excluded from the initial MVP unless separately approved.
37.1 Advanced AI Capabilities
Multi-agent teams
Autonomous task execution
Browser-control agents
Computer-use agents
Long-running autonomous workflows
Automatic external actions
AI-generated tool chains
Complex planner-executor systems
Multi-model consensus generation

37.2 Knowledge and Files
Large document knowledge bases
PDF question answering
Cloud-drive synchronisation
Website crawling
Continuous knowledge refresh
Advanced semantic document search
OCR pipelines
Large-scale embedding infrastructure
Basic file support may be evaluated after the memory-chat foundation is stable.

37.3 Collaboration
Multi-user workspaces
Workspace roles
Team invitations
Shared billing
Approval workflows
Comments and mentions
Shared private memories
Organisation administration

37.4 Integrations
Gmail
Google Calendar
Slack
GitHub
Notion
Google Drive
Zapier
Make
n8n
Browser extensions
Public developer API

37.5 Media and Modalities
Image generation
Image analysis
Audio generation
Speech-to-text
Text-to-speech
Video generation
Real-time voice conversation

37.6 Platform Expansion
Native Android app
Native iOS app
Desktop application
Offline mode
On-premise deployment
Local-model execution
Enterprise private cloud
The responsive web application may be made installable as a PWA after web stability is demonstrated.

37.7 Commercial Expansion
Managed AI credits
Provider token resale
Enterprise contracts
White-label deployment
Marketplace
Template marketplace
Affiliate provider billing
Usage-based AI markup

38. MVP Release Boundaries
38.1 Internal Prototype
The internal prototype must demonstrate:
Authentication
One workspace
One provider
Basic chat
Streaming
Message storage
Manual memory
Basic prompt enhancement
Usage logging
It is not a public product.

38.2 Private Alpha
Private alpha should add:
Second provider
Structured memory extraction
Memory controls
Prompt-enhancement modes
Model recommendation
Private chat
Runtime-details view
Basic usage dashboard
Data deletion
Error monitoring
Private alpha access will be invitation-only.

38.3 Closed Beta
Closed beta should include:
Improved onboarding
Provider setup guidance
Memory conflict handling
Workspace export
Account deletion
Usage and cost warnings
Feedback collection
Improved security testing
Reliability monitoring
Basic pricing experiments

38.4 Public MVP
Public MVP release requires:
Stable provider connections
Reliable streaming
Tested user isolation
Encrypted credential handling
Correct workspace isolation
Usable memory controls
Private-chat support
Data export and deletion
Error monitoring
Rate limiting
Privacy policy
Terms of service
Support channel
Backup and recovery procedures
Production deployment process

39. MVP Launch Gates
Gexor must not launch publicly until the following conditions are met:
Product Gates
Primary user journey works end to end.
Users can connect at least two providers.
Users can create and manage workspaces.
Prompt enhancement works in all three modes.
Memory can be created, inspected, corrected, and deleted.
Private mode prevents persistent memory extraction.
Users can view runtime details.
Users can view basic usage and estimated costs.

Security Gates
API keys are not stored in plain text.
Cross-user data-access tests pass.
Cross-workspace isolation tests pass.
Authentication and authorization tests pass.
Sensitive values are excluded from logs.
Rate limiting is enabled.
Account and data deletion are tested.
Security-critical dependencies are reviewed.

Reliability Gates
Provider errors are handled clearly.
Streaming failures do not corrupt conversations.
Background-job failures are recoverable.
Database backups exist.
Production rollback procedure exists.
Critical errors trigger alerts.
Usage data is not silently lost.

Quality Gates
Prompt enhancement does not routinely change user intent.
Memory retrieval does not routinely use unrelated memories.
Incorrect memories can be corrected immediately.
Direct-provider and enhanced-response comparisons are conducted.
Early users demonstrate repeat usage.
Serious user-reported memory problems are resolved.

40. MVP Completion Definition
The MVP will be considered complete when:
1. A target user can register successfully.
2. The user can create a project or client workspace.
3. The user can connect a supported provider securely.
4. The user can start a conversation.
5. Gexor can enhance the prompt according to the selected mode.
6. Relevant workspace memory can be retrieved.
7. A response can be streamed from the selected provider.
8. Usage and estimated cost can be recorded.
9. Useful memory candidates can be processed after the response.
10. The user can inspect and control memories.
11. The user can use private mode.
12. The user can switch supported models or providers.
13. The user can export and delete stored data.
14. The system meets defined security and reliability launch gates.
15. Early users demonstrate that Gexor improves project continuity.

41. Scope-Control Rules
Any proposed MVP feature must answer:
1. Does it directly support the primary promise?
2. Does it solve a repeated problem for primary users?
3. Is it required for security, trust, or reliability?
4. Can the MVP launch without it?
5. Does it create major technical complexity?
6. Does it increase operating cost materially?
7. Does it require another major system?
8. Can it be tested clearly?
9. Will users notice and value it?
10. Should it be postponed until after validation?
A feature should be removed or postponed when it:
Does not improve project continuity
Does not improve answer quality
Does not improve trust or control
Serves only a small secondary segment
Requires disproportionate infrastructure
Delays the primary runtime
Creates external-action risk
Duplicates existing provider functionality

42. Section 3 Acceptance Criteria
This section is complete when:
The MVP objective is measurable.
Included capabilities are clearly listed.
Each major capability has defined boundaries.
Provider and model behaviour is defined.
Prompt-enhancement modes are defined.
Context and memory responsibilities are defined.
Private-mode requirements are documented.
Usage and cost visibility are included.
Explicit exclusions are recorded.
Release stages are separated.
Public launch gates are established.
MVP completion has a clear definition.

Gexor — Product Requirements Document
Section 4: Product Experience, User Journeys, Interaction Requirements, and User States

43. Product Experience Objective
Gexor must present complex AI runtime capabilities through a familiar and understandable interface.
The user should experience Gexor primarily as a clean AI workspace rather than as a collection of technical engines.
Internal capabilities such as:
Intent classification
Prompt construction
Context retrieval
Memory ranking
Token budgeting
Provider routing
Background processing
Memory extraction
should operate without requiring the user to understand their internal implementation.
However, users must be able to inspect important runtime decisions when they want greater control or transparency.
The product experience must balance:
Simplicity
Intelligence
Transparency
User control
Speed
Security
Cost awareness

44. Experience Principles
44.1 Familiar First Experience
The main chat interface should feel familiar to users of existing AI chat applications.
The initial experience should not require users to understand:
AI orchestration
Retrieval systems
Embeddings
Prompt-engineering syntax
Context windows
Memory confidence scoring
Provider adapter architecture
Advanced information should remain available through optional views.

44.2 Progressive Disclosure
Gexor should reveal complexity gradually.
The default interface should show:
Workspace
Conversation
Selected provider
Selected model
Prompt mode
Memory status
Message input
Advanced runtime information should appear through expandable views such as:
Context used
Memories used
Final prompt
Token usage
Cost estimate
Routing reason
Response latency

44.3 User Control Without Constant Interruption
Gexor should not require confirmation for every normal action.
The product should automatically handle low-risk operations while requesting confirmation for:
Sensitive memory creation
Conflicting memories
High-cost requests
Provider-key removal
Workspace deletion
Account deletion
Significant irreversible actions

44.4 Clear System Status
The user should always understand whether Gexor is:
Connecting to a provider
Enhancing a prompt
Retrieving memory
Waiting for the provider
Streaming a response
Processing memories in the background
Experiencing an error
Retrying a request
Status indicators should be understandable and should not expose unnecessary technical detail.

44.5 Reversible Actions
Where practical, the user should be able to reverse:
Memory creation
Memory edits
Memory deletion for a short recovery period
Workspace archival
Conversation archival
Model recommendation
Prompt-enhancement selection
Permanent actions must clearly explain their consequences.

45. Information Architecture
45.1 Primary Navigation
The MVP should contain the following primary areas:
1. Home
2. Workspaces
3. Conversations
4. Memories
5. Providers
6. Usage
7. Settings
8. Help and Feedback

45.2 Home
The Home page should provide:
Recent workspaces
Recent conversations
Continue-work shortcuts
Provider-connection status
Recent usage summary
Suggested next actions
Create workspace action
Start private chat action
The Home page must not become a complex analytics dashboard during the MVP.

45.3 Workspaces
The Workspaces area should allow users to:
View active workspaces
Create a workspace
Search workspace names
Filter by workspace type
Open a workspace
Archive a workspace
Delete a workspace
Export workspace data

45.4 Workspace Detail
Each workspace should contain:
Overview
Conversations
Memories
Instructions
Provider and model preferences
Usage
Workspace settings

45.5 Conversations
The Conversations area should allow users to:
View recent conversations
Search conversation titles
Filter by workspace
Open a conversation
Rename a conversation
Archive a conversation
Delete a conversation
Start a new conversation

45.6 Memories
The Memories area should allow users to:
View all memories
Filter by workspace
Filter by category
Search memory content
View suggested memories
View confirmed memories
View disabled memories
Add a memory manually
Edit a memory
Delete a memory
Inspect its source
Review conflicting memories

45.7 Providers
The Providers area should allow users to:
Connect Gemini
Connect OpenAI
Test connections
View connection status
Replace credentials
Remove credentials
View supported models
Access provider setup instructions
Review provider billing guidance

45.8 Usage
The Usage area should show:
Current month usage
Provider usage
Model usage
Workspace usage
Input tokens
Output tokens
Estimated provider cost
Recent expensive requests
Warning and hard-block preferences

45.9 Settings
Settings should contain:
Profile
Authentication
Default provider
Default model
Prompt-enhancement preference
Memory preference
Cost preference
Privacy preference
Data export
Account deletion

46. First-Time User Journey
46.1 Entry
The user arrives through:
Product landing page
Invitation link
Referral
Direct application URL
The landing page should explain:
What Gexor does
What Gexor does not do
That users connect their own AI provider
That provider usage may create separate charges
That Gexor manages memory, context, and prompt intelligence
That the public beta is initially free

46.2 Registration
The user can register using:
Google authentication
Email and password
The user must accept:
Terms of service
Privacy policy
Provider-cost disclosure

46.3 Welcome Experience
After registration, the user should see a short explanation:
Gexor helps your connected AI models remember the right project context, improve rough prompts, and maintain continuity across conversations.
The welcome experience should avoid technical engine terminology.

46.4 Provider Setup
The user chooses:
Connect Gemini
Connect OpenAI
Skip for now
If the user selects a provider, Gexor provides:
1. Provider-specific setup instructions
2. API-key creation guidance
3. Billing explanation
4. Security explanation
5. Credential entry
6. Connection test
7. Default-model selection
The API key must be masked immediately after entry.
Provider onboarding must include an integrated Check Key Status macro.
The macro must validate authentication, provider access, available-model permission, quota or billing status, and provider availability while avoiding unnecessary paid generation wherever practical.
When validation fails, Gexor must map the provider error code to specific corrective guidance rather than returning a generic connection failure.
If the provider returns insufficient_quota or billing_hard_limit_reached, Gexor must display exactly:
“Your external AI provider account balance is ₹0 or has hit its billing limit. Please check your billing profile directly with OpenAI/Google.”

46.5 First Workspace Setup
The user selects:
Project workspace
Client workspace
The user enters:
Workspace name
Optional description
Main objective
Optional initial instructions
Default provider
Default model
Cost-quality preference
The user should be able to skip optional fields.

46.6 Memory Preference
The user selects a memory behaviour:
Balanced
Confirmation-focused
Manual only
The recommended default should be Balanced.
The onboarding interface must explain that memories remain:
Visible
Editable
Deletable
Workspace-specific
Linked to their source

46.7 First Conversation
Gexor should offer an example prompt related to the workspace.
For a project workspace:
Explain what you are building and what decision you want help with.
For a client workspace:
Explain the client, their goals, and the current task.
Gexor should then demonstrate:
Prompt enhancement
Relevant workspace context
Streamed response
Runtime-details view
Memory suggestion or creation

46.8 Onboarding Completion
Onboarding is complete when the user has:
Created an account
Connected at least one provider
Created one workspace
Sent one successful request
Seen how memory works
Users who skip provider setup should see a clear action to complete it later.

47. Returning User Journey
A returning user should be able to:
1. Sign in.
2. See recent workspaces and conversations.
3. Open an active workspace.
4. Continue a previous conversation or start a new one.
5. Send a request without repeating stable context.
6. Receive a response using relevant workspace information.
7. Review newly created or suggested memories.
8. Monitor usage when required.
The shortest path from login to sending a message should require minimal interaction.

48. Workspace Creation Journey
48.1 Start
The user selects:
Create Workspace

48.2 Workspace Type
The user selects:
Project
Client
The type changes suggested field labels but not the underlying security model.

48.3 Core Details
Required:
Workspace name
Optional:
Description
Objective
Current status
Instructions
Default provider
Default model
Cost preference

48.4 Initial Context
The user may add initial context manually.
Examples:
Product objective
Client background
Technical stack
Writing style
Important restrictions
Current milestone
Initial context should be stored as structured workspace instructions or memories rather than as an uncontrolled block where possible.

48.5 Completion
After creation, the user lands inside the new workspace and sees:
Start conversation
Add memory
Edit instructions
Connect provider if missing

49. Provider Connection Journey
49.1 Select Provider
The user selects Gemini or OpenAI.

49.2 Understand Responsibility
Before entering credentials, the user must see:
Gexor does not provide the provider account.
Provider billing is separate.
The user should configure provider-side spending limits.
API credentials must not be shared publicly.
The key can be removed from Gexor at any time.

49.3 Enter Credential
The credential field must:
Hide entered characters
Prevent accidental browser exposure where practical
Never redisplay the complete key
Prevent credentials from appearing in analytics or logs

49.4 Test Connection
Gexor should validate:
Credential format where possible
Provider authentication
Basic API access
Available model access
The test should avoid unnecessary paid token consumption.

49.5 Connection Result
Success state:
Provider connected
Connection timestamp
Available models
Select default model
Failure state:
Invalid credential
Permission problem
Provider quota problem
Billing problem
Network or provider failure
Unknown error
Errors should include corrective guidance.

49.6 Check Key Status and Diagnostic Error Mapping
The Check Key Status macro must be available during provider onboarding and callable during active chat processing whenever provider authentication, quota, billing, model access, or permission status is uncertain.
The macro should distinguish at minimum:
Invalid or revoked credential
Missing model or project permission
Insufficient quota
Billing hard limit reached
Provider rate limit
Provider outage or network failure
Unsupported or retired model
Unknown provider error
Provider-side error codes must be mapped to actionable user guidance and must remain available in internal diagnostics without exposing secrets.
For insufficient_quota or billing_hard_limit_reached, the user-facing message must be:
“Your external AI provider account balance is ₹0 or has hit its billing limit. Please check your billing profile directly with OpenAI/Google.”
During active chat processing, a failed key-status check must preserve the user’s unsent or failed message and offer actions to recheck the key, replace the key, open provider billing guidance, or switch to another connected provider.

50. New Conversation Journey
50.1 Conversation Creation
The user may start a conversation from:
Home
Workspace
Conversation list
Continue-work suggestion
A normal conversation must belong to one workspace.

50.2 Runtime Preferences
Before or during the conversation, the user can select:
Provider
Model
Prompt mode
Memory retrieval status
Cost-quality mode
Defaults should come from workspace settings.

50.3 Message Composition
The input area should support:
Multi-line text
Send action
Keyboard shortcut
Character or token warning for extremely large inputs
Prompt-mode indicator
Memory-status indicator

50.4 Pre-Send Behaviour
Gexor may perform lightweight local or server-side checks for:
Empty input
Excessive length
Missing provider
Invalid provider connection
Hard cost limit
Workspace access
Private-mode settings
The user should not be shown unnecessary processing steps for normal requests.

50.5 Response Generation
After sending:
1. The message appears immediately.
2. Gexor prepares the provider request.
3. A clear processing state is shown.
4. Provider output begins streaming.
5. The user can stop generation.
6. Usage data is recorded.
7. Background processing begins after response delivery.
Rapid-fire message behaviour:
If the user sends Message B before background processing for Message A completes, the interface must accept Message B immediately and must not display a blocking memory-processing state.
Gexor must apply a Snapshot Lock and generate Message B using the workspace context that was active at that exact moment.
Memories extracted from Message A become available only after safe background completion and may influence the next prompt, Message C.
The user may continue chatting normally while background memory work remains in progress.

50.6 Post-Response Actions
The user may:
Copy
Regenerate
Give feedback
Inspect runtime details
Save an explicit memory
Continue the conversation
Change model
Edit and resend their previous message

51. Prompt Enhancement Experience
51.1 Off Mode
The interface should indicate:
Prompt Enhancement: Off
The system should not rewrite the semantic request.
Memory retrieval remains controlled separately.

51.2 Auto Mode
The interface should indicate:
Prompt Enhancement: Auto
Gexor decides whether enhancement is necessary.
The user does not need to approve routine enhancement before every request.

51.3 Strong Mode
The interface should indicate:
Prompt Enhancement: Strong
The system may create a more detailed provider-ready request.
The user must still be able to inspect the final prompt after sending.

51.4 Enhancement Failure
If prompt enhancement fails:
Gexor should not lose the user’s message.
The user should be offered direct-send fallback where safe.
The error should be logged.
The interface should explain that enhancement was unavailable.

52. Memory Interaction Journey
52.1 Explicit Memory
When the user says:
Remember that the first release supports Gemini and OpenAI.
Gexor should:
1. Detect an explicit instruction.
2. Create a structured memory.
3. Show a confirmation notification.
4. Allow immediate undo.
5. Link the memory to its source message.

52.2 Automatic Memory
When a clear, stable, confirmed, non-sensitive fact is detected:
1. The system creates a memory candidate.
2. It assigns category and confidence.
3. It checks for duplicates and conflicts.
4. It saves the memory when automatic-save requirements are met.
5. It informs the user through a non-disruptive notification.

52.3 Suggested Memory
For uncertain, inferred, changing, or sensitive information:
1. The system creates a suggested memory.
2. The user sees:
Proposed memory
Category
Source
Reason it may be useful
3. The user can:
Confirm
Edit and confirm
Reject
Ignore temporarily

52.4 Memory Used in a Response
The runtime-details view should show:
Memory text
Memory category
Source
Why it was considered relevant
Whether it was confirmed or inferred
The user may disable or correct the memory directly from this view.

52.5 Memory Conflict
When two important memories conflict, the user should see:
Existing memory
New memory candidate
Source of each
Creation date
Resolution options
Resolution options:
Keep existing
Replace existing
Keep both with conditions
Edit manually
Mark unresolved
If the user dismisses or ignores the conflict prompt and continues the conversation:
Gexor must continue prompt generation without blocking or crashing.
The Context Engine must use the chronologically most recent user statement as the authoritative value for the active request.
The workspace must continue showing the unresolved conflict until the user explicitly resolves it.
The UI should indicate which recent statement is being used as the temporary active truth.
Neither conflicting record should be permanently removed solely because the fallback was applied.

52.6 Memory Deletion
Before deleting an important memory, Gexor should explain:
Future responses will no longer use it.
Source conversation will remain unless separately deleted.
Deletion may be reversible for a limited period where supported.

53. Private Chat Journey
53.1 Start Private Chat
The user selects:
Start Private Chat
The interface must clearly indicate private mode.

53.2 Default Behaviour
By default:
Existing workspace memories are not read.
New persistent memories are not created.
Workspace summaries are not updated.
Decisions are not extracted into long-term memory.

53.3 Optional Existing-Memory Access
The user may enable:
Use existing workspace memory in this chat.
This allows memory reading only.
It must not allow new persistent memory creation.

53.4 Private Conversation Storage
The MVP minimum requirement is:
Private conversation may remain saved in chat history.
It remains excluded from persistent memory processing.
A later version may support fully temporary sessions that are not stored after completion.

53.5 Private Mode Visibility
Private mode should remain visibly active throughout the conversation.
The interface must prevent the user from accidentally assuming memory is disabled when it is not.

54. Model Recommendation Journey
54.1 Recommendation Trigger
Gexor may recommend a model when:
The current model appears unnecessarily expensive
The task requires stronger reasoning
The task requires a larger context window
A faster model is suitable
The selected model is unavailable
Workspace cost preference suggests another model

54.2 Recommendation Presentation
A recommendation should contain:
Recommended model
Short reason
Estimated relative cost
Expected speed category
User override
Example:
Recommended: Gemini model X — suitable for this task and expected to cost less than your current selection.

54.3 User Control
The user may:
Accept once
Keep current model
Set recommendation as workspace default
Disable recommendations
The selected model must remain visible during response generation.

55. Cost-Control Journey
55.1 Cost Preferences
The user may select:
Economy
Balanced
Best Quality

55.2 Request Cost Warning
When the estimated cost exceeds the user’s warning threshold, Gexor should display:
Estimated input cost
Estimated output-cost range
Selected model
Main cost drivers
Continue action
Select cheaper model action
Reduce context action where practical

55.3 Hard Block
When a reliable estimate exceeds the user’s hard limit:
The request must not be sent automatically.
The user should be able to choose a cheaper model.
The user may reduce context.
The user may temporarily override the block after explicit confirmation where allowed.

55.4 Cost Estimate Disclaimer
The interface must state that:
Estimates are approximate.
Final provider charges may differ.
Provider-side billing remains authoritative.

56. Error Experience
56.1 Error Principles
Errors must be:
Clear
Actionable
Non-technical where possible
Preserving of user input
Traceable internally
Safe from secret disclosure

56.2 Provider Authentication Error
The user should see:
Provider connection failed
Likely credential or permission issue
Test connection action
Replace credential action
Setup guide link

56.3 Provider Quota or Billing Error
The user should see:
Provider rejected the request
Possible quota or billing cause
Provider billing-dashboard guidance
Switch provider or model action

56.4 Provider Availability Error
The user should be able to:
Retry
Select another model
Select another connected provider
Preserve the unsent message
Automatic fallback may be introduced later after user trust is established.

56.5 Background Processing Error
If response delivery succeeds but memory processing fails:
The response must remain available.
The conversation must not be marked failed.
Gexor may retry background processing.
The user should only be notified when action is required.

56.6 Security or Access Error
The system must not reveal whether another user’s protected resource exists.
Access errors should return a generic authorised-access message while recording sufficient internal detail for investigation.

57. Empty States
57.1 No Workspace
Show:
What a workspace is
Create project workspace
Create client workspace

57.2 No Provider
Show:
Provider connection explanation
Connect Gemini
Connect OpenAI
Provider billing disclosure

57.3 No Conversation
Show:
Start conversation
Example prompts
Workspace-specific suggestions

57.4 No Memory
Show:
What Gexor memory stores
What it does not store
Add memory manually
Start a conversation
Memory-control explanation

57.5 No Usage
Show:
Usage will appear after provider requests
Provider charges remain separate
Cost-setting shortcut

58. Loading and Processing States
The system should distinguish:
Loading page data
Testing provider connection
Preparing request
Waiting for provider
Streaming response
Stopping response
Saving memory
Processing memory candidate
Exporting data
Deleting data
Long operations must provide progress or status feedback where practical.

59. Notifications
Gexor may use in-app notifications for:
Provider connected
Provider connection failed
Memory saved
Memory suggested
Memory conflict detected
Export ready
Deletion scheduled
Cost threshold reached
Background processing requires attention
Notifications should be:
Relevant
Dismissible
Non-disruptive
Linked to an action where required
Email notifications should remain minimal during the MVP.

60. Responsive Web Requirements
The MVP must work on:
Desktop web
Tablet web
Mobile web
The desktop experience may provide the most complete workspace layout.
Mobile web must support the core journey:
Sign in
Select workspace
Start conversation
Send message
View response
Change model
Control memory
Use private mode
Inspect basic usage
Advanced administration may be optimised primarily for desktop.

61. Accessibility Requirements
The product should support:
Keyboard navigation
Visible focus states
Screen-reader labels
Sufficient text contrast
Semantic headings
Accessible form labels
Clear error messages
Non-colour-only status indicators
Scalable text
Reduced-motion preferences where practical
Detailed accessibility targets will be defined in Non-Functional Requirements.

62. User-Control Hierarchy
When Gexor automation conflicts with explicit user settings, priority should be:
1. Security and legal restrictions
2. Explicit current-message instruction
3. Private-mode restrictions
4. Explicit workspace setting
5. Explicit account preference
6. Confirmed workspace memory
7. Confirmed general preference
8. Automatic recommendation
9. Default system behaviour
The system must not override explicit user intent merely because an older memory suggests another preference.

63. Product Experience Success Criteria
The product experience should be considered successful when primary users can:
Complete onboarding without direct founder assistance
Connect a provider successfully
Understand separate provider billing
Create a workspace
Start a conversation
Understand prompt and memory controls
Continue a project without repeating major context
Inspect and correct memory
Use private chat confidently
Understand model and cost information
Recover from common provider errors
Export or delete their data

64. Section 4 Acceptance Criteria
This section is complete when:
Primary navigation is defined.
First-time and returning-user journeys are documented.
Workspace creation is defined.
Provider connection is defined.
Conversation behaviour is defined.
Prompt-enhancement interaction is defined.
Memory creation, suggestion, conflict, and deletion are defined.
Private-chat behaviour is defined.
Model recommendation is defined.
Cost warning and hard-block behaviour are defined.
Error, loading, notification, and empty states are documented.
Responsive and accessibility expectations are established.

Gexor — Product Requirements Document
Section 5: Business Model, Commercial Strategy, Product Metrics, Validation, and Growth

65. Business Model Objective
Gexor will operate as a provider-independent software-as-a-service platform.
Gexor’s primary commercial value comes from the intelligence layer surrounding external AI models, including:
Structured memory
Prompt enhancement
Context management
Provider-independent continuity
Model recommendation
Token and cost visibility
Workspace organisation
Privacy and user controls
Gexor will not initially make money by:
Training its own foundation model
Reselling provider tokens
Adding hidden markups to user API usage
Selling user conversations
Selling user memories
Advertising inside private workspaces
Locking user data to one provider

66. Bring Your Own Key Commercial Model
66.1 Core Model
Users will connect their own supported AI-provider API keys.
The user will have two separate commercial relationships:
1. Gexor subscription or product access
2. AI-provider API billing
Gexor will charge for:
Runtime intelligence
Memory management
Workspace functionality
Provider interoperability
Cost controls
Advanced context management
Future integrations and collaboration
The external provider will charge for:
Input tokens
Output tokens
Model-specific usage
Provider-specific tools
Provider account fees where applicable

66.2 BYOK Benefits
The BYOK model provides:
Lower direct inference liability for Gexor
Transparent provider billing
User control over selected providers
Easier provider switching
Reduced dependency on one model vendor
Ability for users to configure provider-side limits
Clear separation between software cost and model cost

66.3 BYOK Limitations
The BYOK model introduces:
More difficult onboarding
Provider-account setup requirements
Separate billing complexity
Provider quota and permission errors
User concern about API-key security
Different model availability by account or region
Greater customer-support requirements
Gexor must address these limitations through:
Guided setup
Security explanations
Connection testing
Provider billing guidance
Error diagnosis
Cost transparency
Easy credential removal

67. Public Beta Commercial Strategy
67.1 Initial Public Beta
The initial public beta will be free to use.
Users will continue paying their connected AI providers directly.
The free public beta exists to validate:
Product usefulness
User retention
Memory reliability
Prompt-enhancement quality
BYOK willingness
Provider setup success
Infrastructure cost
Support requirements
Willingness to pay

67.2 Beta Limitations
Gexor may apply reasonable free-beta limitations such as:
Limited number of active workspaces
Limited stored memories
Limited conversation retention
Limited background processing
Fair-use rate limits
Limited export frequency
Restricted access to experimental features
Limits must be disclosed clearly.
The beta must not create the impression that all future functionality will remain free.

67.3 Paid Launch Trigger
Paid subscriptions should not become mandatory until Gexor demonstrates:
Repeat weekly usage
Meaningful project continuity
Acceptable memory accuracy
Stable provider connections
Understandable operating costs
User willingness to pay
Sufficient product reliability
A support process capable of handling paying users

68. Future Subscription Structure
The initial paid structure may contain the following plans.
68.1 Free Plan
Intended for:
Product discovery
Light personal use
Basic validation
New-user onboarding
Possible limits:
One active workspace
Limited memory records
Limited runtime history
Basic prompt enhancement
Two supported providers
Basic cost visibility
Community or email support

68.2 Personal Plan
Intended for:
Individual professionals
Freelancers
Students with long-running work
Light project users
Possible capabilities:
Multiple workspaces
Increased memory limits
Full prompt modes
Advanced runtime details
Data export
Usage history
Cost warnings
Priority background processing

68.3 Pro Plan
Intended for:
Founders
Independent builders
Consultants
AI power users
Heavy project users
Possible capabilities:
Higher or flexible workspace limits
Advanced memory controls
Advanced model recommendations
Cost hard limits
Expanded usage analytics
Faster background processing
Early access to additional providers
Future file and knowledge features
Priority support

68.4 Team Plan — Future
Intended for:
Agencies
Small product teams
Consulting teams
Research groups
Potential future capabilities:
Shared workspaces
Member roles
Shared memories
Private personal memories
Team usage controls
Central billing
Audit history
Administrative controls
The Team plan is not part of the initial MVP.

69. Pricing Principles
Gexor pricing should follow these principles:
Provider usage remains separately billed.
Pricing should be understandable.
Memory and workspace limits should not feel deceptive.
Users should not be charged for failed provider requests caused by Gexor.
No hidden token markup should be applied initially.
Free-plan limits should support meaningful evaluation.
Paid plans should unlock measurable value.
Pricing should reflect infrastructure and support costs.
Pricing should not depend only on message count.
Early pricing should remain easy to change.

70. Initial Pricing Hypothesis
Final prices will be validated through interviews and beta usage.
An initial India-oriented hypothesis may be:
Free: ₹0
Personal: approximately ₹199 per month
Pro: approximately ₹499 per month
Team: approximately ₹1,499 per month in a future release
These values are hypotheses rather than locked commercial commitments.
Before pricing is finalised, Gexor must evaluate:
User willingness to pay
Average infrastructure cost
Memory-processing cost
Support cost
Paid conversion
Retention
Competitor positioning
Value delivered to primary users

71. Future Revenue Opportunities
Possible future revenue sources include:
Individual subscriptions
Team subscriptions
Enterprise subscriptions
Advanced memory and knowledge limits
Premium integrations
Private or local deployment
Developer API access
Managed provider connections
White-label deployment
Priority support
Professional onboarding
Workspace migration services
These opportunities must not distract from proving the core MVP.

72. Prohibited or Discouraged Revenue Practices
Gexor should not rely on:
Selling personal user data
Selling workspace content
Targeted advertising using private conversations
Hidden provider markups
Dark-pattern subscriptions
Difficult cancellation
Unclear billing separation
Artificial token consumption
Unnecessary model calls intended to increase revenue
Trust is a core product requirement.

73. Product Success Framework
Gexor success will be evaluated across five dimensions:
1. User value
2. Product quality
3. Trust and safety
4. Commercial viability
5. Operational sustainability
High registration numbers alone will not prove product success.

74. North-Star Metric
The proposed north-star metric is:
Weekly Active Continuity Workspaces
A Weekly Active Continuity Workspace is a workspace in which, during a seven-day period:
The user sends meaningful AI requests
At least one request uses existing workspace context or memory
The workspace is used across more than one session or conversation
This metric represents the core Gexor value:
Ongoing work
Reused context
Persistent continuity
Repeated product usage

75. Primary Product Metrics
75.1 Activation Metrics
Track:
Account registration completion
Provider connection success rate
Workspace creation rate
First successful request rate
First memory creation rate
Onboarding completion rate
Time to first successful response
A user may be considered activated when they:
1. Create an account
2. Connect a provider
3. Create a workspace
4. Send a successful request
5. Create or confirm at least one memory

75.2 Engagement Metrics
Track:
Daily active users
Weekly active users
Monthly active users
Active workspaces
Conversations per active workspace
Requests per active workspace
Returning-workspace rate
Multi-session workspace usage
Private-chat usage
Runtime-details usage

75.3 Retention Metrics
Track:
Day-1 retention
Day-7 retention
Day-30 retention
Weekly cohort retention
Workspace retention
Provider-connection retention
Paid-plan retention after monetisation
Retention should be evaluated primarily for users who successfully activated.

75.4 Memory Metrics
Track:
Memories created
Memories automatically saved
Memories suggested
Suggested-memory confirmation rate
Memory reuse rate
Memory edit rate
Memory deletion rate
Incorrect-memory reports
Irrelevant-memory usage
Memory conflicts
Time between memory creation and reuse

75.5 Prompt and Context Metrics
Track:
Off, Auto, and Strong mode usage
Enhancement success rate
Enhancement failure rate
Enhanced-answer preference
User-intent-change reports
Context tokens added
Context tokens excluded
Conversation-summary usage
Average memories retrieved per request
Requests requiring clarification

75.6 Provider and Model Metrics
Track:
Provider connection attempts
Provider connection success
Provider authentication failures
Requests by provider
Requests by model
Model recommendation rate
Recommendation acceptance rate
Model-switching rate
Provider-switching rate
Provider error rate
Provider response latency

75.7 Usage and Cost Metrics
Track:
Input tokens
Output tokens
Context tokens
Background-processing tokens
Estimated provider cost
Estimated cost per active workspace
Cost-warning triggers
Hard-limit triggers
Hard-limit overrides
Expensive request frequency

75.8 Trust Metrics
Track:
Private-mode adoption
Memory undo rate
Memory correction rate
Data-export requests
Data-deletion requests
Provider-key removal
Security-related support tickets
Privacy-related support tickets
User-reported context leakage
Cross-workspace context incidents
Any verified cross-user or cross-workspace leakage is a critical incident.

76. Primary Quality Metric
The primary answer-quality metric will be:
Enhanced Response Preference Rate
This metric compares:
A response generated through Gexor’s runtime
A response generated directly using the same or comparable provider model without Gexor enhancement
Users or evaluators should select:
Gexor response preferred
Direct response preferred
Approximately equal
Both unacceptable
The comparison must account for:
Same task
Equivalent model conditions
Similar generation settings
No misleading presentation bias

77. Continuity Metrics
Gexor should measure whether users repeat less context.
Possible continuity indicators include:
Number of stable facts manually repeated
Number of relevant memories reused
Number of new conversations continuing an existing project
User-rated continuity
Contradiction frequency
Time required to resume a project
Project-summary reuse
Cross-provider continuity usage

78. MVP Success Thresholds
Before declaring the MVP validated, Gexor should aim to demonstrate:
Users can complete core onboarding without direct assistance.
A meaningful percentage of activated users return weekly.
Users create and reuse workspace memories.
Enhanced responses are preferred more often than direct responses.
Incorrect-memory incidents remain low and correctable.
Provider connection success is acceptable.
Cross-workspace leakage is not observed.
Users report reduced repeated context.
Infrastructure cost per active user remains sustainable.
A portion of retained users express willingness to pay.
Exact numerical thresholds should be defined after the first internal and private-alpha datasets become available.

79. Validation Program
79.1 Problem Validation
Before or during prototype development, interview target users about:
Repeated context
Long-running AI projects
Provider switching
Memory trust
Prompt difficulty
Token costs
API-key willingness
Current workarounds
Payment willingness

79.2 Prototype Validation
The prototype should demonstrate:
Workspace creation
Provider connection
Prompt enhancement
Memory creation
Memory reuse
New-conversation continuity
Runtime transparency
Cost visibility
The goal is not to demonstrate every future capability.

79.3 Private Alpha Validation
Private-alpha users should complete real project work.
The founder should observe:
Setup difficulties
Repeated-context reduction
Memory mistakes
Provider failures
Model-selection behaviour
Feature confusion
Unmet expectations
Returning usage

79.4 Blind Quality Evaluation
Where practical, users should compare:
Direct provider output
Gexor-enhanced output
The labels should be hidden or randomised where possible.
The evaluation should measure:
Relevance
Completeness
Consistency
Actionability
Project alignment
Preferred response

79.5 Pricing Validation
Pricing should be tested using:
Interviews
Willingness-to-pay questions
Pricing-page experiments
Paid pilot offers
Monthly versus annual preference
Feature-package comparisons
Compliments and waitlist sign-ups must not be treated as payment validation.

80. User Research Requirements
Research participants should include:
Startup founders
Independent builders
Freelancers
Consultants
AI power users
Research should include users with different levels of:
Technical ability
AI usage
Provider familiarity
Project complexity
Cost sensitivity
Privacy sensitivity
Research records should avoid collecting unnecessary sensitive data.

81. Product Analytics Requirements
Product analytics should capture meaningful product events without storing unnecessary conversation content.
Analytics events may include:
Account created
Provider connected
Provider connection failed
Workspace created
Conversation started
Request completed
Request failed
Prompt mode changed
Memory saved
Memory confirmed
Memory rejected
Memory edited
Memory deleted
Private chat started
Model recommendation accepted
Cost warning triggered
Export requested
Account deletion requested
Analytics must not include:
API keys
Authentication secrets
Complete private messages by default
Sensitive memory content
Provider credentials
Raw exported data

82. Growth Strategy
82.1 Initial Growth Method
Initial growth should prioritise founder-led distribution.
Channels may include:
Direct outreach
Founder communities
Independent-builder communities
AI power-user communities
Freelancer communities
Demonstration videos
Product walkthroughs
Waitlist referrals
Private invitations
User case studies

82.2 Primary Growth Message
The primary adoption message will be:
Stop repeating your project context.
Supporting messages may include:
Keep your project memory across AI providers.
Turn rough prompts into project-aware instructions.
Control what your AI remembers.
See which context and model were used.
Bring your own AI provider.

82.3 Growth Restrictions
Gexor should avoid:
Large paid advertising before retention
Broad “AI for everyone” positioning
Promising perfect memory
Promising guaranteed lower cost
Claiming to own or provide the external AI models
Acquiring users faster than support and security can handle

83. Referral and Community Features
Referral incentives may be considered after initial validation.
Possible future incentives:
Extended beta limits
Temporary Pro access
Additional workspace capacity
Early access to new providers
Referral systems must not delay the MVP.
A user community may later support:
Product feedback
Provider setup help
Workflow sharing
Product announcements
Early feature testing

84. Commercial Risks
84.1 Users Prefer Provider Subscriptions
Users may prefer paying a fixed monthly provider subscription rather than managing API usage.
Mitigation:
Target users already comfortable with APIs
Explain provider billing clearly
Demonstrate cross-provider continuity
Make cost visible
Consider managed usage later

84.2 Users Do Not Want Two Bills
Users may resist paying both Gexor and their AI provider.
Mitigation:
Clearly separate the value of Gexor
Keep initial Gexor pricing modest
Demonstrate saved time and improved continuity
Provide meaningful free evaluation
Avoid hidden usage markups

84.3 Memory Is Not Valuable Enough
Users may not pay merely for memory.
Mitigation:
Gexor must provide a combined value layer:
Memory
Context management
Prompt improvement
Provider portability
Cost controls
Workspace organisation

84.4 Existing Providers Add Similar Features
AI providers may improve their own memory and project functionality.
Mitigation:
Gexor should focus on:
Provider independence
Cross-provider portability
Transparent memory
User-controlled runtime
BYOK
Workspace-owned data
Cost-aware model flexibility

84.5 Operating Cost Exceeds Subscription Value
Background model calls, storage, logs, and support may create high costs.
Mitigation:
Use deterministic processing where possible
Batch background work
Limit unnecessary extraction
Apply fair-use limits
Measure cost per active workspace
Design paid plans around actual cost

85. Decision-Making Metrics
Feature decisions should prioritise improvements to:
1. Weekly Active Continuity Workspaces
2. Activated-user retention
3. Enhanced Response Preference Rate
4. Relevant memory reuse
5. Reduced repeated context
6. Trust and correction metrics
7. Provider connection success
8. Sustainable cost per active user
Features that increase raw messages without improving these measures should not automatically receive priority.

86. Section 5 Acceptance Criteria
This section is complete when:
The BYOK commercial model is defined.
Public-beta pricing status is defined.
Future subscription structure is outlined.
Pricing principles are documented.
Prohibited revenue practices are documented.
A north-star metric is selected.
Activation, engagement, retention, memory, provider, and cost metrics are defined.
Answer-quality and continuity measurements are defined.
Validation methods are documented.
Product analytics boundaries are established.
Initial growth strategy is defined.
Major commercial risks are documented.

Gexor — Product Requirements Document
Section 6: Product Assumptions, Constraints, Dependencies, Risks, and Mitigation Strategy

87. Section Purpose
This section identifies the conditions Gexor depends on, the limitations within which it must operate, and the major risks that may prevent the product from delivering its intended value.
The section exists to prevent the team from treating uncertain assumptions as confirmed facts.
Every major product assumption should be:
Documented
Testable
Assigned a validation method
Reviewed during development
Updated when evidence changes
Every material risk should have:
A defined cause
A possible impact
An estimated priority
A mitigation strategy
A detection method
A responsible owner in future project planning

88. Product Assumptions
88.1 User-Problem Assumption
Gexor assumes that repeating project context is a sufficiently frequent and painful problem for target users.
Expected evidence:
Users report repeated context as a recurring frustration.
Users maintain external notes or copy context between chats.
Users return to ongoing projects across multiple sessions.
Users value a system that preserves project decisions.
Validation methods:
Target-user interviews
Usage observation
Repeated-context measurement
Retention analysis
Paid pilot behaviour
Invalidation signal:
Users understand the concept but do not repeatedly use project memory or workspaces.

88.2 Enhanced-Answer Assumption
Gexor assumes that structured context, prompt enhancement, and relevant memory will produce answers that users prefer over direct provider interactions.
Expected evidence:
Gexor-enhanced responses win blind comparisons.
Users report less manual prompt preparation.
Users regenerate fewer responses.
Users repeat less context.
Users continue projects more efficiently.
Invalidation signal:
Gexor adds complexity or tokens without consistently improving response usefulness.

88.3 Memory-Value Assumption
Gexor assumes that users will value structured memory when it is:
Relevant
Accurate
Visible
Editable
Deletable
Workspace-specific
Linked to its source
Expected evidence:
Users create or confirm memories.
Existing memories are reused.
Users return to memory-enabled workspaces.
Users actively correct memories rather than disabling the system entirely.
Invalidation signal:
Users avoid memory, delete most extracted memories, or prefer manual context entry.

88.4 Memory-Trust Assumption
Gexor assumes that transparency and reversible controls can create sufficient trust in automated memory.
Expected evidence:
Users accept Balanced mode.
Automatic-memory undo rates remain manageable.
Memory-related support complaints remain low.
Users understand why memories were used.
Invalidation signal:
Users consistently switch to Manual Only because automatic memory feels unsafe or intrusive.

88.5 BYOK Willingness Assumption
Gexor assumes that primary users are willing to:
Create provider API keys
Connect them to Gexor
Understand separate provider billing
Configure provider-side spending controls
Resolve occasional provider-account issues
Expected evidence:
Provider connection completion is high among qualified users.
Users complete setup without founder assistance.
API-key concerns do not prevent activation.
Invalidation signal:
A large percentage of interested users abandon onboarding at provider connection.

88.6 Two-Bill Acceptance Assumption
Gexor assumes retained users may accept paying separately for:
1. Gexor
2. Their chosen AI provider
Expected evidence:
Retained users recognise Gexor’s independent value.
Paid pilots convert despite separate provider billing.
Users compare Gexor pricing to productivity value rather than token access alone.
Invalidation signal:
Users consistently state that they will only pay for a bundled AI subscription.

88.7 Provider-Portability Assumption
Gexor assumes users value keeping their project context independent of one provider.
Expected evidence:
Users connect more than one provider.
Users switch models while continuing the same project.
Cross-provider continuity is mentioned as a purchase reason.
Invalidation signal:
Most users remain permanently attached to one provider and do not value portability.

88.8 Cost-Awareness Assumption
Gexor assumes that target users value:
Per-request token visibility
Cost estimates
Model recommendations
Warning thresholds
Context-overhead information
Expected evidence:
Users view usage details.
Users configure cost preferences.
Users accept cheaper-model recommendations.
Cost controls influence model behaviour.
Invalidation signal:
Cost controls are rarely used and add interface complexity without affecting decisions.

88.9 Workspace-Assumption
Gexor assumes project and client workspaces are an understandable way to isolate context.
Expected evidence:
Users create multiple workspaces for distinct projects.
Cross-workspace mistakes remain rare.
Users understand where a conversation and memory belong.
Invalidation signal:
Users find workspace boundaries confusing or prefer one global memory space.

88.10 Web-First Assumption
Gexor assumes a responsive web application is sufficient to validate the product before native applications are developed.
Expected evidence:
Core usage occurs successfully on desktop and mobile web.
Native-app absence does not materially block activation or retention.
Invalidation signal:
Target users require native mobile capabilities before they will adopt the product.

89. Technical Assumptions
89.1 Provider API Stability
Gexor assumes Gemini and OpenAI will continue providing:
Public API access
Streaming responses
Usage metadata
Supported authentication
Stable documentation
Sufficient model availability
The architecture must still expect API changes.

89.2 Provider Abstraction
Gexor assumes that common provider operations can be represented through a unified internal interface while preserving provider-specific capabilities.
Common abstraction may include:
Provider
Model
Message roles
Streaming events
Token usage
Errors
Cost estimates
Capability metadata
Provider-specific behaviour must not be erased merely to force complete uniformity.

89.3 Structured Memory Feasibility
Gexor assumes useful memory can be represented through structured records rather than storing complete history as permanent context.
This assumption requires:
Reliable extraction
Classification
Confidence scoring
Conflict handling
Relevance retrieval
User correction

89.4 Lightweight Initial Retrieval
Gexor assumes the MVP can begin with:
Structured filters
Keyword or full-text relevance
Metadata ranking
Basic similarity methods
A dedicated vector infrastructure may be added later when necessary.

89.5 Background Processing
Gexor assumes memory extraction and summarisation can occur after response delivery without damaging the visible user experience.
The system must account for:
Failed jobs
Delayed jobs
Duplicate processing
Out-of-order completion
Retry behaviour
Idempotency

89.6 Cost Estimation
Gexor assumes provider token usage and public pricing information are sufficient to provide useful estimates.
The system must treat estimates as approximate because:
Providers may change prices.
Cached tokens may be priced differently.
Internal provider calculations may vary.
Some usage metadata may arrive after generation.
Taxes and currency conversion may differ.

89.7 Secure Secret Storage
Gexor assumes the selected infrastructure can securely store user provider credentials using:
Encryption
Strict server-side access
Per-user isolation
Secret masking
Safe logging rules
Credential deletion
This assumption must be verified through implementation and security testing.

90. Product Constraints
90.1 Founder Constraint
Gexor is initially being developed as a first startup with limited:
Capital
Engineering resources
Security resources
Operational capacity
Customer-support capacity
Marketing budget
The product must therefore prioritise:
Narrow MVP scope
Managed infrastructure
Automation of repetitive operations
Simple architecture
Low fixed cost
Gradual user growth
Selective professional review

90.2 Non-Coder Founder Constraint
The founder may use AI-assisted development but cannot depend on generated code without understanding and validation.
The project must include:
Clear technical documentation
Small implementation steps
Version control
Automated tests
Repeatable deployment
Security review for critical components
Decision records
Rollback procedures

90.3 Budget Constraint
The early product should remain compatible with free or low-cost infrastructure tiers where practical.
However, cost reduction must not compromise:
Credential security
User-data isolation
Backup reliability
Monitoring
Deletion requirements
Production stability

90.4 Time Constraint
The product must reach a testable prototype without implementing the complete long-term platform.
Features that are not required to validate the central hypothesis must be postponed.

90.5 BYOK Constraint
Because users bring provider credentials:
Provider errors will vary by user account.
Billing problems may appear as product failures.
Available models may differ between users.
Support documentation must cover external provider setup.
Gexor cannot control final provider billing.

90.6 Provider Constraint
Gexor depends on external systems for response generation.
Gexor cannot guarantee:
Provider availability
Model behaviour
Model factual accuracy
Provider response latency
Provider pricing stability
Provider policy stability
Model availability in every region

90.7 Privacy Constraint
Gexor must process conversation and memory data to deliver its value.
It must therefore minimise:
Unnecessary retention
Cross-workspace access
Sensitive-content exposure
Secret logging
Unrestricted administrative access
Hidden memory behaviour

90.8 Latency Constraint
Runtime intelligence may add processing time.
The MVP must avoid excessive delay from:
Classification
Prompt enhancement
Memory retrieval
Model recommendation
Cost estimation
Background processing
Simple requests should not trigger expensive multi-step orchestration.

90.9 Model-Quality Constraint
Prompt enhancement cannot guarantee a better response for every request.
Some prompts may perform better when sent directly.
The product must therefore provide:
Off mode
Transparent runtime details
User override
Direct-send fallback
Quality measurement

90.10 Legal and Compliance Constraint
The initial MVP will not claim formal enterprise certifications unless they are actually achieved.
Gexor must not represent itself as:
Legally compliant in every jurisdiction
Suitable for regulated professional decisions without qualification
Certified under standards not formally completed
A replacement for professional legal, medical, or financial judgement

91. External Dependencies
91.1 AI Provider APIs
Critical dependencies:
Google Gemini API
OpenAI API
Dependency risks:
Outages
Rate limits
Authentication changes
Pricing changes
Model retirement
API-version changes
Policy changes
Required controls:
Provider adapter layer
Connection-health checks
Clear error mapping
Configurable model catalogue
Provider-status monitoring
Future fallback support

91.2 Cloud Infrastructure
Gexor depends on infrastructure for:
Web hosting
Server execution
Database
Authentication
Secret storage
Background jobs
Monitoring
Backups
Email
Each dependency must have:
Defined responsibility
Failure handling
Cost monitoring
Export or migration strategy where practical

91.3 Authentication Provider
Authentication availability affects all user access.
Required controls:
Secure session handling
Recovery flow
Email delivery monitoring
OAuth configuration
Account-linking rules
Authentication-event logging

91.4 Email Delivery
Email may be required for:
Verification
Password reset
Security notifications
Data-export notifications
Account-deletion confirmation
Gexor must not rely on email for core chat operation after authentication.

91.5 Payment Provider — Future
Paid subscriptions will eventually depend on a payment provider.
Payment functionality is not required for the free public beta.
Before paid launch, Gexor will require:
Subscription creation
Payment confirmation
Failed-payment handling
Cancellation
Refund policy
Invoice or receipt handling
Webhook verification
Plan-entitlement enforcement

91.6 Analytics and Monitoring
Gexor may depend on external tools for:
Product analytics
Error monitoring
Performance monitoring
Availability checks
Security alerts
No external monitoring tool should receive:
API keys
Authentication secrets
Complete private messages by default
Sensitive memory content without explicit justification

92. Risk Classification
Risks will be classified by:
Probability
Low
Medium
High
Impact
Low
Medium
High
Critical
Priority
Priority is based on combined probability and impact.
Critical security and privacy risks receive priority regardless of estimated probability.

93. Product Risks
93.1 Weak User Demand
Risk: Users may consider the idea useful but not important enough to adopt regularly.
Impact: High
Mitigation:
Target users with long-running AI work
Validate before broad development
Measure repeated-context pain
Recruit users with existing multi-model workflows
Focus on observable continuity benefits
Test willingness to pay
Detection:
Low activated-user retention
Low memory reuse
Low workspace return rate
Weak paid-pilot interest

93.2 Product Feels Like Another Chat Wrapper
Risk: Users may view Gexor as a thin interface over existing AI providers.
Impact: High
Mitigation:
Demonstrate continuity across new chats
Demonstrate cross-provider memory
Show context and prompt transparency
Measure answer-quality improvement
Make memory controls visibly stronger
Build project-oriented workflows
Detection:
Users compare only interface appearance
Low use of memory and workspace features
Users return to direct provider interfaces

93.3 BYOK Onboarding Abandonment
Risk: Users may abandon setup while creating or entering an API key.
Impact: High
Mitigation:
Step-by-step provider guides
Clear billing explanations
Connection tests
Save onboarding progress
Provider-specific troubleshooting
Target technically comfortable early adopters
Detection:
Low provider-connection completion
High drop-off at credential screen
Frequent setup-support requests

93.4 Low Willingness to Pay
Risk: Users may value Gexor but resist paying Gexor in addition to the provider.
Impact: High
Mitigation:
Prove measurable time savings
Keep initial pricing accessible
Provide meaningful free evaluation
Test pricing before building complex billing
Position Gexor as workspace infrastructure, not token access
Detection:
Strong usage with weak paid conversion
Repeated objections to separate billing
Preference for provider subscription interfaces

93.5 Feature Overload
Risk: Too many settings may make the product difficult to understand.
Impact: Medium to High
Mitigation:
Progressive disclosure
Recommended defaults
Simple chat-first UI
Hide advanced details until requested
Limit MVP modes and options
Conduct usability testing
Detection:
Onboarding confusion
Users unable to explain settings
High support volume
Settings rarely changed after confusion

93.6 Scope Creep
Risk: The product may expand into agents, files, teams, integrations, and native applications before validating memory-chat value.
Impact: High
Mitigation:
Enforce explicit MVP exclusions
Use scope-control questions
Require documented approval for additions
Tie features to north-star and retention metrics
Maintain post-MVP backlog
Detection:
Repeated release delays
Large unfinished modules
Core memory quality remains untested
Development spreads across unrelated systems

94. Memory Risks
94.1 Incorrect Memory
Risk: Gexor may save incorrect information as a fact.
Impact: High
Mitigation:
Confidence scoring
Source traceability
Suggested confirmation
Easy edit and deletion
Separate confirmed and inferred status
Avoid saving AI-generated assumptions
Detection:
User correction rate
Incorrect-memory reports
Contradictory-response reports
High automatic-memory undo rate

94.2 Irrelevant Memory Retrieval
Risk: Correct memory may be used in an unrelated request.
Impact: High
Mitigation:
Workspace isolation
Relevance thresholds
Category filtering
Context budgets
Retrieval evaluation
Runtime details
User feedback controls
Detection:
Irrelevant-memory feedback
Low response preference
High memory-disable rate
Manual correction after responses

94.3 Conflicting Memories
Risk: Multiple stored memories may contradict each other.
Impact: High
Mitigation:
Conflict detection
Recency and source comparison
Explicit user resolution
Replacement status
Version history
Avoid silently using unresolved conflicts
Detection:
Conflict events
Contradictory answer reports
Multiple active facts for the same property

94.4 Memory Overcollection
Risk: The system may save too much information.
Impact: High
Mitigation:
Stable-value threshold
Memory-mode settings
Sensitivity classification
Duplicate merging
Expiration
Retention controls
Automatic-memory notifications
Detection:
High deletion or undo rate
Rapid memory growth
Low memory reuse
Privacy complaints

94.5 Stale Memory
Risk: Outdated information may continue affecting responses.
Impact: Medium to High
Mitigation:
Last-confirmed timestamp
Expiry dates
Recency weighting
Workspace-status updates
Stale-memory review prompts
Replacement workflow
Detection:
Old memories repeatedly corrected
Contradictory new decisions
Low relevance for frequently used old memories

94.6 Sensitive Memory Storage
Risk: Sensitive personal, client, or business information may be stored without appropriate consent.
Impact: Critical
Mitigation:
Sensitivity detection
Confirmation requirements
Restricted categories
Manual-only rules for high-risk information
Encryption
User deletion
Audit controls
Detection:
Sensitive-memory reports
Security reviews
Memory-category audits
Privacy-support tickets

95. Security Risks
95.1 API-Key Exposure
Risk: A user’s provider API key may be exposed through storage, logs, interface, analytics, or application vulnerabilities.
Impact: Critical
Mitigation:
Encryption
Server-side access only
Secret masking
Log filtering
Strict authorization
Secure environment management
Key-removal support
Security review
Detection:
Secret scanning
Log audits
Access monitoring
Incident alerts
Penetration testing

95.2 Cross-User Data Leakage
Risk: One user may access another user’s conversations, memories, provider connection, or workspace information.
Impact: Critical
Mitigation:
Row-level security
Server-side authorization
Ownership checks
Negative-access tests
Separate administrative permissions
Secure identifiers
Regular security testing
Detection:
Automated isolation tests
Audit logs
Access anomalies
User reports
Security monitoring

95.3 Cross-Workspace Context Leakage
Risk: Information from one workspace may be included in another workspace’s provider request.
Impact: Critical
Mitigation:
Workspace identifiers on every relevant record
Query-level workspace filters
Runtime ownership validation
Retrieval isolation tests
Context-source logging
No global memory by default
Detection:
Runtime context audits
Automated workspace-isolation tests
User feedback
Retrieval evaluation

95.4 Prompt Injection
Risk: User content, memories, or future uploaded documents may attempt to override system instructions or extract protected information.
Impact: High
Mitigation:
Separate instruction hierarchy
Treat retrieved content as untrusted data
Limit tool and external-action permissions
Do not expose secrets to model context
Input and output controls
Prompt-injection testing
Detection:
Security test suite
Suspicious-pattern monitoring
User reports
Runtime anomaly analysis

95.5 Administrative Abuse
Risk: Internal administrative access may be used to inspect or modify user information improperly.
Impact: Critical
Mitigation:
Least-privilege roles
Audit logs
Restricted support access
Break-glass procedures
No casual content browsing
Strong authentication
Access reviews
Detection:
Administrative audit reviews
Suspicious-access alerts
Approval records

95.6 Account Takeover
Risk: An attacker may access a user account and provider credentials.
Impact: Critical
Mitigation:
Secure authentication
Session expiration
Password reset controls
OAuth safeguards
Optional future MFA
Suspicious-login monitoring
Credential-removal notifications
Detection:
Login anomaly alerts
Session monitoring
User reports
Authentication logs

96. Technical Risks
96.1 Provider API Changes
Risk: A provider may change authentication, models, request formats, or usage fields.
Impact: High
Mitigation:
Provider adapter layer
Versioned integrations
Integration tests
Configurable model registry
Provider-specific monitoring
Clear degradation behaviour

96.2 Provider Outage
Risk: Requests may fail because an external provider is unavailable.
Impact: High
Mitigation:
Clear error states
Retry options
Preserve user input
Model/provider switching
Status monitoring
Future fallback support

96.3 Excessive Latency
Risk: Runtime processing may make Gexor slower than direct provider chat.
Impact: High
Mitigation:
Lightweight classification
Parallel safe operations
Background memory extraction
Avoid extra calls for simple prompts
Cache stable instructions
Track time-to-first-token
Detection:
Latency percentiles
User complaints
Direct-versus-Gexor comparisons
Abandoned requests

96.4 Excessive Token Overhead
Risk: Added memory and prompt instructions may increase user provider costs.
Impact: High
Mitigation:
Context budgets
Memory relevance thresholds
Deduplication
Summaries
Compact structured memory
Economy mode
Per-request cost visibility
Detection:
Runtime overhead ratio
Provider-cost trends
User cost complaints
Long prompt audits

96.5 Background Job Failure
Risk: Memory extraction or summary updates may fail after a successful response.
Impact: Medium
Mitigation:
Retry policies
Idempotent jobs
Failure queues
Status tracking
Manual reprocessing
Monitoring and alerts

96.6 Data Growth
Risk: Conversations, messages, memories, logs, and runtime records may grow faster than expected.
Impact: Medium to High
Mitigation:
Retention policies
Archival
Indexing
Usage limits
Log expiration
Cost monitoring
Storage forecasts

96.7 Generated-Code Quality
Risk: AI-assisted code may contain security, reliability, or maintainability problems.
Impact: High
Mitigation:
Small reviewed changes
Automated testing
Static analysis
Dependency scanning
Code review
Documentation
Security review for critical systems
No blind deployment of generated code

97. Operational Risks
97.1 Founder Support Overload
Risk: Provider setup, billing questions, and memory problems may create excessive support requirements.
Impact: High
Mitigation:
Guided onboarding
Troubleshooting guides
Error categorisation
In-app diagnostics
Gradual invitation growth
Support issue tracking

97.2 Infrastructure Cost Growth
Risk: Free users may create storage and background-processing costs without revenue.
Impact: High
Mitigation:
Fair-use limits
Free-plan memory limits
Processing budgets
Cost-per-active-workspace tracking
Abuse controls
Paid-plan introduction after validation

97.3 Insufficient Monitoring
Risk: Failures or security incidents may remain undetected.
Impact: Critical
Mitigation:
Error monitoring
Availability checks
Provider-failure alerts
Cost alerts
Security alerts
Audit logs
Incident-response procedures

97.4 Poor Documentation Maintenance
Risk: Documentation may become inconsistent with implementation.
Impact: Medium to High
Mitigation:
Documentation as source of truth
Change records
Pull-request documentation checks
Architecture decision records
Release reviews
Update tests with requirements

97.5 Dependency Lock-In
Risk: Gexor may become overly dependent on one infrastructure vendor.
Impact: Medium
Mitigation:
Standard PostgreSQL-compatible data model
Exportable data
Provider abstraction
Infrastructure documentation
Avoid unnecessary proprietary services
Maintain migration options for critical systems

98. Legal and Trust Risks
98.1 Misleading Cost Claims
Risk: Users may believe Gexor guarantees cheaper provider usage.
Mitigation:
Use “designed to reduce unnecessary token usage”
Display estimates and disclaimers
Show runtime overhead
Avoid guaranteed savings claims

98.2 Misleading Quality Claims
Risk: Users may believe Gexor guarantees correct or superior answers.
Mitigation:
State that quality varies by task and provider
Maintain Off mode
Measure preferences honestly
Avoid “always better” language

98.3 Provider Trademark Confusion
Risk: Users may believe Gexor owns, represents, or is officially affiliated with external AI providers.
Mitigation:
Clear provider attribution
Separate billing disclosure
Correct trademark usage
No false partnership claims

98.4 User-Content Responsibility
Risk: Users may use Gexor for harmful, unlawful, or prohibited activities.
Mitigation:
Acceptable-use policy
Provider policy compliance
Abuse reporting
Account suspension
Rate limits
Documented enforcement process

98.5 Data Deletion Expectations
Risk: Users may misunderstand the difference between immediate application removal, the Gexor hard-purge window, and independent provider-side retention.
Mitigation:
Clearly explain deletion stages
Define backup retention
Explain provider-side responsibility
Confirm completed deletion where possible
Soft-delete account or workspace data immediately so it is hidden from application visibility and normal runtime access
Permanently hard-purge all associated rows, assets, metadata, cached background queues, and Gexor-controlled system-backup copies within exactly 30 days
Record and monitor the deletion request timestamp, purge deadline, and completion timestamp
Explain that provider-side copies remain governed by the external provider’s retention and deletion policies

99. Risk Prioritisation for the MVP
Critical Before Any External Testing
API-key exposure
Cross-user data leakage
Cross-workspace context leakage
Authentication failure
Secret logging
Uncontrolled administrative access

Critical Before Private Alpha
Incorrect workspace retrieval
Broken data deletion
Private-mode memory leakage
Provider credential mismanagement
Background jobs creating duplicate or incorrect memories

Critical Before Public Beta
Memory trust failures
Provider onboarding failure
Inadequate rate limiting
Missing monitoring
Missing backup and recovery
Unclear cost disclosures
Unusable account deletion
Weak incident response

Validate During Beta
Willingness to pay
Long-term retention
Provider portability value
Cost-control usage
Appropriate Free-plan limits
Referral effectiveness
Demand for files and knowledge

100. Assumption and Risk Review Process
The founder and future team should review assumptions and risks:
Before architecture approval
Before implementation of critical systems
Before private alpha
Before closed beta
Before public beta
Before paid launch
After every critical incident
After material provider changes
Each review should record:
Assumption status
New evidence
Risk changes
Mitigation progress
Required product changes
Responsible owner
Review date

101. Section 6 Acceptance Criteria
This section is complete when:
Product assumptions are explicitly documented.
Technical assumptions are identified.
Founder, budget, time, and provider constraints are defined.
Critical external dependencies are listed.
Product, memory, security, technical, operational, and legal risks are covered.
Every critical risk has mitigation and detection methods.
MVP risk priorities are established.
A repeatable review process is defined.

Gexor — Product Requirements Document
Section 7: Release Strategy, Product Roadmap, Milestones, and Launch Readiness

102. Release Strategy Purpose
This section defines how Gexor will move from an internal prototype to a stable public product.
The release strategy exists to:
Prevent premature public launch
Control technical and security risk
Validate the core product hypothesis gradually
Keep development focused on the MVP
Limit support and infrastructure overload
Establish measurable entry and exit criteria
Separate experimental features from stable features
Define what must be completed at each milestone
Ensure documentation, testing, and operations evolve with the product
A release milestone will not be considered complete merely because its features have been coded.
Each milestone must satisfy:
Product requirements
Functional acceptance
Security requirements
Reliability requirements
Testing requirements
Documentation requirements
Operational readiness
User-validation requirements

103. Release Principles
103.1 Prove the Core Before Expanding
Gexor must first prove that users benefit from:
Workspace continuity
Structured memory
Relevant context retrieval
Prompt enhancement
Provider-independent operation
Transparent runtime controls
Features such as files, agents, teams, integrations, voice, and native applications must not distract from this validation.

103.2 Release Gradually
Gexor will follow controlled release stages:
1. Technical foundation
2. Internal prototype
3. Founder validation
4. Private alpha
5. Closed beta
6. Public beta
7. Paid launch
8. Post-MVP expansion
Each stage must have a limited and clearly understood audience.

103.3 Security Before Scale
User growth must not exceed the product’s ability to securely isolate:
Accounts
Workspaces
Conversations
Messages
Memories
Provider credentials
Usage records
Administrative access
Security-critical defects block progression to the next release stage.

103.4 Reliability Before Monetisation
Gexor must not charge users for a product that cannot reliably provide:
Successful provider connection
Stable message streaming
Correct workspace isolation
Controllable memory
Clear cost information
Data export
Data deletion
Reasonable support

103.5 Evidence-Based Progression
Release stages will advance based on measurable evidence rather than a fixed calendar alone.
Schedule targets may be established, but quality and validation gates determine whether progression is allowed.

103.6 Small Reversible Releases
Development should favour:
Small feature increments
Feature flags
Limited rollout
Staging validation
Rollback capability
Clear migration plans
Measurable outcomes
Large releases containing many unrelated changes should be avoided.

104. Release Stage Overview
Stage	Primary Goal	Intended Users
Technical Foundation	Establish safe project infrastructure	Founder/development environment
Internal Prototype	Prove end-to-end runtime	Founder only
Founder Validation	Perform real project usage	Founder and trusted tester
Private Alpha	Validate core value and usability	10–25 invited users
Closed Beta	Improve reliability and retention	50–150 invited users
Public Beta	Validate broader demand and operations	Gradually expanded public users
Paid Launch	Validate commercial viability	Retained users and new customers
Post-MVP	Expand capabilities carefully	Broader individual and team markets

The user ranges are planning targets and may be adjusted according to operational capacity.

105. Stage 0 — Technical Foundation
105.1 Objective
Establish the minimum engineering and operational foundation required to build Gexor safely.

105.2 Required Deliverables
Source-code repository
Branching strategy
Development environment
Environment-variable management
Supabase or selected database project
Authentication foundation
Database migration process
Hosting environment
Basic CI checks
Error monitoring
Logging baseline
Secret-scanning protection
Dependency-management process
Documentation repository
Issue and task tracking
Architecture decision record process

105.3 Required Environments
At minimum:
Local development
Staging
Production-ready environment definition
Production may not yet contain public users, but its configuration approach must be documented.

105.4 Exit Criteria
Stage 0 is complete when:
A developer can set up the project using documentation.
Code can be deployed to staging.
Database migrations can be applied safely.
Secrets are excluded from source control.
Basic authentication works.
Errors can be observed.
Automated checks run before merging or deployment.
A rollback approach exists.

106. Stage 1 — Internal Prototype
106.1 Objective
Prove the complete basic request path from user input to provider response.

106.2 Required Scope
Founder account
Email or Google authentication
One workspace
One connected provider
One or more provider models
Basic conversation creation
User-message storage
Provider request execution
Streamed response
Assistant-message storage
Manual provider and model selection
Basic prompt enhancement
Manual memory creation
Basic memory retrieval
Usage-record creation
Error handling
Basic runtime logs

106.3 Prototype Runtime
The prototype must demonstrate:
User message
→ Workspace validation
→ Provider credential retrieval
→ Basic context construction
→ Provider request
→ Streamed response
→ Message persistence
→ Usage persistence

106.4 Prototype Exclusions
The internal prototype does not require:
Polished onboarding
Multiple providers
Automatic memory extraction
Subscription billing
Public landing page
Full mobile optimisation
Complete analytics
Advanced administration
Public legal documents

106.5 Exit Criteria
Stage 1 is complete when:
The founder can complete an end-to-end conversation.
Responses stream reliably.
Messages persist correctly.
A manually added memory can influence a later request.
Provider errors do not lose the user’s message.
Credentials do not appear in logs or the interface.
Workspace access checks are implemented.
Usage is recorded.

107. Stage 2 — Founder Validation
107.1 Objective
Use Gexor for real, continuing project work before exposing the product to external users.

107.2 Validation Activities
The founder should use Gexor for:
Product planning
Technical decisions
Long-running documentation
Research
Project continuation across new conversations
Switching between supported models
Reviewing memory usage
Correcting memories
Testing private mode
Reviewing token and cost information

107.3 Required Improvements
During founder validation, Gexor should add:
Second provider
Prompt modes: Off, Auto, Strong
Memory retrieval toggle
Structured memory records
Automatic and suggested memory candidates
Memory source traceability
Runtime-details view
Conversation-title search
Private chat
Basic usage dashboard
Provider connection testing
Workspace creation flow

107.4 Founder Validation Questions
The founder must determine:
Does Gexor reduce repeated context?
Are responses more relevant?
Does prompt enhancement preserve intent?
Are memories usually correct?
Is workspace isolation understandable?
Is provider switching useful?
Does runtime processing feel too slow?
Does context increase cost excessively?
Are controls understandable?
Is the product useful enough for repeated personal use?

107.5 Exit Criteria
Stage 2 is complete when:
Gexor is used repeatedly for real project work.
Multiple conversations can continue the same project.
Memory correction works.
Private mode behaves correctly.
Two providers work through the same runtime abstraction.
No known critical credential or isolation defect remains.
The founder chooses Gexor over direct provider chat for selected ongoing work.
Major usability blockers are documented or fixed.

108. Stage 3 — Private Alpha
108.1 Objective
Validate whether qualified external users understand and repeatedly use Gexor’s core capabilities.

108.2 Target Participants
Initial private-alpha participants should include:
Startup founders
Independent builders
Freelancers
Consultants
AI power users
Participants should preferably:
Use AI several times per week
Work on a continuing project
Be comfortable using API keys
Agree to provide detailed feedback
Understand that the product is experimental

108.3 Participant Count
Planning target:
First cohort: 5–10 users
Expanded alpha: up to 25 users
Growth should occur only after the first cohort completes onboarding and real use.

108.4 Alpha Capabilities
Private alpha should include:
Google and email authentication
Gemini and OpenAI connections
Project and client workspaces
Streaming chat
Prompt modes
Memory retrieval toggle
Balanced, Confirmation-Focused, and Manual memory modes
Structured memory
Memory suggestions
Automatic memory with Undo
Memory editing and deletion
Private chat
Runtime details
Basic model recommendation
Usage and estimated-cost visibility
Feedback reporting
Account and workspace deletion

108.5 Alpha Onboarding
Private-alpha onboarding may include direct founder assistance.
However, the founder must document:
Where assistance was needed
Which provider steps failed
Which explanations were unclear
Which settings confused users
Which errors lacked actionable guidance
The goal is to remove manual assistance before public beta.

108.6 Alpha Measurements
Track:
Invitation acceptance
Registration completion
Provider connection success
Workspace creation
First successful request
First memory creation or confirmation
Activation
Seven-day return
Memory reuse
Memory correction
Prompt-mode usage
User-reported repeated-context reduction
Enhanced-response preference
Support requests

108.7 Alpha Exit Criteria
Private alpha may progress when:
Core onboarding succeeds for most qualified participants.
No unresolved critical security defect exists.
No cross-user or cross-workspace leakage is detected.
Most activated users successfully complete real work.
Memory errors are visible and correctable.
Provider failures are understandable.
Some users return after the initial session.
Users demonstrate memory reuse.
Founder support requirements are documented.
Product value is stronger than novelty alone.

109. Stage 4 — Closed Beta
109.1 Objective
Improve product reliability, onboarding independence, retention, and operational readiness with a larger controlled audience.

109.2 Target Participant Count
Planning target:
Approximately 50–150 invited users
Expansion must remain gradual.

109.3 Closed-Beta Additions
Closed beta should add or mature:
Self-service onboarding
Provider-specific setup guides
Reliable email verification and password recovery
Better memory conflict resolution
Workspace export
Account export
Account deletion
Cost warning and hard-block controls
Improved mobile web
Product analytics
Error monitoring
Rate limiting
Abuse controls
Backup validation
Operational dashboards
Help centre
Support workflow
Feature flags
Release notes

109.4 Closed-Beta Testing
Required testing should include:
Authentication tests
Authorization tests
Row-level security tests
Cross-user negative-access tests
Cross-workspace retrieval tests
Provider-adapter tests
Streaming tests
Background-job tests
Memory precision evaluation
Prompt-intent preservation tests
Private-mode tests
Export tests
Deletion tests
Mobile-browser tests
Basic accessibility tests
Cost-estimation tests

109.5 Closed-Beta Metrics
Closed beta must focus on:
Activated-user retention
Weekly Active Continuity Workspaces
Provider connection success
Enhanced Response Preference Rate
Relevant memory reuse
Incorrect-memory rate
Repeated-context reduction
Request success rate
Time to first token
Support cases per active user
Infrastructure cost per active workspace

109.6 Closed-Beta Exit Criteria
Closed beta may progress when:
Self-service onboarding works for qualified users.
Critical user journeys work on desktop and mobile web.
Provider connections remain stable.
Memory precision meets the internally defined acceptable level.
Private mode passes functional and isolation testing.
Data export and deletion work reliably.
Product analytics are operational.
Monitoring and alerts are operational.
Backup restoration has been tested.
A documented incident-response process exists.
Retention shows evidence of continuing value.
Infrastructure cost is understood.
Public legal documents are prepared.

110. Stage 5 — Public Beta
110.1 Objective
Validate wider market demand, self-service adoption, product operations, and free-plan sustainability.

110.2 Access Model
Public beta should launch through controlled expansion.
Possible access methods:
Waitlist
Invitation codes
Gradual account opening
Geographic or cohort limits
Fair-use limits
“Public beta” does not require immediately accepting unlimited users.

110.3 Public-Beta Requirements
Before public beta:
Landing page is published.
Product positioning is clear.
Separate provider billing is disclosed.
Privacy policy is published.
Terms of service are published.
Acceptable-use policy is published.
Support contact is active.
Status and incident communication method exists.
Account deletion is available.
Data export is available.
Rate limits are enabled.
Security-sensitive logs are filtered.
Backup and rollback procedures exist.
Monitoring and alerts are enabled.
Beta limitations are disclosed.

110.4 Public-Beta Limits
The free public beta may limit:
One active workspace
Active memory records
Background-memory processing
Request frequency
Storage
Export frequency
Experimental features
The user’s provider API usage remains subject to provider billing.

110.5 Public-Beta Objectives
Public beta must determine:
Whether Gexor attracts qualified users
Whether users complete BYOK onboarding
Whether workspaces are reused
Whether users trust memory
Whether users return weekly
Whether support scales
Whether free usage is financially sustainable
Whether users request file knowledge
Whether users are willing to pay
Which plan boundaries are understandable

110.6 Public-Beta Exit Criteria
The product may prepare for paid launch when:
Retention targets are defined and met by a meaningful cohort.
Weekly Active Continuity Workspaces show sustained growth.
Memory quality remains acceptable at increased usage.
Critical security incidents are absent or fully resolved.
Support volume is manageable.
Infrastructure cost per active user is understood.
Personal and Pro plan boundaries are validated.
Pricing interviews or paid pilots show willingness to pay.
Subscription and entitlement systems are tested.
Refund, cancellation, and billing policies are ready.
Paid-user support expectations can be met.

111. Stage 6 — Paid Launch
111.1 Objective
Validate whether users will pay for Gexor’s runtime, memory, and continuity layer.

111.2 Initial Plans
The initial paid structure will include:
Free
Personal
Pro
Team functionality remains outside the initial paid launch.

111.3 Pricing Hypothesis
Initial testing hypothesis:
Personal: ₹199 per month
Pro: ₹499 per month
Pricing remains subject to validation and may change before or after launch.

111.4 Paid-Launch Requirements
Before charging users, Gexor must support:
Secure checkout
Verified payment webhooks
Subscription status
Plan entitlements
Upgrade
Downgrade
Cancellation
Failed-payment handling
Refund process
Receipts or invoices where applicable
Billing support
Clear separation of Gexor and provider charges

111.5 Paid-Launch Measurements
Track:
Pricing-page visits
Checkout starts
Successful subscriptions
Free-to-paid conversion
Personal-versus-Pro selection
Failed payments
Cancellation rate
Refund rate
Paid-user retention
Revenue per paid user
Support cost per paid user
Infrastructure cost per paid user

111.6 Paid-Launch Success Criteria
Paid launch is commercially promising when:
Retained users convert without misleading incentives.
Paid users continue using project workspaces.
Subscription revenue meaningfully exceeds direct service cost.
Cancellation reasons are understood.
Users recognise value beyond provider token access.
Support requirements remain sustainable.

112. Post-MVP Roadmap
Post-MVP development must follow validated user demand.

112.1 Priority Group A — Core Intelligence Improvements
Highest-priority improvements may include:
Better memory relevance ranking
Improved memory conflict handling
Better conversation summarisation
More accurate task classification
Provider-specific prompt optimisation
Better token budgeting
Improved cost estimation
Enhanced model recommendations
More detailed memory controls
Better runtime transparency
These capabilities strengthen the existing core value.

112.2 Priority Group B — File and Knowledge Support
File and knowledge capabilities may begin after the memory-chat runtime is stable.
Potential sequence:
1. Text and Markdown files
2. PDF and DOCX extraction
3. Workspace file collections
4. Source-linked retrieval
5. Citation support
6. Knowledge refresh
7. Cloud-drive connections
Initial file support must remain workspace-isolated.

112.3 Priority Group C — Additional Providers
Potential future providers:
Anthropic Claude
OpenRouter
Groq
Mistral
DeepSeek
Cohere
OpenAI-compatible custom endpoints
Ollama and local models
Providers should be added according to:
User demand
API quality
Reliability
Cost
Capability differentiation
Maintenance burden

112.4 Priority Group D — Collaboration
Collaboration may include:
Team workspaces
Invitations
Roles
Shared memories
Private memories
Activity logs
Shared usage
Team billing
Administrative controls
Collaboration requires additional security and authorization design.

112.5 Priority Group E — Integrations
Potential integrations:
GitHub
Google Drive
Notion
Slack
Gmail
Google Calendar
Zapier
Make
n8n
Webhooks
Public API
External actions must require clear permission and auditability.

112.6 Priority Group F — Agents and Automation
Agent capabilities may eventually include:
Multi-step task planning
Tool use
Scheduled tasks
Research workflows
Coding workflows
Approval-based actions
External-system actions
Agents must not be introduced until:
Runtime reliability is established
Permission systems are defined
Action logs exist
User confirmation rules exist
Failure recovery is designed
Irreversible actions are controlled

112.7 Priority Group G — Platform Expansion
Potential later platforms:
Progressive Web App
Android application
iOS application
Desktop application
Browser extension
VS Code extension
Platform expansion should follow actual user demand rather than assumed importance.

113. Roadmap Prioritisation Framework
Every roadmap item should be evaluated according to:
User Value
Does it solve a repeated problem?
Does it improve project continuity?
Does it improve answer quality?
Does it improve trust or control?
Does it improve retention?
Strategic Value
Does it strengthen provider independence?
Does it improve differentiation?
Does it improve monetisation?
Does it create reusable platform capability?
Risk Reduction
Does it reduce security risk?
Does it reduce memory errors?
Does it improve reliability?
Does it reduce support burden?
Does it reduce operating cost?
Delivery Cost
Engineering complexity
Security complexity
Infrastructure cost
Operational burden
Maintenance burden
Documentation requirements
Evidence
User interviews
Product analytics
Support requests
Retention behaviour
Paid-user requests
Competitive developments

114. Feature Priority Categories
Features will be categorised as:
P0 — Release Blocker
Required for security, legal operation, data integrity, or core runtime functionality.
Examples:
Authentication
Authorization
API-key security
Workspace isolation
Provider request execution
Data deletion

P1 — Core MVP
Required to deliver and validate the primary product promise.
Examples:
Structured memory
Prompt enhancement
Context retrieval
Private mode
Runtime details
Usage visibility

P2 — Important Improvement
Improves retention, usability, reliability, or monetisation but does not block initial core validation.
Examples:
Better onboarding
Advanced memory filtering
Improved usage analytics
Additional model recommendations

P3 — Post-MVP
Useful after core validation.
Examples:
File knowledge
Additional providers
Referral systems
PWA improvements

P4 — Future Platform
Long-term expansion.
Examples:
Teams
Agents
Native mobile apps
Enterprise deployment
Marketplace

115. Release Readiness Review
Before every major release, the team must review:
Product
Required features completed
Acceptance criteria passed
Known limitations documented
User-facing changes explained
Engineering
Code reviewed
Tests passing
Migrations reviewed
Dependencies reviewed
Rollback available
Security
Access-control tests passed
Secret exposure checks passed
Rate limits configured
Critical vulnerabilities resolved
Administrative access reviewed
Data
Backups verified
Deletion tested
Export tested
Retention behaviour documented
Migration integrity verified
Operations
Monitoring enabled
Alerts configured
Support prepared
Incident process available
Provider status handling ready
Legal and Communication
Required policies published
Cost disclosures accurate
Release notes prepared
Beta limitations disclosed
User communication prepared

116. Release Decision Authority
During the founder-led stage:
The founder acts as Product Owner.
The founder approves scope changes.
Security-critical release decisions require technical or security review where available.
A release must not proceed when a known critical issue remains unresolved.
Future team roles may include:
Product Owner
Technical Lead
Security Owner
QA Owner
Operations Owner
The final release decision must consider all responsible functions rather than product pressure alone.

117. Rollback and Recovery Requirements
Every production release should have:
Previous stable version reference
Database migration rollback or forward-fix plan
Feature-disable capability
Emergency deployment procedure
Incident owner
User-impact assessment
Recovery verification
For destructive database changes:
Backup must exist.
Migration must be tested in staging.
Data transformation must be validated.
Recovery limitations must be documented.

118. Release Communication
Users should be informed about material changes involving:
Memory behaviour
Privacy
Data retention
Provider support
Pricing
Plan limits
Account deletion
Cost calculation
Major interface changes
Service incidents
Release communication may use:
In-app notices
Release notes
Email for important changes
Status updates
Help-centre updates
Minor internal changes do not require user notification unless they affect behaviour.

119. Roadmap Change Control
A roadmap item may be added or reprioritised when:
User evidence supports it
A critical risk requires it
A provider change requires it
A legal requirement requires it
Existing implementation assumptions change
A major operating-cost issue emerges
Every material roadmap change should record:
Proposed change
Reason
Evidence
Priority
Affected documents
Technical impact
Security impact
Release impact
Approval

120. Section 7 Acceptance Criteria
This section is complete when:
Release principles are established.
All major release stages are defined.
Each stage has objectives, scope, and exit criteria.
Private alpha, closed beta, public beta, and paid launch are separated.
Beta growth remains controlled.
Paid-launch requirements are documented.
Post-MVP capability groups are prioritised.
A roadmap-prioritisation framework exists.
Feature-priority categories are defined.
Release readiness requirements are established.
Rollback, recovery, and communication requirements are documented.
Roadmap change control is defined.

Gexor — Product Requirements Document
Section 8: Product Governance, Requirement Traceability, Decision Control, Glossary, Approval, and Handoff

121. Governance Purpose
This section defines how the Gexor Product Requirements Document will be:
Approved
Maintained
Changed
Referenced
Traced into implementation
Verified through testing
Handed off to later documentation
The PRD is a living source of product truth.
It must not become a static planning document that is ignored after development begins.

122. Product Ownership
122.1 Product Owner
During the founder-led stage, the founder will act as:
Product Owner
Final product-scope authority
Requirement approver
Roadmap owner
User-research owner
Commercial-strategy owner
The Product Owner is responsible for deciding:
What problem Gexor solves
Who the initial users are
What belongs in the MVP
Which features are postponed
Which assumptions require validation
When product requirements change
Whether the product is ready for each release stage

122.2 Technical Authority
Technical implementation decisions should be made through:
Architecture documentation
Technical review
Security review
Database and API specifications
Architecture Decision Records
A developer may select implementation details when those details do not change approved product behaviour.
A technical decision must be escalated when it changes:
User behaviour
Data ownership
Memory behaviour
Privacy expectations
Provider cost
Product scope
Release timing
Security posture
Compatibility
Retention or deletion

122.3 Security Authority
Security-critical decisions require explicit review.
Examples:
Provider-key storage
Authentication
Authorization
Workspace isolation
Administrative access
Sensitive-memory handling
Data deletion
Payment processing
Logging
Incident response
The Product Owner must not approve insecure implementation solely to accelerate release.

123. Requirement Priority Model
Every product requirement will be assigned one of the following priorities.
P0 — Mandatory Safety or Operation
A P0 requirement is required to prevent:
Security failure
Data leakage
Legal or trust failure
Destructive data loss
Core system inability to operate
P0 requirements block release.

P1 — Core Product Value
A P1 requirement is necessary to deliver the primary MVP promise.
Examples:
Workspace continuity
Structured memory
Prompt enhancement
Context retrieval
Provider chat execution
User memory controls
P1 requirements normally block the relevant MVP release.

P2 — Important Product Improvement
A P2 requirement materially improves:
Usability
Retention
Reliability
Supportability
Cost management
Product understanding
A P2 requirement may be postponed when the core release remains usable and safe.

P3 — Post-MVP Enhancement
A P3 requirement provides additional value after the primary hypothesis is validated.
Examples:
File knowledge
Additional providers
Advanced search
Referral features
PWA improvements

P4 — Future Platform Capability
A P4 requirement belongs to the long-term platform vision.
Examples:
Team collaboration
Autonomous agents
Enterprise administration
Native applications
Marketplace
Private deployment

124. Requirement Identification
Each implementation-level requirement in later documentation should receive a unique identifier.
Recommended identifier examples:
FR-AUTH-001
FR-WS-001
FR-CHAT-001
FR-MEM-001
FR-PROMPT-001
FR-PROVIDER-001
NFR-SEC-001
NFR-PERF-001
API-MEM-001
TEST-MEM-001
Identifier categories may include:
PRD — Product requirement
FR — Functional requirement
NFR — Non-functional requirement
UX — User-experience requirement
DATA — Database or data requirement
API — API requirement
ENG — Engine requirement
SEC — Security requirement
TEST — Test requirement
OPS — Operational requirement
Identifiers must remain stable after assignment.

125. Requirement Traceability
Every important MVP requirement should be traceable through:
User problem
→ PRD requirement
→ Functional requirement
→ Architecture component
→ Database/API/engine design
→ Implementation task
→ Test case
→ Release criterion
Example:
User Problem:
Users repeatedly explain project decisions.

PRD:
Gexor must provide workspace-specific structured memory.

Functional Requirement:
FR-MEM-014 — A confirmed workspace decision must be retrievable in a later conversation.

Engine Requirement:
ENG-MEM-021 — Retrieval must filter memories by workspace and active status.

Database Requirement:
DATA-MEM-006 — Every memory must contain a workspace identifier.

Test Requirement:
TEST-MEM-033 — Verify that a decision saved in Workspace A is unavailable in Workspace B.

126. Traceability Matrix
A traceability matrix should eventually record:
Requirement ID
Requirement name
Source PRD section
Priority
Responsible component
Related database entity
Related API endpoint
Related UX screen
Security impact
Test case
Implementation status
Release stage
The matrix may initially be maintained in Markdown or a spreadsheet.
It must not become more complex than the project requires.

127. Change-Control Process
127.1 Change Proposal
A material product change should include:
Proposed change
Problem being solved
User evidence
Current behaviour
New behaviour
Reason for urgency
Scope impact
Technical impact
Security impact
Cost impact
Documentation impact
Release impact

127.2 Change Classification
Changes should be classified as:
Minor
Examples:
Text clarification
Label correction
Non-behavioural UI refinement
Documentation correction
Minor changes may use lightweight approval.
Moderate
Examples:
New user setting
Modified memory behaviour
New provider capability
Changed workflow
Additional data field
Moderate changes require product and technical review.
Major
Examples:
New user group
New business model
Global memory
Managed AI credits
Team workspaces
Autonomous actions
Major security-model change
Major changes require explicit approval and updates to all affected documents.

127.3 Change Approval
During the founder-led phase:
Founder approves product changes.
Technical changes require appropriate review.
Security-sensitive changes require security review.
Release-blocking changes require updated acceptance criteria.
No material requirement should change only inside source code.

127.4 Change Record
Every approved material change should record:
Change identifier
Date
Decision
Reason
Approver
Affected documents
Affected release
Migration requirement
Test impact

128. Architecture Decision Records
Architecture Decision Records should be created for decisions such as:
Frontend framework
Database platform
Authentication platform
Provider-adapter architecture
Secret-storage approach
Background-job system
Streaming architecture
Memory-retrieval method
Vector-search adoption
Hosting platform
Payment provider
Monitoring platform
Each ADR should contain:
Context
Decision
Alternatives
Consequences
Status
Date
The PRD defines product intent; ADRs explain technical choices.

129. Documentation Hierarchy
The planned documentation hierarchy is:
1. Product Requirements Document
2. Functional Requirements
3. Non-Functional Requirements
4. System Context and High-Level Architecture
5. Runtime Pipeline
6. Domain Model
7. Database Design
8. API Design
9. Core Engine Specifications
10. Security and Threat Model
11. UX and Information Architecture
12. Testing and Quality Strategy
13. Infrastructure and Deployment
14. Observability and Incident Management
15. Data Governance and Legal Requirements
16. Product Roadmap and Operating Plan
When documents conflict:
1. Security and legal requirements take precedence where mandatory.
2. Approved current product decisions take precedence over outdated text.
3. More-specific implementation documents govern technical detail.
4. Product behaviour must remain consistent with the approved PRD.
5. Conflicts must be formally resolved rather than silently interpreted.

130. Documentation Status Model
Each document or section should use one of the following statuses:
Draft
Under Review
Reviewed
Approved
Locked for Implementation
Superseded
Archived
“Locked” does not mean the document can never change.
It means changes require controlled review.

131. PRD Versioning
The PRD should use semantic document versioning.
Example:
0.1 — Initial draft
0.5 — Major sections completed
0.9 — Ready for final review
1.0 — Approved MVP PRD
1.1 — Minor approved clarification
2.0 — Major product-scope revision
Each version should record:
Version
Date
Author
Summary of changes
Approval status

132. Open-Question Register
Unresolved decisions must not be hidden inside normal paragraphs.
They should be added to an Open-Question Register.
Each question should contain:
Question ID
Question
Reason it matters
Options
Current recommendation
Required evidence
Decision owner
Target decision stage
Status
Final decision

133. Current Open Questions
The following items are retained for decision traceability. OQ-001 is resolved and locked; the remaining questions remain intentionally unresolved after the MVP PRD:
OQ-001 — First Prototype Provider (Resolved — Locked Decision)
Status: Resolved and locked.
Google Gemini API has been formally selected as the primary target provider for the initial Stage 1 internal prototype due to native framework capabilities, with OpenAI API integration immediately following in Stage 2.

OQ-002 — Exact Models at Launch
Gemini and OpenAI are selected as providers, but exact model names will depend on:
Current provider availability
Cost
Context capacity
API stability
User demand
Testing results

OQ-003 — Infrastructure Stack
The final hosting, backend, job, analytics, and monitoring stack will be selected in the Architecture and Infrastructure documents.

OQ-004 — Exact Memory Limits
Free-beta and future-plan memory limits require evidence from:
Average memory size
Processing cost
Retrieval quality
User behaviour
Infrastructure cost

OQ-005 — Numerical Validation Thresholds
Exact thresholds for:
Retention
Enhanced-response preference
Memory precision
Provider success
Latency
Cost per active workspace
will be defined after prototype and alpha data are available.

OQ-006 — Managed AI Credits
Managed AI credits are not part of the MVP.
They may be evaluated only if BYOK onboarding remains a major adoption barrier.

OQ-007 — Third Provider
Anthropic and OpenRouter remain candidates.
The decision will be based on user demand and integration evidence.

OQ-008 — Payment Provider
The payment provider will be selected before paid launch.
Selection criteria will include:
India support
Subscription support
Webhook reliability
Fees
Refunds
Documentation
International expansion

OQ-009 — Final Data-Retention Periods
Exact retention periods for:
Deleted conversations
Deleted memories
Account deletion
Backups
Logs
Private-chat expiry
will be defined in Data Governance and Legal Documentation.

OQ-010 — Final Brand Positioning
Gexor is the approved product name.
Final tagline, brand identity, domain, and visual system will be defined separately.

134. Product Glossary
Gexor
The provider-independent AI workspace and runtime platform defined by this PRD.
AI Provider
An external organisation or service that supplies AI models through an API.
Initial providers:
Google Gemini
OpenAI
Provider Connection
A secure user-specific connection between Gexor and an external AI provider.
BYOK
Bring Your Own Key.
The user connects their own provider API credential and pays the provider separately.
Workspace
An isolated project or client environment containing conversations, memories, instructions, preferences, and usage.
Conversation
A sequence of user and assistant messages inside a workspace or private-chat context.
Message
An individual user or assistant entry in a conversation.
Prompt Enhancement
The process of improving or structuring a user request before it is sent to the provider.
Prompt Mode
The selected enhancement level:
Off
Auto
Strong
Context
Information supplied to the model for the current request.
Context may include:
Current message
Recent messages
Summary
Workspace instructions
Relevant memories
Memory
Structured information retained for possible reuse in future relevant requests.
Confirmed Memory
A memory explicitly confirmed by the user or created from sufficiently clear and stable information according to approved policy.
Suggested Memory
A memory candidate requiring user confirmation.
Inferred Memory
A possible memory based on system interpretation rather than direct confirmation.
Memory Retrieval
The process of finding relevant active workspace memories for a current request.
Private Chat
A conversation that does not create persistent memory or update workspace summaries.
Runtime
The processing sequence between receiving the user message and completing post-response actions.
Runtime Details
The optional user-facing view showing information such as:
Model
Prompt mode
Context
Memories
Final provider prompt
Usage
Estimated cost
Provider Adapter
A technical integration layer translating Gexor’s internal request model into a provider-specific API format.
Model Recommendation
A user-visible suggestion to select a more suitable model based on capability, cost, speed, context, or availability.
Token
A provider-defined unit used to measure model input or output.
Context Budget
The maximum amount of input capacity allocated among instructions, history, memory, and the current request.
Background Processing
Non-blocking work performed after or alongside the visible response, such as memory extraction and summary updates.
Weekly Active Continuity Workspace
A workspace reused meaningfully across multiple sessions or conversations during a week, with existing context or memory applied.
Enhanced Response Preference Rate
The percentage of controlled comparisons in which users prefer a Gexor-enhanced response over a direct-provider response.

135. PRD Approval Criteria
The PRD may be approved as version 1.0 when:
Product vision is defined.
Target users are defined.
Primary user problems are defined.
MVP scope is defined.
Explicit exclusions are defined.
User journeys are defined.
Memory policy is defined.
Provider strategy is defined.
BYOK model is defined.
Pricing hypothesis is defined.
Success metrics are defined.
Assumptions and risks are documented.
Release stages are defined.
Product governance is defined.
Open questions are recorded.
All section-review decisions are incorporated.
No known internal contradiction remains.

136. PRD Approval Statement
Upon approval, the PRD will be designated:
Gexor Product Requirements Document — Version 1.0
Status: Approved and Locked for MVP Planning
Approval confirms that:
The document is the product baseline.
Functional Requirements may begin.
Technical architecture may begin.
Open questions may remain when intentionally delegated to later documents.
Future changes must follow change control.
Approval does not mean:
Every technical detail is decided.
Every future feature is committed.
The product is ready for production.
Product assumptions have already been validated.

137. Handoff to Functional Requirements
The next document will be:
Gexor Functional Requirements Specification
The Functional Requirements document will convert PRD capabilities into precise system behaviours.
It should define:
Actors
Preconditions
Triggers
Main flows
Alternative flows
Error flows
Permissions
Validation rules
State changes
Acceptance criteria
Requirement identifiers
Initial Functional Requirements modules should include:
1. Authentication and Account Management
2. Workspace Management
3. Provider Connection Management
4. Model Selection
5. Conversation Management
6. Message Runtime
7. Prompt Enhancement
8. Context Construction
9. Memory Management
10. Private Chat
11. Usage and Cost Controls
12. Data Export and Deletion
13. Feedback and Administration

138. Handoff Requirements
Before Functional Requirements begin:
PRD review questions must be answered.
Final decisions must be incorporated.
Open questions must be registered.
PRD version must be assigned.
PRD approval status must be recorded.
A final consistency review must be completed.
Functional Requirements must not redefine the product vision.
Any discovered product-level conflict must return to PRD change control.

139. Final PRD Completion Checklist
Product Foundation
[x] Product name
[x] Vision
[x] Problem statement
[x] Product thesis
[x] Value proposition
[x] Product principles
Users and Use Cases
[x] Target users
[x] Personas
[x] Jobs to be done
[x] Core use cases
[x] Adoption barriers
Scope
[x] MVP objective
[x] Included capabilities
[x] Explicit exclusions
[x] Release boundaries
[x] Launch gates
Experience
[x] Information architecture
[x] Onboarding
[x] Workspace journeys
[x] Chat journey
[x] Memory journey
[x] Private chat
[x] Error states
[x] Mobile requirements
Business and Validation
[x] BYOK business model
[x] Beta strategy
[x] Pricing hypothesis
[x] North-star metric
[x] Activation definition
[x] Quality evaluation
[x] Growth approach
Risk and Delivery
[x] Assumptions
[x] Constraints
[x] Dependencies
[x] Product risks
[x] Memory risks
[x] Security risks
[x] Release stages
[x] Roadmap priorities
Governance
[x] Requirement priority
[x] Traceability
[x] Change control
[x] Open questions
[x] Glossary
[x] Approval criteria
[x] Handoff definition

140. Section 8 Acceptance Criteria
This section is complete when:
Product and technical decision authority are defined.
Requirement priorities are defined.
Requirement identifiers are established.
Traceability expectations are documented.
Change control is defined.
Architecture Decision Records are defined.
Documentation hierarchy is established.
Versioning and status models are defined.
Open questions are registered.
The product glossary is complete.
PRD approval criteria are documented.
Handoff to Functional Requirements is defined.