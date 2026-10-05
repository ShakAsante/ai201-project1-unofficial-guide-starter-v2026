# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:** This corpus is built from short administrative and student-life
facts, so a good answer is usually a single clear passage rather than a long,
multi-document explanation. I set the bar at 4 of 5 because one question may be
harder than the rest even in a good pipeline, but the system should still land on
the right chunk for the majority of the questions it is meant to answer.

---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:** In Campus Life, the same policy fact can be phrased in a few
different ways, and it is easy to sound confident without being grounded in the
actual documents. Requiring a source makes the answer auditable: if a fact cannot
be tied back to a document, it is not reliable enough for advising or deadlines.

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

<!-- The five questions are the ones in `OUT_OF_SCOPE` at the bottom of
     `questions.py`, and `run_eval.py` puts them through the gate and writes
     what happened into your run log. Swap them for your own if you'd rather —
     just keep five of them, or the "4 of 5" above has nothing to be 4 of. -->

**Why this target:** These questions are intentionally far outside the corpus and
should be easy to separate from real campus-life prompts. A 4-of-5 target is
strict enough to catch a bad gate, but realistic because some off-topic questions
can still sit close to the cutoff when the embedding model is fuzzy on wording.

---

## 4. Chunks must be a certain size

The chunks must be at least 200 characters and at most 400 characters, and no
chunk should have formatting issues.

**Why this target:** In this corpus, many useful passages are short factual
statements from policy pages or student advice threads, so chunks under 200
characters often lose context or are just headings with no real content. Chunks
above 400 characters start to mix multiple ideas together, which makes retrieval
less precise and makes it easier for the model to answer with the wrong detail.

---

## 5. Words in the corpus

The corpus should include the key words from the user question, or close
paraphrases of them, in the retrieved chunks.

**Why this target:** Campus Life questions are usually about very specific topics
like majors, deadlines, financial aid, housing, or course requirements, and those
ideas are often expressed with a narrow vocabulary. If the retrieved passage does
not contain the important terms from the question, the system is likely matching
on a loose similarity rather than on the actual subject matter.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
