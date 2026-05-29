# Copilot Agent Instructions

## Task: Find Missing OSP Model Repositories

When asked to find repositories that are missing from `templates.json`, perform the following search and filtering steps:

### 1. Gather Data

- **Search** for all public repositories in the GitHub organization [Open-Systems-Pharmacology](https://github.com/Open-Systems-Pharmacology) that have the topic **`osp-model`**. Use paginated search to retrieve all results (the organization may have 200+ matching repositories).
- **Parse** the file `templates.json` (on branch `update_12.3`) and extract all unique repository names from the `Url` fields. Each URL follows the pattern `https://raw.githubusercontent.com/Open-Systems-Pharmacology/<REPO_NAME>/<version>/<file>`.

### 2. Apply Filters

From the full list of `osp-model` repositories, **exclude** any repository that matches **any** of the following conditions:

| # | Condition |
|---|-----------|
| 1 | Repository name is exactly one of: `Glucose-Insulin-Model`, `Pregnancy-Models`, `Thyroid-Hormones-PB-QSP-Model` |
| 2 | Repository name starts **or** ends with `Example` (case-insensitive) |
| 3 | Repository name starts **or** ends with `DDI`, `DDGI`, or `Pediatrics` (case-insensitive) |
| 4 | Repository name already appears in any `Url` node of `templates.json` |
| 5 | Repository has **zero** releases (including pre-releases) — i.e., only keep repos that have **at least one** release |

### 3. Output

Print the final list of matching repository URLs, one per line, in the format:

```
https://github.com/Open-Systems-Pharmacology/<REPO_NAME>
```

### Notes

- All repositories in the search are public (the `osp-model` topic search in the org only returns public repos).
- When checking releases, include pre-releases — a repository with only pre-releases still counts as having a release.
- The GitHub search API returns at most 100 results per page; make sure to paginate through all pages.
- When extracting repo names from `templates.json` URLs, multiple templates may reference the same repository — deduplicate the list.
