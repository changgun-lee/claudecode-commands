# Jira to Commit Command

Convert a Jira issue to code changes and create a commit.

## Usage

```bash
jira_to_commit ISSUE-123
```

## What this command does

1. Fetches the specified Jira issue using Atlassian MCP
2. Analyzes the issue summary and description
3. Makes necessary code modifications based on the issue content
4. Creates a git commit with format: "ISSUE-123 issue summary"

## Implementation

You are a specialized assistant that converts Jira issues into code changes and commits.

Given a Jira issue key (e.g., ISSUE-123), you will:

1. **Fetch Jira Issue**: Use the Atlassian MCP tools to get the issue details
   - Use `mcp__atlassian__getAccessibleAtlassianResources` to get cloud ID
   - Use `mcp__atlassian__getJiraIssue` to fetch the issue details

2. **Analyze Issue Content**: Extract key information from:
   - Issue summary
   - Issue description  
   - Issue type (bug, feature, task, etc.)
   - Acceptance criteria or requirements

3. **Implement Changes**: Based on the issue content:
   - Search the codebase to understand the relevant files
   - Make necessary code modifications
   - Follow the project's coding standards from CLAUDE.md
   - Test the changes if possible

4. **Create Commit**: 
   - Stage the changes with `git add`
   - Create commit with message format: "{ISSUE-KEY} {issue summary}"
   - Include co-author attribution as per CLAUDE.md guidelines

## Error Handling

- If the issue key is not found, provide a clear error message
- If the issue description is unclear, ask for clarification
- If code changes are too complex, break them down into smaller tasks

## Arguments

- `issue_key`: The Jira issue key (e.g., PROJ-123) - required

## Examples

```bash
# Convert issue PROJ-123 to code changes and commit
jira_to_commit PROJ-123

# Result: Fetches issue, implements changes, creates commit "PROJ-123 Fix login validation bug"
```