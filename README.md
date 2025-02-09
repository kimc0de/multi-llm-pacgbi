# Multi-LLM PACGBI

An extended version of the Pipeline for Automated Code Generation from Backlog Items (PACGBI). Uses multiple Large Language Models (LLMs) to automatically implement backlog items through a GitLab CI pipeline.

## Features

- Automated implementation & evaluation of GitLab issues
- Seamless integration with GitLab CI/CD
- Flexibility to use any OpenAI, Claude, and DeepSeek models.

## Setup

1. Copy this  `.gitlab-ci.yml` file to the GitLab project where you want to use the PACGBI.
2. In the GitLab project, create a GitLab Access Token as described in this [GitLab article](https://docs.gitlab.com/ee/user/project/settings/project_access_tokens.html#create-a-project-access-token). Save the token key and value for the next step.
3. Retrieve API keys from OpenAI, Claude Sonnet, and Deepseek. Make sure you have sufficient credits to use all of the LLMs.
4. Next, go to **Setting > CI/CD > Variables** and declare the following variables:

| Key | Value | Visibility (optional) | Protected |
| --- | --- | --- | --- |
| GITLAB_ACCESS_TOKEN | Your GitLab access token from Step 2 | No | No |
| OPENAI_API_KEY | Your OpenAI API Key | No | No |
| OPENAI_MODEL | Name of the OpenAI model you want to use | No | No |
| CLAUDE_SONNET_API_KEY | Your Claude API Key | No | No |
| CLAUDE_SONNET_MODEL | Name of the Claude model you want to use | No | No |
| DEEPSEEK_CODER_API_KEY | Your Deepseek API Key | No | No |
| DEEPSEEK_CODER_MODEL | Name of the Deepseek model you want to use | No | No |
| SYSTEM_MESSAGE | Your individual system message| Yes | No |

## Usage
1. Open the GitLab Issue that you want to be implemented by the multi-LLM PACGBI.
2. Set an Issue label with the name of the code file which needs to be modified by the PACGBI to solve the Issue with the file extension.
> **_NOTE:_** Currently, the multi-LLM PACGBI only supports modifying a single file, meaning one label per issue.
3. Make sure the Issue description is clear and detailed. In our paper, we used this template:

```
Story Context: << Your text here >>
Acceptance Criteria: << Your text here >>
Technical Solution: << Your text here >>
```

4. Create a new branch with the desired **LLM prefix** and **issue number** after the "/" to trigger the PACGBI. For example:
```
openai/12-implement-something
claude/12-implement-something
deepseek/12-implement-something
```
5. If the pipeline runs through all stages successfully, you can find the merge request with the LLM-generated code in **Code > Merge requests**.

> **_CAUTION:_** The generated merge request must be reviewed by developers before merging into the main codebase to prevent unexpected or unintended changes.
