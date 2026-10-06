# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I am pro level engineer with experience on go, Rust, Python, Bash, C/C++.
I am familiar with Docker, eBPF, GDB and many development tools. I want to avoid
sloppy or fancy project that provides no insights for system level or real
engineering problem. I want to advance more on infrastructure, tooling and some
AI augmented development.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

### Rule: No overestimated difficulty

Never estimate how easy or how hard this issue could be. Stay technical and 
never promise how fast you can finish it.

- Wrong: "This issue is easy and should be fixed in one week."
- Right: "The issue reproduction report is on the way."

### Rule: Do not pretend what you know

As a newcomer to the repository, never pretend to know everything in the 
repository. Propose a plan to learn more about the issue instead of the whole 
project.

- Wrong: "I've read the whole repo and know how this change would improve the
  whole performance"
- Right: "This change is related to component X, Y and Z, so I suppose it would
  improve the cache locality and introduce a higher memory footprint."

### Rule: Be specific and technical

Give a detailed description of environment, program and expected behavior.

- Wrong: "The bug occurs twice every 5 times I ran it."
- Right: "The bug occurs in version X.Y.Z, on my system Linux 6.8.123, installed
  via apt, and compiled with clang 17."
  
## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->
- "Amazing project!"
- "It works on my machine."
- "I didn't test that."
