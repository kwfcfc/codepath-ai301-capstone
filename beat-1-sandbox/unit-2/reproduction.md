# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

kwfcfc
---

## Posted upstream

**Claim comment**

[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5862069638

```markdown
Hi, I'd like to pick up this issue. I plan to first run the `test_verify_with_wrong_hash_format`
unit test and write up a bug reproduction report. Then I will propose an exception handler for the
`verify_password` function when the `passlib.CryptContext` fails to decode malformed hashed
password.
```

**Reproduction comment**

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5862828554

~~~markdown
# Candidate Repro Report

Here is report about how I reproduce the issue with information about environment, program version,
steps, expected and actual behavior.

Environment:
- OS: macOS 26.6.2
- Python: 3.12.13
- Libraries:
  - bcrypt: 4.3.0
  - passlib: 1.7.4

Version: the program runs on commit `f89c06fc3ff292df2a04a39ac51319d32a76b779`

Steps:

1. use `uv` to install dependencies:

```bash
$ uv venv --relocatable .venv
$ uv pip install -e ".[dev]"
```

2. activate the python `venv` environment:

```bash
$ source .venv/bin/activate
```

3. I ran the python function `verify_password` directly with a malformed hash password:

```bash
$ python -c "from core.security import verify_password, hash_password
verify_password('password', 'not_a_valid_bcrypt_hash')"

Traceback (most recent call last):
  File "<string>", line 3, in <module>
  File "/private/tmp/pathreview-ai301-fa26-s1/core/security.py", line 37, in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/private/tmp/pathreview-ai301-fa26-s1/.venv/lib/python3.12/site-packages/passlib/context.py", line 2343, in verify
    record = self._get_or_identify_record(hash, scheme, category)
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/private/tmp/pathreview-ai301-fa26-s1/.venv/lib/python3.12/site-packages/passlib/context.py", line 2031, in _get_or_identify_record
    return self._identify_record(hash, category)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/private/tmp/pathreview-ai301-fa26-s1/.venv/lib/python3.12/site-packages/passlib/context.py", line 1132, in identify_record
    raise exc.UnknownHashError("hash could not be identified")
passlib.exc.UnknownHashError: hash could not be identified
```

4. I have also run `pytest` in a verbose mode to show the error trace back that tracks the error to
   the `passlib.context` identify record error. The test:

```bash
$ python -m pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v
============================= test session starts ==============================
platform darwin -- Python 3.12.13, pytest-9.1.1, pluggy-1.6.0 -- /private/tmp/pathreview-ai301-fa26-s1/.venv/bin/python
cachedir: .pytest_cache
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
hypothesis profile 'default'
rootdir: /private/tmp/pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: cov-7.1.0, asyncio-1.4.0, benchmark-5.3.0, hypothesis-6.168.2, pytest_httpserver-1.1.5, platformdirs-4.12.0, anyio-4.15.1
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collecting ... collected 25 items / 24 deselected / 1 selected

tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL [100%]

=============================== warnings summary ===============================
.venv/lib/python3.12/site-packages/passlib/utils/__init__.py:854
  /private/tmp/pathreview-ai301-fa26-s1/.venv/lib/python3.12/site-packages/passlib/utils/__init__.py:854: DeprecationWarning: 'crypt' is deprecated and slated for removal in Python 3.13
    from crypt import crypt as _crypt

core/config.py:7
  /private/tmp/pathreview-ai301-fa26-s1/core/config.py:7: PydanticDeprecatedSince20: Support for class-based `config` is deprecated, use ConfigDict instead. Deprecated in Pydantic V2.0 to be removed in V3.0. See Pydantic V2 Migration Guide at https://errors.pydantic.dev/2.13/migration/
    class Settings(BaseSettings):

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
================ 24 deselected, 1 xfailed, 2 warnings in 0.20s =================
```

Expected: The pytest should return `False` when verifying wrong hash format password.

Actual: The pytest throws `UnknownHashError: hash could not be identified`. It also throws two
        unrelated warnings about deprecated `crypt` and class-based `config` usage.


# AI usage disclosure

1. I used Claude Code with model Sonnet 5 and Opus 5 to help me set up Pyhton environment and learn
   usage about pytest. I ran all the commands in the steps above and draft the comment myself.
~~~


## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

- Run 1:
  categories: clear-accept 3/8  disclosure 0/1  no-evidence 4/4  unfollowable-comms 2/3  wrong-target 4/4
  agreement: 13/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in disclosure)
- Run 2:
  categories: clear-accept 7/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
  agreement: 19/20 scored items  (bar: 18/20: PASS)

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

| item | gold | verdict |
| ---  | ---  | --- |
| pkg-01 | accept  | reject  |

The failed check is: correct reproduction steps. This check asks for reproduction
report to follow the issue ste by step and use equivalent command and input. In
the pkg-01, the candidate use `http --offline ...` command, so the check fails
because it is not an equivalent command.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

One quoted check is:

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| correct reproduction steps | reproduction must follow the steps in the issue | the reproduction should follow the steps in the issue, and use equivalent command and input to reproduce the issue | required |

This asks candidate to follow the exact steps of commands and inputs to
successfullly reproduce the issue. If the candidate does not follow these steps,
they may fail to reproduce the issue or give false negative result.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

This check says equivalent commands but it does not distinguish whether an
argument is required for the reproduction. In the `pkg-01`, candidate used
`--offline` because it is sufficient to reproduce the issue by printing out the
headers instead of sending the actual request.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
