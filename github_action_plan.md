# GitHub Action Plan: Self-Hosted Profile Stats

The stats and streak cards in the profile README are served by free third-party services (github-readme-stats and streak-stats). When those services are down, the cards break. This document describes the plan for replacing them with a self-hosted GitHub Action.

## Goal

Generate the stats images inside this repository on a schedule, so the profile never depends on an external service being up.

## Plan

First, add a workflow under .github/workflows/ that runs once a day and on manual dispatch. Second, use the built-in GITHUB_TOKEN so no extra secrets are needed for public data. Third, generate the stats card as an SVG and commit it to a dedicated output branch. Fourth, point the README image links at the raw SVG on that branch. Finally, keep the hosted cards as a fallback until the workflow has run successfully for a week.

## Checks

The workflow should finish without errors on the scheduled run, the generated SVG should render correctly in both light and dark themes, and the README image links should resolve without depending on a third-party host.
