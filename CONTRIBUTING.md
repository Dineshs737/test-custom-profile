# Contributing to Animated GitHub Profile Generator

First off, thanks for taking the time to contribute! 🎉

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check existing issues. When creating a bug report, include as many details as possible:

**Bug Report Template:**

```markdown
**Describe the bug**
A clear description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Go to '...'
2. Click on '....'
3. See error

**Expected behavior**
What you expected to happen.

**Screenshots**
If applicable, add screenshots.

**Environment:**
 - OS: [e.g. Windows, macOS, Linux]
 - Node Version: [e.g. 18.0.0]
 - NPM Version: [e.g. 9.0.0]

**Additional context**
Add any other context about the problem.
```

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, include:

- **Clear title** and description
- **Use case** - Why is this enhancement useful?
- **Examples** - Show how it would work
- **Alternatives** - Other solutions you've considered

### Pull Requests

1. Fork the repo and create your branch from `main`
2. Make your changes
3. Test your changes thoroughly
4. Update documentation if needed
5. Submit a pull request

**Pull Request Template:**

```markdown
**Description**
Brief description of changes

**Type of change**
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

**Testing**
How has this been tested?

**Checklist:**
- [ ] Code follows project style
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] No new warnings
- [ ] Tests added/updated
```

## Development Setup

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/github-profile-generator.git

# Install dependencies
npm install

# Create a branch
git checkout -b feature/my-feature

# Make changes and test
npm run build
npm run generate

# Commit with conventional commits
git commit -m "feat: add new theme"

# Push and create PR
git push origin feature/my-feature
```

## Commit Message Guidelines

We follow [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation only
- `style:` Formatting, missing semicolons, etc.
- `refactor:` Code change that neither fixes a bug nor adds a feature
- `test:` Adding tests
- `chore:` Updating build tasks, package manager configs, etc.

Examples:
```
feat: add dark mode toggle
fix: resolve token expiration issue
docs: update installation guide
style: format code with prettier
```

## Code Style

- Use TypeScript
- Follow existing code structure
- Use meaningful variable names
- Add comments for complex logic
- Keep functions focused and small

## Testing

Before submitting PR:

```bash
# Build
npm run build

# Test generation
export GITHUB_TOKEN=your_token
npm run generate

# Verify files created
ls -la profile.svg README.md
```

## Documentation

- Update README.md for user-facing changes
- Add JSDoc comments for functions
- Update troubleshooting guide if needed

## Community

- Be respectful and inclusive
- Help others in discussions
- Share your customizations
- Star the repo if you like it!

Thank you for contributing! 🚀
