# Git Conventions

## Commit Message Guidelines

### Format
```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types
- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation only changes
- **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **perf**: A code change that improves performance
- **test**: Adding missing tests or correcting existing tests
- **build**: Changes that affect the build system or external dependencies
- **ci**: Changes to CI configuration files and scripts
- **chore**: Other changes that don't modify src or test files
- **revert**: Reverts a previous commit

### Scope
The scope should be the name of the npm package affected (as perceived by the person reading the changelog generated from commit messages).

### Subject
- Use the imperative, present tense: "change" not "changed" nor "changes"
- Don't capitalize the first letter
- No dot (.) at the end
- Limit to 50 characters

### Body
- Use the imperative, present tense: "change" not "changed" nor "changes"
- Include motivation for the change and contrast with previous behavior
- Wrap at 72 characters

### Footer
- Reference GitHub issues and pull requests
- Note breaking changes starting with "BREAKING CHANGE:"

## Example Commit Messages

### Simple feature
```
feat(auth): add OAuth2 integration for Google login
```

### Bug fix with description
```
fix(api): prevent race condition in user data fetch

The previous implementation could cause duplicate API calls when
multiple components requested user data simultaneously. This fix
adds a caching layer with request deduplication.

Fixes #123
```

### Breaking change
```
feat(api): update authentication endpoint structure

BREAKING CHANGE: Authentication endpoints have been reorganized.
/api/auth/login is now /api/v2/auth/signin
/api/auth/logout is now /api/v2/auth/signout
```

## Branch Naming Conventions

### Format
```
<type>/<ticket-number>-<short-description>
```

### Examples
- `feature/PROJ-123-add-user-dashboard`
- `fix/PROJ-456-resolve-login-error`
- `hotfix/PROJ-789-critical-security-patch`
- `chore/update-dependencies`

### Branch Types
- **feature**: New features or enhancements
- **fix**: Bug fixes
- **hotfix**: Urgent fixes for production
- **release**: Release preparation branches
- **chore**: Maintenance tasks

## Pull Request Guidelines

### Title Format
Should follow the same convention as commit messages:
```
<type>(<scope>): <description>
```

### PR Description Template
```markdown
## Description
Brief description of what this PR does.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update

## How Has This Been Tested?
Describe the tests that you ran to verify your changes.

## Checklist
- [ ] My code follows the style guidelines of this project
- [ ] I have performed a self-review of my own code
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] I have made corresponding changes to the documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing unit tests pass locally with my changes
```

## Git Workflow

### Feature Development
1. Create feature branch from `main`
2. Make commits following conventions
3. Push branch and create PR
4. Address review feedback
5. Squash and merge to `main`

### Hotfix Process
1. Create hotfix branch from `main`
2. Apply fix with appropriate commits
3. Test thoroughly
4. Create PR with "hotfix" label
5. Merge to `main` after approval
6. Tag release if needed

### Release Process
1. Create release branch from `main`
2. Update version numbers
3. Update changelog
4. Create PR to `main`
5. After merge, tag the release
6. Deploy to production