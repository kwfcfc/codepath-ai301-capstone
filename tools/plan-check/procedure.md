# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. Read the **issue section and repro evidence first**. Record the reported bug behavior, the inputs or commands that reproduce it, and any evidence that constrains the possible cause.
2. Read the **candidate plan** only after the issue evidence is understood. Record:
   - the files named in the plan's scope;
   - the automated checks named in the test plan;
   - the plan's explanation of the bug's cause.
3. Use the issue evidence as the reference when later judging whether the plan's diagnosis is consistent with the reported behavior.
   
## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

For each required check, gather the following evidence:

- **Scope:**: Look where the plan says what it will change. Record each file explicitly named as a file the plan will modify.
- **Test:** Read the plan's test plan. Record the automated check the plan proposes and determine whether that check can visibly change from failing before the fix to passing after the fix. Do not count an existing automated check that already passes before the change.
- **Diagnosis:** Read the bug explanation in the issue section and the diagnosis in the candidate plan. Record the cause claimed by the plan and compare it with the evidence in the issue report. The diagnosis must explain the reported bug without contradicting that evidence.

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

- **Scope — P** only if every file changed in Git is mentioned in the plan's scope.
- **Test — P** only if the plan names an automated check that visibly flips from failing to passing because of the proposed fix. A check that already passes does not satisfy this requirement.
- **Diagnosis — P** only if the plan states what causes the bug described in the issue and that explanation does not contradict the evidence presented in the issue report.

Once the needed evidence for a check has been recorded, grade that check from the recorded evidence without re-reading the entire package unless the evidence is internally inconsistent.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

The verdict is **ready** only if every required check — **Scope, Test, and Diagnosis** — receives **P**.

If any required check receives **F** or **?**, the verdict is **hold**.

In the final grading output, report each check's grade and quote or summarize the specific evidence that determined it. For a `hold` verdict,
