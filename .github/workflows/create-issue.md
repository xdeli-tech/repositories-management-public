name: Create Issue

on:
  workflow_dispatch:
    inputs:
      repository:
        description: 'Repository Name'
        required: true
      title:
        description: 'Issue Title'
        required: true
      body:
        description: 'Issue Body'
        required: true
      assignee:
        description: 'Issue Assignee'
        required: false

jobs:
  create-issue:
    runs-on: ubuntu-latest
    steps:
      - name: Create Issue
        uses: octokit/request-action@v2.x
        with:
          route: POST /repos/:org/:repo/issues
          org: xdeli-tech
          repo: ${{ github.event.inputs.repository }}
          title: ${{ github.event.inputs.title }}
          body: ${{ github.event.inputs.body }}
          assignees: ${{ github.event.inputs.assignee }}
          mediaType: |
            previews:
              - symmetra
        env:
          GITHUB_TOKEN: ${{ secrets.XDELI_BOT_TOKEN }}
