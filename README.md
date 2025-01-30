# Tech Quiz with GitHub Actions and Cypress Testing

## Description
A comprehensive tech quiz application featuring automated testing with Cypress, GitHub Actions for CI/CD, and deployment to Render. This project demonstrates best practices in modern web development workflows, including branching strategies, automated testing, and continuous deployment.

[Live Application](your-render-url) | [GitHub Repository](your-repo-url)

## Table of Contents
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Testing](#testing)
- [CI/CD Pipeline](#ci-cd-pipeline)
- [Branch Strategy](#branch-strategy)
- [Deployment](#deployment)
- [Screenshots](#screenshots)

## Project Structure
```
tech-quiz/
├── .github/
│   └── workflows/
│       ├── develop-pr.yml      # PR workflow for develop branch
│       └── main-deploy.yml     # Deployment workflow for main branch
├── client/
│   └── src/
├── cypress/
│   ├── component/
│   ├── e2e/
│   └── fixtures/
├── server/
└── package.json
```

## Branch Strategy
The repository maintains three types of branches:
- `main`: Production branch
- `develop`: Integration branch
- `feature/*`: Feature development branches

### Workflow:
1. Create feature branch from `develop`
2. Develop and test feature
3. Submit PR to `develop`
4. Automated tests run via GitHub Actions
5. Merge to `develop` after approval
6. Submit PR from `develop` to `main`
7. Automated deployment to Render on `main` merge

## GitHub Actions

### PR to Develop Branch
```yaml
name: Cypress Tests
on:
  pull_request:
    branches: [ develop ]

jobs:
  cypress-run:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Cypress Run
        uses: cypress-io/github-action@v6
        with:
          command: npm run test
```

### Deploy to Main Branch
```yaml
name: Deploy to Render
on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to Render
        uses: renderinc/deploy-action@v1
        with:
          service-id: ${{ secrets.RENDER_SERVICE_ID }}
```

## Installation

1. Clone the repository:
```bash
git clone [your-repo-url]
cd tech-quiz
```

2. Install dependencies:
```bash
npm install
```

3. Create feature branch:
```bash
git checkout -b feature/your-feature develop
```

## Testing

Run Cypress tests:
```bash
# Component tests
npm run test:component

# E2E tests
npm run test:e2e

# All tests
npm run test
```

## Deployment
The application automatically deploys to Render when changes are merged to the `main` branch.

Manual deployment steps:
1. Ensure all tests pass locally
2. Create PR to `develop`
3. Wait for GitHub Actions tests to pass
4. Merge to `develop`
5. Create PR to `main`
6. Merge to trigger deployment

## Features
- Interactive tech quiz interface
- Automated testing pipeline
- Continuous deployment
- Branch protection rules
- Comprehensive test coverage

## Screenshots
[Add screenshots here]
- Application interface
- GitHub Actions workflow
- Cypress test results
- Render deployment

## Development Guidelines
- Create feature branches from `develop`
- Include comprehensive tests
- Follow naming conventions:
  - Branches: `feature/feature-name`
  - Components: PascalCase
  - Files: kebab-case
- Write descriptive commit messages
- Update tests with new features

## Quality Assurance
- All Cypress tests must pass
- Code follows ESLint rules
- Responsive design
- Cross-browser compatibility
- Accessibility standards met

## Contributing
1. Fork the repository
2. Create feature branch from `develop`
3. Implement feature with tests
4. Submit PR to `develop`
5. Ensure all checks pass

## License
[Choose and add appropriate license]

## Contact
- Developer: [Your Name]
- GitHub: [Your Profile]
- Email: [Your Email]
