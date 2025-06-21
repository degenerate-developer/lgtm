┌─────────────────────────────────────────────────────────────────────────────────────┐
│                    LGTM Protocol: Knowledge → Implementation Pipeline               │
└─────────────────────────────────────────────────────────────────────────────────────┘

INPUT: originalQuestion + userPrior (optional)
  │                                    
  ▼                                    
┌─────────────────────────────────────┐     ┌─────────────────────────────────────┐
│         INITIALIZATION              │────▶│        RUN FOLDER STRUCTURE         │
│                                     │     │  <runFolderPath>/                   │
│ 1. Evidence Gathering (AgentStep)   │     │  ├── worldview.json                 │
│    └─ UseTool(WebSearch/FileSearch) │     │  ├── knowledge/k_*.md               │
│ 2. Process → k_*.md (standardized)  │     │  ├── hypotheses/hyp_*.json          │
│ 3. Decompose → Areas {A_i}          │     │  ├── null_challenges/nc_*.json      │
│ 4. Generate Initial h_i per A_i     │     │  └── plan_synth_*_final.md          │
└─────────────────────────────────────┘     └─────────────────────────────────────┘
  │                                    
  ▼                                    
┌─────────────────────────────────────┐     
│    HYPOTHESIS REFINEMENT LOOP       │     ┌─────────────────────────────────────┐
│    (Iterate primitive)              │────▶│        STATE MANAGEMENT             │
│                                     │     │                                     │
│ FOR EACH h_i in parallel (Fork):    │     │  StateT Worldview M manages:        │
│ ├─ Critique existing hypothesis     │     │  • knowledgeBase.entries[]          │
│ ├─ Generate tactical questions      │     │  • areasOfAnalysis[]                │
│ ├─ AgentStep → search evidence      │     │  • microHypotheses[]                │
│ ├─ UseTool → gather new k_*.md      │     │  • hypothesisConflicts[]            │
│ ├─ Refine h_i → new version         │     │  • synthesisOutput                  │
│ └─ Validate → mark status           │     │                                     │
│                                     │     │  All file I/O via explicit          │
│ CONTINUE UNTIL convergence criteria │     │  primitives: WriteFile, ReadFile    │
└─────────────────────────────────────┘     └─────────────────────────────────────┘
  │                                    
  ▼                                    
┌─────────────────────────────────────┐     
│   NULL HYPOTHESIS CHALLENGE         │     ┌─────────────────────────────────────┐
│   (Parallel Fork execution)         │────▶│         EFFECT PRIMITIVES           │
│                                     │     │                                     │
│ FOR EACH candidate h_i:             │     │  Pipeline a = Free PipelinePrimF a  │
│ ├─ Identify falsification targets   │     │                                     │
│ ├─ Generate falsification queries   │     │  • GenText (LLM generation)         │
│ ├─ AgentStep → search counter-evid  │     │  • AgentStep (reasoning only)       │
│ ├─ UseTool → find contradictions    │     │  • UseTool (external tools)         │
│ ├─ Analyze evidence per target      │     │  • Fork/Join (parallel execution)   │
│ └─ Record outcome in nc_*.json      │     │  • Iterate (loops)                  │
│                                     │     │  • WriteFile/ReadFile/CreateDir     │
│ RESULT: Passed/Failed per h_i       │     │  • GetWorldview (state access)      │
└─────────────────────────────────────┘     └─────────────────────────────────────┘
  │                                    
  ▼                                    
┌─────────────────────────────────────┐     
│        SYNTHESIS PIPELINE           │     ┌─────────────────────────────────────┐
│                                     │────▶│        INTERPRETER LAYER            │
│ INPUT: Validated {h_i} only         │     │                                     │
│                                     │     │  interpret :: Pipeline a            │
│ 1. Analyze all validated h_i        │     │            -> StateT Worldview M a  │
│ 2. Generate unified narrative       │     │                                     │
│ 3. Extract implementation prereqs   │     │  • Executes primitives in M monad   │
│ 4. Identify key dependencies        │     │  • Updates Worldview state          │
│ 5. Validate synthesis output        │     │  • Handles parallel Fork execution  │
│                                     │     │  • Manages tool invocations         │
│ OUTPUT: synthesisOutput object      │     │  • Persists state via WriteFile     │
└─────────────────────────────────────┘     └─────────────────────────────────────┘
  │                                    
  ▼                                    
┌─────────────────────────────────────┐     
│       META-PLANNING PHASE           │     ┌─────────────────────────────────────┐
│                                     │────▶│           TOOLS ECOSYSTEM           │
│ 1. Generate base plan from synthesis│     │                                     │
│ 2. Create initial pipeline def      │     │  tools :: Map ToolID (Args->M Result)
│ 3. Optimize via Plan primitive      │     │                                     │
│ 4. Store optimized pipeline         │     │  Available Tools:                   │
└─────────────────────────────────────┘     │  • WebSearch                        │
  │                                         │  • CodebaseGrep                     │
  ▼                                         │  • FileSearch                       │
┌─────────────────────────────────────┐     │  • WriteFile                        │
│    FINAL PLAN GENERATION            │     │  • CreateDirectory                  │
│                                     │     │  • ReadFile                         │
│ 1. Execute optimized pipeline       │     │                                     │
│ 2. Generate relevant diagrams       │     │  Accessed via UseTool primitive     │
│ 3. Assemble final document          │     └─────────────────────────────────────┘
│ 4. Write plan_synth_*_final.md      │     
└─────────────────────────────────────┘     
  │                                    
  ▼                                    
OUTPUT: Complete Implementation Plan Document

┌─────────────────────────────────────┐
│           KEY FEATURES              │
│                                     │
│ • Explicit Effects: All I/O via     │
│   primitives (no hidden side fx)    │
│ • Modular: Each phase = Pipeline    │
│ • Parallel: Fork/Join for scale     │
│ • Traceable: Full provenance        │
│ • Testable: Null hypothesis checks  │
│ • Synthesized: Evidence-based plan  │
└─────────────────────────────────────┘

MATHEMATICAL FOUNDATION:
• Knowledge Category (𝓚): k_*.md standardized entries
• Hypothesis Category (𝓗): micro-hypotheses {h_i}  
• Implementation Category (𝓘): final plan components
• Natural Transformation η: 𝓗_synth → 𝓘 (synthesis to implementation)