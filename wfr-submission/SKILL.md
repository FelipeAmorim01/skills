---
name: wfr-submission
description: >
  Guides users through preparing and submitting functions to the Wolfram Function Repository (WFR),
  ensuring compliance with official formatting, documentation, and quality standards. Use this skill
  whenever the user mentions the Wolfram Function Repository, WFR, submitting or publishing a Wolfram
  function, writing a Definition notebook, asking about WFR guidelines, requirements, style rules, or
  best practices — even if they don't say "submission guide". Also trigger when the user wants to
  update or republish an existing WFR entry, asks about Publisher IDs, ResourceFunction, or
  DefineResourceFunction in the context of sharing their work publicly. When in doubt, use this skill.
---

# Wolfram Function Repository (WFR) Submission Guide

Guides users through the full process of preparing, documenting, and submitting functions to the
[Wolfram Function Repository](https://resources.wolframcloud.com/FunctionRepository) — the curated,
open platform for extending the Wolfram Language.

Official style guidelines: https://resources.wolframcloud.com/FunctionRepository/style-guidelines

> **Important:** Submissions should always be made through the **Definition Notebook**, downloaded
> from the WFR website. Do not guide users toward programmatic submission via Wolfram Language
> symbols such as `ResourceSubmit`, `DefineResourceFunction`, etc.

---

## 1. Before You Start

### Publisher ID
- Users must have a Publisher ID in order to submit a function to the Wolfram Function Repository. Have the user evaluate `$PublisherID` in a notebook and check what the publisher id is. If the user doesn't have one, request it at:
  https://resources.wolframcloud.com/publisher/request-publisher-id
- To **update** a published function, you must be connected to the same Publisher ID used for
  the original submission. Check a published function's Publisher ID with
  `ResourceObject[...]["ContributorInformation"]`.

### Avoiding Duplicates

- Search the repository at https://resources.wolframcloud.com/FunctionRepository before submitting.
- Submissions must not substantially replicate existing functions or symbols.
- If you have many related functions, consider submitting a **paclet** to the
  [Wolfram Language Paclet Repository](https://resources.wolframcloud.com/PacletRepository)
  instead of multiple separate WFR submissions.

---

## 2. Getting the Definition Notebook

Download the blank Function Repository Definition Notebook directly from the WFR website:
https://resources.wolframcloud.com/FunctionRepository/Unnamed-Function.nb

This notebook is the required starting point for all submissions. Fill in each section as
described below.

---

## 3. Code (Definition Section)

- Use `SetDelayed` (`:=`) for all function definitions.
- The definition must be **standalone** — no external sources (GitHub, cloud objects, etc.) may be
  loaded. All dependencies must be included in the Definition section.
- Long definitions should be **split across multiple cells** for readability.
- Functions should perform only the specified computation — avoid undocumented or unexpected side effects.
- There should be **only one symbol** (the function name) that users interface with.
- Avoid placing all dependent helper functions inside a `Module` as local symbols.

### Options

- Use **existing** Wolfram Language option symbols (e.g., `Method`, `MaxItems`) or strings for
  option names. New symbols used for option names won't work correctly in resource functions due
  to context handling.
- Implement options using `OptionsPattern` and `OptionValue` so users can pass options as symbols.
- **Do not** include options in usage messages — document them in Details & Options only.

### Parallel Computing Note

When using `ParallelMap` or other parallel functions, your symbols won't be in the global context
by default inside a resource function. You may need to adjust `$DistributedContexts`. See the
Advanced Topics section of the style guidelines for details.

---

## 4. Documentation

### Title & Description

- Function names should be **as specific as possible** to reflect functionality and avoid overlap.
  Single common words (e.g., `Step`, `Turn`) are rarely specific enough.
- The description below the name should be a brief, plain-text, stand-alone sentence beginning
  with an **imperative verb**, with **no ending punctuation**.

### Usage Messages

- Write **one usage message per argument specification**.
- Each usage (input pattern + text) should form a complete sentence ending with a period.
- **Template** every argument name and every reference to a built-in Wolfram Language symbol
  using the **"Template Input"** button in the Tools menu.
- Options must not appear in usage messages.

### Details & Options

- Document all options in a **three-column table** (no header row): option name | default value | brief description.
- Option names that are built-in symbols should be linked to their documentation via "Template Input".
- Use straight quotes (`"`) not curly quotes for strings.
- If the function requires an **API key**, document this clearly here.
- If the function pulls data from **external sources** (websites, databases), document this here
  with links to those sources.
- To add hyperlinks: select text → **Insert → Hyperlink**.

---

## 5. Examples

- Every example must have a **preceding text caption** ending in a colon.
- Captions should be brief — typically one sentence, no more.
- Move detailed commentary to Details & Options, not into example captions.
- Each example should be **short** and explicitly use the submitted function.
- More elaborate demonstrations belong in **Applications** or **Neat Examples** sections.
- Separate multiple examples within a section using the **"Insert Delimiter"** button in the Tools bar.
- Examples that depend on definitions from previous cells **must not** be separated by delimiters.
- Every input pattern in the usage messages should have a corresponding example.

---

## 6. Source & Additional Information

- **Keywords** are mandatory — fill these out.
- **Related Symbols**: include symbols with similar purposes in the same knowledge area.
  Do not include symbols merely used to implement the function internally.
- Search across all Wolfram repositories (not just the Function Repository) to find related
  Resource Objects to link.

### Author Notes (optional)

Use for background, implementation details, possible improvements, or version notes that fall
outside the scope of the main documentation.

### Submission Notes

Use to communicate with the WFR review team — especially useful when submitting an update to
explain what has changed.

---

## 7. Final Checks & Submission

1. Click the **Check** button in the notebook toolbar to identify errors and recommendations.
2. Run a spell check: **Edit → Check Spelling**.
3. Click the **Deploy** button to deploy the function to the cloud and test it live.
4. When satisfied, click the **Submit** button in the notebook to submit to the WFR team for review.
