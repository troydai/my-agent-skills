# Rust Dev Setup Skill - Usage Guide

## Overview

The `rust-dev-setup` skill automates the process of preparing a Rust development environment. It's designed to be called by code agents to set up a clean, validated feature branch for development work.

## What It Does

1. ✅ Syncs the repository's default branch (main/master) with the remote
2. ✅ Creates a new feature branch with proper naming convention
3. ✅ Validates the setup with `cargo build`
4. ✅ Validates tests with `cargo test`
5. ✅ Stops the workflow if validation fails

## Installation

Upload the `rust-dev-setup.skill` file to Claude using the Skills menu in Settings.

## Usage Examples

### Example 1: Simple Setup

**User prompt:**
```
Set up a Rust dev environment for adding authentication feature
```

**What happens:**
1. Claude uses the skill to detect this is a Rust setup request
2. Runs the setup script with branch description "add-authentication"
3. Creates branch `feature/add-authentication`
4. Validates with cargo build and test
5. Reports success or any errors

### Example 2: Bug Fix

**User prompt:**
```
Prepare a Rust branch to fix the parser bug described in issue #123
```

**What happens:**
1. Skill is triggered
2. Creates branch `feature/fix-parser-bug` (or similar based on issue description)
3. Validates and reports status

### Example 3: Agent Workflow

When another AI agent needs to work on Rust code:

```
Agent: I need to implement feature X in the Rust codebase at ~/projects/my-app
Claude: [Uses rust-dev-setup skill]
       [Sets up feature/implement-feature-x branch]
       [Validates build and tests]
       [Hands over clean development environment]
```

## Script Usage

The skill includes `setup_rust_branch.py` which can be used directly:

```bash
# Basic usage
python3 setup_rust_branch.py /path/to/repo "feature-description"

# Skip tests (faster, only validates build)
python3 setup_rust_branch.py /path/to/repo "feature-description" --skip-tests
```

## Branch Naming

Branches follow the format: `feature/<description>`

**Good descriptions:**
- add-authentication
- fix-parser-bug
- implement-caching
- refactor-database

**Avoid:**
- Too vague: "fix", "update"
- Too long: "add-new-authentication-system-with-oauth"
- Wrong case: "Add-Authentication"

## Error Handling

The skill will stop and report errors if:

- Repository path doesn't exist
- Not a git repository
- Not a Rust project (no Cargo.toml)
- `cargo build` fails
- `cargo test` fails

Errors include:
- Full error output
- Debugging suggestions
- Recommended next steps

## Requirements

- Git repository already cloned locally
- Rust toolchain installed (cargo available)
- Network access to fetch from remote repository
- Repository has a default branch (main or master)

## Troubleshooting

**Issue:** "Not a Rust project" error
**Solution:** Ensure Cargo.toml exists in repository root

**Issue:** Build or test failures
**Solution:** Check error output, verify dependencies, ensure default branch is not broken

**Issue:** Branch already exists
**Solution:** Choose different name or delete existing branch

## Benefits

- **Consistency**: Every development session starts with a clean, validated environment
- **Safety**: Catches broken builds before development begins
- **Automation**: Eliminates manual Git operations and validation steps
- **Error Prevention**: Stops workflow if validation fails
- **Agent-Friendly**: Designed for seamless integration with AI code agents
