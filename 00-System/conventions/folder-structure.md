# Folder Structure Convention

Every company and product follows the same internal skeleton:

  CLAUDE.md, product/ (or company/), architecture/, research/, meetings/, decisions/

Rules:
- New company → copy `01-Companies/YourCompany` skeleton
- New product → copy `YourCompany/products/YourProduct` skeleton
- Colocate by scope, not by type: `meetings/`, `decisions/`, `research/` live inside
  every scope, not as one global folder
- Retire → move the whole subtree into `99-Archive/`, preserving its original path
