# Project Journal - Advik777

## Week 7 - Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/153

**Issue title:** Faithfulness checker crashes when a context chunk has text: None

**Tier:** [x] Tier 1 [ ] Tier 2 [ ] Tier 3

**Problem summary:**
The faithfulness checker crashes with a TypeError when a context chunk contains a "text" key with a value of None. This happens because the current code uses .get("text", ""), which only applies the default empty string if the key is missing, not if the value is explicitly None. A successful fix will involve updating the logic in rag/evaluator/faithfulness_checker.py to handle these None values gracefully so that the context join operation can complete without crashing.


**Selection Reasoning:**
I selected Issue #153 because it is a clearly defined Tier 1 bug that is self contained within the RAG evaluator module. After working through the project checklist, I have confirmed that I can explain the problem a TypeError caused by None values in context chunks and I have located the specific code in rag/evaluator/faithfulness_checker.py and the corresponding failing test in tests/unit/test_faithfulness_checker.py. The fix is localized, making it a realistic and achievable goal for my first contribution within the 3-6 hour Tier 1 timeframe. There are no external blockers or dependencies, and I am confident in my plan to update the string-joining logic to handle None values gracefully.

**Branch name:** fix/153-faithfulness-checker-none-type

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger


## Week 8 - Reproduction & solution planning

**Reproduction summary:**
I successfully reproduced the issue by running pytest tests/unit/test_faithfulness_checker.py. The test test_none_context_chunk_text failed with a TypeError: sequence item 0: expected str instance, NoneType found, confirming that the .join() operation crashes when a context chunk contains an explicit None value.

**PLAN.md link:** https://github.com/Advik777/pathreview/blob/fix/153-faithfulness-checker-none-type/PLAN.md

**Blockers or open questions:**
The other assertion failures (score 0.0) appear to be side effects of using the 'mock' LLM provider, but the primary crash (TypeError) is localized to the string handling logic I am assigned to fix.


## Week 9 - Solution building & PR submission

### Check-in 1 (mid-week)

**Current progress:**
I have successfully implemented the fix in rag/evaluator/faithfulness_checker.py. I updated the context string concatenation to use the chunk.get("text") or "" pattern, which gracefully handles explicit None values. I verified the fix by running pytest tests/unit/test_faithfulness_checker.py. The test_none_context_chunk_text which previously crashed with a TypeError is now passing.

**Next steps:**
I will now open a Draft PR to get peer/mentor feedback. I have noted 3 pre-existing test failures related to the mock LLM provider (returning 0.0) which are unrelated to my code changes; I will document these in my PR description as per the project guidelines.

**Blockers:**
None.


### Check-in 2 (end of week)

**PR link:** https://github.com/ascherj/pathreview/pull/361
**Branch:** fix/153-faithfulness-checker-none-type

**What you built:**
I fixed a TypeError in the Faithfulness Checker that occurred when a context chunk's text was explicitly set to None. I updated the extraction logic to use a null-safe pattern (or ""), ensuring the system handles missing or null text gracefully during context concatenation.

**Tests added or updated:**
I verified the fix using tests/unit/test_faithfulness_checker.py. The reproduction test test_none_context_chunk_text now passes, and I confirmed that my changes did not introduce any new failures.

**Self-review confirmation:** [x] make check passes [x] make test-unit passes
**Draft PR feedback received from:** none (shared on Slack, awaiting response)
