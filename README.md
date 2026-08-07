# Databricks DAB learning repo

This repository is a hands-on example for understanding Databricks Asset Bundles (DABs). It combines a local Python project, bundle configuration, and example bronze/silver/gold pipelines that can be deployed to Databricks as jobs and pipelines.

## What you will learn

- How to set up a local DAB project with Databricks CLI and Python tooling
- How bundle targets such as `dev` and `prod` separate environments
- How to define bronze, silver, and gold pipeline resources in YAML
- How a workflow job can orchestrate the layers and run on a schedule

## Repository structure

- [databricks.yml](databricks.yml): bundle entry point and target configuration
- [resources/](resources/): YAML resource definitions for pipelines and jobs
- [src/](src/): Python and DLT example code that the bundles deploy
- [tests/](tests/): example unit tests for the shared Python package

## Local setup

1. Install the Databricks CLI and authenticate:
   - `databricks configure`
2. Install Python dependencies:
   - `uv sync --dev`
3. Deploy the bundle to your development environment:
   - `databricks bundle deploy --target dev`
4. Run the example workflow or pipeline:
   - `databricks bundle run`

## Bundle concepts demonstrated here

- Environment setup:
  - The bundle uses targets in [databricks.yml](databricks.yml) to separate `dev` and `prod` behavior.
- Bronze layer:
  - [resources/bronze_pipeline.pipeline.yml](resources/bronze_pipeline.pipeline.yml) shows a raw-ingestion pipeline.
- Silver layer:
  - [resources/silver_pipeline.pipeline.yml](resources/silver_pipeline.pipeline.yml) shows data cleaning and standardization.
- Gold layer:
  - [resources/gold_pipeline.pipeline.yml](resources/gold_pipeline.pipeline.yml) shows reporting-ready aggregates.
- Workflow scheduling:
  - [resources/dab_learning_workflow.job.yml](resources/dab_learning_workflow.job.yml) runs the bronze, silver, and gold pipelines in sequence on a daily schedule.

## Recommended learning flow

1. Start with [databricks.yml](databricks.yml) and understand the bundle targets.
2. Review the pipeline YAML files to see how each layer is defined.
3. Deploy the bundle and inspect the created jobs and pipelines in your Databricks workspace.
4. Adjust the schemas, naming, and schedules to fit your own data platform patterns.

## Local tests

Run the example tests with:

- `uv run pytest`
