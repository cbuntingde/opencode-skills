# Intent-to-Code Pipeline

Multi-step feature generation for transforming user intent into production code.

## Overview

The Intent-to-Code Pipeline skill provides a systematic approach to developing features from initial concept through working implementation. It guides users through a structured five-phase pipeline: Intent Analysis, Architecture Design, Implementation Planning, Code Generation, and Verification.

This skill is designed for scenarios where feature requests are vague, incomplete, or require significant architectural decisions. Rather than diving directly into code, it enforces a disciplined workflow that surfaces requirements ambiguities early, ensures architectural soundness, and produces maintainable, well-tested code.

Use this skill when starting complex feature work, when requirements need clarification, or when you want structured guidance from concept to deployment-ready implementation.

## Usage

1. Invoke the skill at the start of feature development
2. Answer clarifying questions about requirements and constraints
3. Review and approve the proposed architecture and implementation plan
4. Collaborate on iterative code generation
5. Verify tests and checks pass

```bash
skill intent-to-code
```

## Examples

**Basic feature request:**
```
User: "Add user authentication"
-> Intent-to-Code asks: What auth method? OAuth, password, SSO? User roles? Token format? Session duration?
-> Proposes architecture: Auth provider integration, middleware design, user model updates
-> Generates: Auth service, login/logout endpoints, token validation, middleware
-> Verifies: Unit tests, integration tests, security linting
```

**Complex feature request:**
```
User: "Build a real-time notification system"
-> Intent-to-Code asks: WebSocket or polling? Notifications stored or ephemeral? Delivery guarantees? Push providers?
-> Proposes: Event-driven architecture, WebSocket server, notification store, delivery workers
-> Generates: Event schemas, WebSocket handlers, notification CRUD, delivery retry logic
-> Verifies: Load tests, fallback path tests, type checking
```

## Configuration

No configuration required. The skill adapts to your project's existing conventions and stack.

## Requirements

- OpenCode agent environment
- Access to the codebase for implementation
- Test framework available in the project (optional, for verification phase)
- Linting/type checking tools (optional, for verification phase)