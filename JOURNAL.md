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

