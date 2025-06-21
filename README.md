# LGTM Protocol V1

lgtm is a meta-prompt i use with my cursor agent when working on a high-complexity task.
it helps me avoid wasting hours finding every bit of context for complex prompt requests.
think of it as a budget deep-researcher with real-time interpretability.

## Usage

1. copy the contents of `.prompts/` (`mm-protocol.md` optional) into your project directory.
2. open a new cursor agent instance, copy and paste (use `command+shift+p`)
   the contents of `.prompts/usage.txt` into the prompt input box.
3. drag `@lgtm-protocol.md` into the prompt input box.
4. at the bottom of the prompt input, type the problem you're trying to solve.
5. run the prompt. once done, you can check and approve the generated report.

- i recommend using claude 4 sonnet for this. unless you're loaded, don't use max mode.
- any frontier reasoning model works, but they all create wildly different experiences.

- still provide as much context as possible when describing the actual problem.
- if the agent is going in the wrong direction, stop the chat and give it feedback.

- you can observe the research process in real-time by reading through generated files.
- create follow-up research queries by running lgtm again alongside `./prompts/runs/`.

- WARNING: LLM hallucinations can compound errors and the protocol is not always followed in its entirety. always check the generated plan before approving it.

## MM Protocol (very-experimental)

I use `mm-protocol.md` to edit the structure of the `lgtm-protocol.md`.

The Meta-Meta Protocol is a meta-meta-prompt that is used for editing meta-prompts.

I tried to define the categories in such a way that they can be used to model every agentic pattern from the "Building effective agents" article by anthropic.

I also tried to ensure that the mm protocol would make changes in a more effective way by specifying certain mathematical properties.

## QAs

### q: how does lgtm protocol work?

### a: it came to me in a dream. then i vibe-coded most of the math.

### q: can you give me a better explanation?

### a: i tried to formally model the academic research process for coding; find evidence, identify gaps in research, create and challenge hypotheses, then finally write a pape. your task proposal paper.

### q: what's with the strange language in the prompt?

### a: some guy in a harvard basement showed me the magic of category theory. i thought it could be a nifty tool for modeling agentic processes more formally. the meta-prompt evolved into haskell at some point after several generations.

### q: anything else?

### a: if you're interested in learning more, check out the `diagram/` folder to see generated ascii diagrams of protocols. also i think inference-time scaling will make lgtm's approach more viable over time.
