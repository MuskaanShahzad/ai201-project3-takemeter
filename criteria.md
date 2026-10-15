# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1. Overall accuracy

Overall accuracy on the held-out test set is at least 0.65.

**Why this target:** Three labels means a coin-flip guesser gets about 33%. 0.65 is a real jump above chance without assuming more than a small fine-tuned model on ~200 examples can plausibly deliver.

---

## 2. Per-label performance

Every label has an F1 of at least 0.55 on the held-out set, except `discussion`, which only needs 0.45.

**Why this target:** In the ~16 real posts I read while designing the taxonomy, `discussion` showed up least often of the three (roughly 3 of 16). I expect it to be my smallest label with the jumpiest test-split score, so it gets a looser bar than `build_log` and `bare_ask`.

---

## 3. Balance

No single label exceeds 65% of the 200 labeled examples.

**Why this target:** `bare_ask` looked like it could dominate — close to half of what I read fit it. Setting the ceiling under the brief's hard 70% cap leaves margin before the model just learns to guess that label.

---

## 4. Consistency

Re-labeling the same 20 posts, blind to my first pass, I'd match myself on at least 85% of them.

**Why this target:** The `discussion` vs. `bare_ask` boundary has a written decision rule, but it still takes judgment ("is this fundamentally seeking an answer?"). 85% leaves room for a few genuinely hard calls to land differently without meaning I'm applying the rule arbitrarily.

---

## 5. Confidence

Accuracy on the model's most-confident third of test predictions is at least 15 points higher than accuracy on its least-confident third.

**Why this target:** If confidence doesn't track correctness at all, the model is probably pattern-matching something spurious rather than the real distinction between labels. A 15-point gap is meaningful but realistic for a model that's actually learned something.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
