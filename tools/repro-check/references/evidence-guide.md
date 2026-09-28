# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

Look for line that starts with "Environment" or "Version" in the candidate's
repro report. Look for the program version, the system version, runtime version 
and installing method.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->
Look for line that starts with `Steps` in the repro report section. Look for 
the following commands it runs, or the instructions on how to run the program.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->
From the command line, look for the terminal output, screenshots, error messages 
and return values. Look for the line that starts with `Actual`.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

Compare the candidate's report claim comment and `Actual` statement with the 
issue and repo facts. Look for whether the reported results matched the log, 
terminal output, screenshots, error messages or return value. 

A good report distinguishes between actual behaviors and assumptions from the 
issue. If the issue cannot be reproduced, the report states that clearly and 
records the reproduction attempt.


## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

Compare the claim comment with the issue template, comment template and general 
guide for contribution and relavent documents in the repo. Make sure to review 
voice guide to adjust the tone and voice. Follow the issue's comment thread and 
the repo's communication requirements, including AI usage and disclosure.

A good claim comment follows all the rules, desribes specific issue and 
reproduction process, and pass the voice guide checks.
