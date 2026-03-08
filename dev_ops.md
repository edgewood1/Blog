# A Comprehensive Guide to DevOps Concepts

This document provides a consolidated overview of DevOps topics, covering Agile methodologies like Scrum, tools such as Jira and Jenkins, and CI/CD automation with GitHub Actions.

## 1. Agile Project Management & Methodologies

### 1.1. Scrum

Scrum is an Agile framework that helps teams work together to develop, deliver, and sustain complex products. It's designed for teams to learn from experience, self-organize while working on a problem, and reflect on their wins and losses to continuously improve.

### 1.2. Jira for Scrum

Jira is a popular tool for issue tracking and agile project management.

**Issue Hierarchy:**
-   **Epic**: A large body of work that can be broken down into a number of smaller stories. An Epic often spans multiple sprints.
-   **Story**: A user story is a requirement or feature expressed from the end-user's perspective. The value of a story is realized when its parent Epic is complete. A standard format is: "As a [user type], I want to [action] so that [benefit]."
-   **Sub-task**: A smaller piece of work required to complete a story.

**Jira Workflow Note**:
In some workflows, an issue (Defect, New Feature, or Improvement) must be linked to a test case (e.g., via an "is tested by" link) before it can be resolved. If this link is missing, you may need to move the issue back to a "Ready" status to trigger the automated creation of a test link.

### 1.3. User Stories and Acceptance Criteria (AC)

A user story describes the "who", "what", and "why" of a requirement. Acceptance Criteria (AC) are the conditions that a software product must meet to be accepted by a user, a customer, or other stakeholders. They are a set of statements, each with a clear pass/fail result.

**Tips for Writing Good AC:**
-   Each criterion should be testable.
-   Criteria should be clear and concise, not ambiguous.
-   Focus on "what," not "how." Describe the observable outcome from the user's perspective, not the implementation details.

### 1.4. Behavior-Driven Development (BDD)

BDD extends Test-Driven Development (TDD) by writing test cases in a natural, human-readable language. It focuses on the system's behavior from the user's point of view. This encourages collaboration between developers, QA, and non-technical participants.

**Gherkin: The Language of BDD**

Gherkin is a business-readable, domain-specific language for defining behaviors without detailing how that behavior is implemented. It's saved in `.feature` files and uses a specific structure with keywords.

-   **`Feature`**: A high-level description of the software feature.
-   **`Scenario`**: A concrete example of how the system should behave in a particular situation.
-   **`Given`**: Describes the initial context or pre-condition.
-   **`When`**: Describes an event or action performed by a user.
-   **`Then`**: Describes the expected outcome or result.
-   **`And`**, **`But`**: Can be used to chain multiple `Given`, `When`, or `Then` steps.
-   **`Background`**: Adds context to all scenarios in a feature. It runs before each scenario.
-   **`Scenario Outline`**: A template for running the same scenario with different data.

**Example Gherkin Scenario:**
```gherkin
Feature: User Authentication

  Scenario: Successful login with valid credentials
    Given the user is on the login page
    When the user enters a valid username and password
    And the user clicks the "Login" button
    Then the user should be redirected to their dashboard
```

-   **Cucumber** is a popular testing framework that understands Gherkin and can execute these scenarios as automated tests.

## 2. CI/CD and Automation Tools

### 2.1. Introduction to Build Automation

Build automation is the process of scripting and automating the activities involved in creating a build artifact (the deployable software), including compiling source code, running tests, and packaging the application.

**Build Automation Servers** (or CI/CD servers) are tools that execute these automated builds on a scheduled or triggered basis.
- **Continuous Integration (CI)**: The practice of frequently merging all developers' code changes into a shared mainline. Each merge triggers an automated build and test run.
- **Continuous Delivery/Deployment (CD)**: The practice of automatically deploying every passed build to a testing or production environment.

Common tools include Jenkins, Travis CI, CircleCI, Bamboo, and GitHub Actions.

### 2.2. Jenkins

Jenkins is an open-source automation server that helps automate the parts of software development related to building, testing, and deploying.

**Practical Example: Using "Build with Parameters"**
Jenkins jobs can be parameterized to allow users to provide inputs at runtime. This is common for deploying specific branches to specific servers.
1.  Navigate to the Jenkins job (e.g., "Feature Build Deploy").
2.  Select "Build with Parameters."
3.  Fill in the required parameters:
    -   `branch`: The name of the feature branch to deploy (e.g., `CSA-5305-study-notes`).
    -   `build`: The component to build (`Web`, `RestApi`, or `All`).
    -   `server`: The target server to deploy to (e.g., `cs-feature`).
4.  Another common use is reverting a server to a clean snapshot before deployment using a "master deploy" job with a `revert` option.

### 2.3. GitHub Actions

GitHub Actions is a CI/CD platform that allows you to automate your build, test, and deployment pipeline directly from GitHub.

**Core Concepts:**
-   **Workflow**: An automated process defined in a YAML file located in the `.github/workflows` directory.
-   **Trigger (Event)**: An event that starts a workflow, such as a `push`, a `pull_request`, a `schedule`, or a manual dispatch.
-   **Job**: A set of steps that execute on the same runner.
-   **Runner**: A server that runs your workflows. GitHub provides hosted runners (Linux, Windows, macOS), or you can host your own.
-   **Step**: An individual task that can run commands or an action.
-   **Action**: A reusable unit of code that performs a specific task. Actions can be from the marketplace (e.g., `actions/checkout@v2`), a public repo, or your own custom action.

**Workflow Syntax Keywords:**
-   **`name`**: The name of your workflow.
-   **`on`**: Specifies the trigger event(s).
-   **`jobs`**: Defines one or more jobs to run.
-   **`runs-on`**: The type of machine to run the job on (e.g., `ubuntu-latest`).
-   **`uses`**: Tells a step to use a specific action.
-   **`run`**: Tells a step to execute a command-line program.
-   **`needs`**: Specifies that a job is dependent on another job and must wait for it to complete.

## 3. General Best Practices

### 3.1. Writing a Good `README.md`

A `README` file is the front door to your project. It should contain:
-   **Project Title**: A clear and concise name.
-   **Description**: A short explanation of what the project is, the motivation behind it, and what it does.
-   **Table of Contents**: For longer READMEs.
-   **Installation**: Step-by-step instructions on how to get the development environment running.
-   **Usage**: How to use the project. Code examples are very helpful.
-   **API Documentation**: A reference for the project's API, or a link to it.
-   **Screenshots/Demos**: Visual aids to show the project in action.
-   **Testing**: Instructions on how to run the project's tests.
-   **Contributing**: Guidelines for how others can contribute to the project.
-   **Credits**: Acknowledge collaborators, inspirations, and key libraries.
-   **License**: Information about the project's license (e.g., MIT, Apache 2.0).
-   **Badges**: Status badges for build, code coverage, version, etc., can provide a quick, scannable overview of the project's health.