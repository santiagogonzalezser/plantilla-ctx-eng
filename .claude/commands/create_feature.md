# Command: create_feature <title> <prompt>
- Find last number in /features using `ls /features` (if none, start at 001).
- Create new folder: /features/feature_00X_{title}/
- Inside that folder:
  - Write INITIAL.md with the <prompt> and use /features/templates/INITIAL_base.md as template.
  - Create empty PRP.md (header only).
  - Create RESULT.md with header "# RESULT".
  - Create ITERATIONS.md with header "# ITERATIONS".