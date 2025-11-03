# AI Claude Code - CLAUDE.md Development System

> **Minimalist yet powerful AI-assisted development framework**
> Production-ready • Opinionated • Tech-stack agnostic • Token-optimized

[![Version](https://img.shields.io/badge/version-1.1.0-blue.svg)](CLAUDE.md)
[![Status](https://img.shields.io/badge/status-production%20ready-brightgreen.svg)](CLAUDE.md)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

---

## 🚀 Quick Start (60 Seconds)

```bash
# 1. Copy to your project
cp -r /path/to/ai-claude-code/{CLAUDE.md,.agent} ./

# 2. Start coding with AI
# That's it! AI automatically follows guardrails.
```

**The system works immediately:**
- ✅ AI loads [CLAUDE.md](CLAUDE.md) automatically (400 lines of guardrails)
- ✅ Language guides auto-load based on file extensions
- ✅ Workflows available when you need them
- ✅ Progressive - starts minimal, grows with your project

📖 **[Read the full Quick Start Guide →](AI_INSTRUCTIONS.md)**

---

## 💡 What Is This?

An **opinionated AI development framework** designed for Claude Code and similar AI assistants.

### Key Features

- **35+ Specific Guardrails** - Not vague suggestions, but testable rules
- **4 Language Guides** - TypeScript, Python, Go, Rust (auto-loading)
- **4 Workflows** - PRD creation, task generation, initialization, troubleshooting
- **3 Modes** - ATOMIC/FEATURE/COMPLEX (scales from bugs to architecture)
- **4D Methodology** - Deconstruct → Diagnose → Develop → Deliver

### Philosophy

> Small, validated changes. Quality enforced. Documentation grows organically.

---

## 📖 Documentation

| Document | Purpose | When to Read |
|----------|---------|--------------|
| [AI_INSTRUCTIONS.md](AI_INSTRUCTIONS.md) | **Quick Start Guide** | Read this first |
| [CLAUDE.md](CLAUDE.md) | Core guardrails & methodology | AI loads automatically |
| [.agent/README.md](.agent/README.md) | .agent/ folder structure | When customizing |

### Language Guides (Auto-Load)

- [TypeScript/JavaScript](.agent/language-guides/typescript.md) - `.ts`, `.tsx`, `.js`, `.jsx`
- [Python](.agent/language-guides/python.md) - `.py`
- [Go](.agent/language-guides/go.md) - `.go`
- [Rust](.agent/language-guides/rust.md) - `.rs`

### Workflows (On-Demand)

- [Initialize Project](.agent/workflows/initialize-project.md) - Setup new/existing projects
- [Create PRD](.agent/workflows/create-prd.md) - Plan complex features
- [Generate Tasks](.agent/workflows/generate-tasks.md) - Break PRDs into tasks
- [Troubleshooting](.agent/workflows/troubleshooting.md) - Debug systematically

---

## 🎯 Use Cases

### New Project
```bash
@.agent/workflows/initialize-project.md
"Initialize a new [TypeScript/Python/Go/Rust] project"
```
AI asks about tech stack, creates directory structure, config files, and `.agent/project.md`.

### Existing Project
```bash
@.agent/workflows/initialize-project.md
"This is an existing project - analyze the codebase"
```
AI scans tech stack, extracts patterns, creates `.agent/project.md` and `.agent/patterns.md`.

### Simple Feature
```
"Fix the login button alignment"
```
AI uses **ATOMIC mode** - single file, quick fix, tests, commit.

### Complex Feature
```bash
@.agent/workflows/create-prd.md
"Build user authentication with OAuth"
```
AI creates structured PRD, generates task breakdown, implements step-by-step.

---

## 🛠️ How It Works

### The 3 Modes

**ATOMIC** (<5 files, clear scope)
- Direct implementation
- Quick validation
- One commit
- Example: Bug fixes, styling, simple features

**FEATURE** (5-10 files)
- Break into 3-5 subtasks
- Implement sequentially
- Integration testing
- Example: New component, API endpoint, refactoring

**COMPLEX** (>10 files, new subsystem)
- Optional: Create PRD
- Generate task breakdown
- Step-by-step implementation
- Example: Authentication, payments, analytics

**AI auto-detects which mode to use.**

### The Guardrails (35+ Rules)

**Code Quality:**
- ✓ Functions ≤50 lines
- ✓ Files ≤300 lines
- ✓ Complexity ≤10 per function
- ✓ All exports have types/docs

**Security (CRITICAL):**
- ✓ All inputs validated
- ✓ Parameterized queries only
- ✓ No secrets in code
- ✓ Dependencies checked for vulnerabilities + licenses

**Testing (CRITICAL):**
- ✓ >80% coverage for business logic
- ✓ >60% overall coverage
- ✓ Tests for all public APIs
- ✓ Regression tests for bugs

**Git:**
- ✓ Conventional commits (`feat:`, `fix:`, etc.)
- ✓ One logical change per commit
- ✓ All tests pass before push
- ✓ PRs required (no direct commits to main)

**[See all guardrails in CLAUDE.md →](CLAUDE.md)**

---

## 📊 System Stats

- **Version**: 1.1.0
- **Status**: Production Ready
- **Total Files**: 15 markdown files
- **Total Lines**: 5,851 lines of documentation
- **CLAUDE.md**: 400 lines (60% more efficient than v1.0)
- **Token Efficiency**: ~1,600 tokens base context (vs. 4,000 before)

---

## 🎓 Learning Path

### Week 1: Learn the Basics
- [ ] Initialize your first project
- [ ] Write 5 features using ATOMIC mode
- [ ] Review guardrails in [CLAUDE.md](CLAUDE.md)
- [ ] Check which language guide applies to you

### Week 2: Try Complex Features
- [ ] Use PRD workflow for a medium feature
- [ ] Generate task breakdown
- [ ] Implement step-by-step
- [ ] Notice how `.agent/project.md` grows

### Week 3: Customize
- [ ] Add project-specific patterns to `.agent/patterns.md`
- [ ] Create first decision log in `.agent/memory/`
- [ ] Review and refine `.agent/project.md`
- [ ] Experiment with different modes

---

## 🤝 Contributing

Contributions welcome! This system is designed to be:
- **Customizable** - Adapt to your workflow
- **Extensible** - Add language guides, workflows, patterns
- **Community-driven** - Share improvements

**To contribute:**
1. Fork this repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

**Ideas for contributions:**
- Additional language guides (Java, C#, PHP, etc.)
- Framework-specific templates (React, Django, Rails, etc.)
- Validation scripts for guardrails
- Integration with other AI assistants
- Real-world case studies

---

## 📄 License

MIT License - See [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

Built with:
- **Claude Code** - Anthropic's AI coding assistant
- **4D Methodology** - Systematic problem-solving approach
- **Community feedback** - Continuous improvement

---

## 📞 Support

- **Documentation**: [AI_INSTRUCTIONS.md](AI_INSTRUCTIONS.md)
- **Issues**: [GitHub Issues](https://github.com/ar4mirez/ai-claude-code/issues)
- **Discussions**: [GitHub Discussions](https://github.com/ar4mirez/ai-claude-code/discussions)

---

**Happy coding with AI! 🚀**

*Generated with [Claude Code](https://claude.com/claude-code)*
