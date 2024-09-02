
GitHub is an indispensable tool for developers worldwide, providing a robust platform for code management, collaboration, and version control. With Kanban style project management functionality aptly called "Projects",  Github has brought project management in close proximity to the codebase, thereby reducing context switching and enhancing traceability. This colocation of source and task management facilitates a more seamless development experience, as engineers can reference commits, pull requests, and issues directly within the project's workflow. 

### Github Project

As per Github: "A project is an adaptable spreadsheet, task-board, and road map that integrates with your issues and pull requests on GitHub to help you plan and track your work effectively. You can create and customize multiple views by filtering, sorting, grouping your issues and pull requests, visualize work with configurable charts, and add custom fields to track metadata specific to your team. "


#### Github Organization

######FOCUS on complicated actions - 

#### Access Control




GitHub Projects inherently simplifies tracking by situating project management in close proximity to the codebase, thereby reducing context switching and enhancing traceability. This colocation of source and task management facilitates a more seamless development experience, as engineers can reference commits, pull requests, and issues directly within the project's workflow. Unlike external tools such as Rally or Jira, GitHub Projects appeals to software professionals for its native integration within the GitHub ecosystem—a platform where many developers already spend a significant portion of their day. This integration streamlines the development process by allowing direct linking between code changes and project tasks, fostering better communication and more efficient collaboration. Moreover, the use of GitHub Actions further automates status updates and issue tracking, keeping the project board effortlessly synchronized with the repository's activity. This tight coupling is particularly advantageous in a DevOps culture, where continuous integration and delivery are pivotal, making GitHub Projects a preferred choice for teams seeking to minimize overhead and maximize productivity.


Group projects by labels

By default anyone who has access to the repository can create an issue. 
**Read**
"Can read and clone this repository. Can also open and comment on issues and pull requests."
we can create a issue template

```
name: OIDS Internal Team Projects
description: This form is used to capture internal team project work within OIDS. 
title: "[OIDS Internal Team Project Work]: "
labels: ["Internal Project"]
projects: ["OptumInsight-Platform/7"]
assignees:
  - jellis29_uhg
body:
  - type: markdown
    attributes:
      value: |
        ## OIDS Internal Team Project Work
        Please fill out the details below to help us understand the project you are working on within the OIDS team.
  - type: textarea
    id: project-overview
    attributes:
      label: Project Overview
      description: What project are you working on to support the team?
      placeholder: Briefly describe the project...
    validations:
      required: true
  - type: textarea
    id: project-impact
    attributes:
      label: Project Impact
      description: Please explain the impact of this problem. Why does this project matter? What is the value of doing this project?
      placeholder: Explain the impact of doing this project...
    validations:
      required: true
  - type: markdown
    attributes:
      value: |
        ## Task Work
        This section is OPTIONAL. You can use the below section in case it would be helpful for you; however, what is required is for you to please create individual task issue forms for the tasks involved with the project.
  - type: textarea
    id: task-work
    attributes:
      label: Task Work
      description: If you would like, fill out this optional section with the tasks required to complete this project.
      placeholder: Tasks
    validations:
      required: false
```      


Say you want to have fine grained control on project intake, you can create custom github actions. Things to keep in mind:
1. Triggers : Label, assignee



secrets.GITHUB_TOKEN only works for some actions like checking orgs, adding projects
Classic token make sure that you give access to projects and also the organizations
Fine grained token - use resource owner as the organization. The organization admins can approve the request.


Github actions

Lessons Learned:
1. There is no way to change and replay
2. The error may be on another line - indentation matters!!
3. Hard to debug error "Unhandled error: SyntaxError: Unexpected string" as line numbers are not printed.
4. Rerun jobs - check the checkbox to enable debug-logging


ou have an error in your yaml syntax on line 80


https://hubstaff.com/blog/github-project-management/

#https://docs.github.com/en/actions/learn-github-actions/expressions

#https://github.com/actions/github-script
#https://github.com/actions/add-to-project
#https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels

https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions

https://docs.github.com/en/rest/teams/members?apiVersion=2022-11-28#get-team-membership-for-a-user
https://octokit.github.io/rest.js/v18#users

https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions


https://github.com/actions/github-script

For error:
- Could not resolve to a ProjectV2 with the number 14.
https://stackoverflow.com/questions/77198990/request-failed-due-to-following-response-errors-could-not-resolve-to-a-projec


running jobs sequentially
https://github.com/orgs/community/discussions/42734

Permissions
https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions
https://docs.github.com/en/rest/actions/permissions?apiVersion=2022-11-28

curl -H "Authorization: token  <TOKEN>" \  
https://api.github.com/user/repos/<username>/<repo>  


curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/user


  curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
https://api.github.com/orgs/OptumInsight-Provider/teams/TCP_GHEC_WRITE/memberships/rsing198_uhg

  https://api.github.com/orgs/ORG/teams/TEAM_SLUG/memberships/USERNAME


#https://stackoverflow.com/questions/72387730/github-action-how-to-check-if-pr-creator-is-part-of-a-specific-team       



https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/making-authenticated-api-requests-with-a-github-app-in-a-github-actions-workflow