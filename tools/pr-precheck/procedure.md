# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->

1. Read the **issue section and plan context first**. Record the reported bug behavior, the inputs or commands that reproduce it, and any evidence that constrains the possible cause. Record:
   - the files named in the plan's scope;
   - the automated checks named in the test plan;
   - the claims about intented pull request plan
2. Read the **diff** only after the issue evidence is understood. Record:
   - source code changes;
   - test file changes;
   - changelog notes
3. Use the test evidence as the reference when later judging whether the plan's test plan is consistent with the reported behavior.
4. note the commit messages as the reference for later pull request policy.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->

For each required check, gather the following evidence:

- **Scope:**: Look where the plan says what it will change. Record each file explicitly named as a file the plan will modify.
- **Test:** Read the plan's test plan. Record the automated check the plan proposes and determine whether that check can visibly change from failing before the fix to passing after the fix. Do not count an existing automated check that already passes before the change.
- **Diagnosis:** Read the bug explanation in the issue section and the expected result in the pull request plan. Record the solution claimed by the plan and compare it with the evidence in the issue report. The solution must explain the reported bug without contradicting that evidence.

Do not infer missing evidence. If the required evidence is not present in the package, record it as absent.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

Grade the required checks in this order: **Scope, Test, Diagnosis**.

- Give a check **P** when the gathered evidence satisfies its pass condition.
- Give a check **F** when the evidence shows that the pass condition is not satisfied, or when required evidence is absent.
- Give a check **?** only when relevant evidence exists but does not make the result clear enough to determine pass or fail.

Apply the checks as follows:

- **Scope — P** only if every file changed in Git diff is mentioned in the plan's scope.
- **Test — P** only if the plan names an automated check that visibly flips from failing to passing because of the proposed fix. A check that already passes does not satisfy this requirement.
- **Diagnosis — P** only if the plan states what causes the bug described in the issue and that solution does not contradict the evidence presented in the issue report.

Once the needed evidence for a check has been recorded, grade that check from the recorded evidence without re-reading the entire package unless the evidence is internally inconsistent.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->

The verdict is **ready** only if every required check — **Scope, Test, and Diagnosis** — receives **P**.

If any required check receives **F** or **?**, the verdict is **hold**.

In the final grading output, report each check's grade and quote or summarize the specific evidence that determined it. For a `hold` verdict,
