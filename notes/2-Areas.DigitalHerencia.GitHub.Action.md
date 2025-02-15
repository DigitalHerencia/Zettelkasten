---
id: 5hqwde6iuaw093dgb94diyl
title: Action
desc: ''
updated: 1739339292969
created: 1739338020613
---

```yaml
openapi: 3.1.0
info:
  title: GitHub Custom Action API
  description: Perform GitHub repository actions via API requests.
  version: 1.0.0

servers:
  - url: https://api.github.com
    description: GitHub API

paths:
  # Pull Requests
  /repos/{owner}/{repo}/pulls/{pull_number}:
    get:
      operationId: getPullRequestDetails
      summary: Retrieve details of a specific pull request.
      parameters:
        - name: owner
          in: path
          required: true
          schema:
            type: string
          description: Owner of the repository.
        - name: repo
          in: path
          required: true
          schema:
            type: string
          description: Repository name.
        - name: pull_number
          in: path
          required: true
          schema:
            type: integer
          description: Pull request number.
      responses:
        "200":
          description: Pull request details retrieved successfully.
          content:
            application/json:
              schema:
                type: object
                properties:
                  title:
                    type: string
                  state:
                    type: string
                  commits:
                    type: integer
                  changed_files:
                    type: integer
        "404":
          description: Pull request not found.

  /repos/{owner}/{repo}/pulls/{pull_number}/diff:
    get:
      operationId: getPullRequestDiff
      summary: Retrieve the diff of a pull request.
      parameters:
        - name: owner
          in: path
          required: true
          schema:
            type: string
        - name: repo
          in: path
          required: true
          schema:
            type: string
        - name: pull_number
          in: path
          required: true
          schema:
            type: integer
      responses:
        "200":
          description: Successfully retrieved the pull request diff.
          content:
            text/plain:
              schema:
                type: string
        "404":
          description: Pull request not found.

  /repos/{owner}/{repo}/pulls/{pull_number}:
    patch:
      operationId: closePullRequest
      summary: Close a pull request.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                state:
                  type: string
                  enum: [closed]
      responses:
        "200":
          description: Pull request closed successfully.
        "404":
          description: Pull request not found.

  /repos/{owner}/{repo}/issues/{issue_number}/comments:
    post:
      operationId: commentOnIssue
      summary: Post a comment on an issue.
      parameters:
        - name: owner
          in: path
          required: true
          schema:
            type: string
        - name: repo
          in: path
          required: true
          schema:
            type: string
        - name: issue_number
          in: path
          required: true
          schema:
            type: integer
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                body:
                  type: string
      responses:
        "201":
          description: Comment posted successfully.
        "404":
          description: Issue not found.

  /repos/{owner}/{repo}:
    get:
      operationId: getRepositoryInfo
      summary: Retrieve repository details.
      responses:
        "200":
          description: Repository information retrieved successfully.
        "404":
          description: Repository not found.

  /repos/{owner}/{repo}/commits:
    get:
      operationId: listCommits
      summary: List all commits in a repository.
      responses:
        "200":
          description: Commits retrieved successfully.

  /repos/{owner}/{repo}/commits/{commit_sha}:
    get:
      operationId: getCommitDetails
      summary: Retrieve details of a specific commit.
      responses:
        "200":
          description: Commit details retrieved successfully.

  /repos/{owner}/{repo}/git/refs:
    post:
      operationId: createBranch
      summary: Create a new branch reference.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                ref:
                  type: string
                sha:
                  type: string
      responses:
        "201":
          description: Branch created successfully.

  /repos/{owner}/{repo}/releases:
    post:
      operationId: createRelease
      summary: Create a new release.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                tag_name:
                  type: string
                name:
                  type: string
                body:
                  type: string
      responses:
        "201":
          description: Release created successfully.

  /repos/{owner}/{repo}/hooks:
    get:
      operationId: listWebhooks
      summary: List webhooks for the repository.
      responses:
        "200":
          description: Webhooks retrieved successfully.

  /users/{username}/repos:
    get:
      operationId: listUserRepositories
      summary: List repositories owned by the user.
      responses:
        "200":
          description: User repositories retrieved successfully.

```