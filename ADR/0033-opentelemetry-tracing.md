# 33. OpenTelemetry Tracing

Date started: 2024-02-27
Date accepted: 2024-MM-DD

## Status

Accepted

## Approvers

-   ?

## Reviewers

-   ?

## Context

Instrumenting the application build pipelines with OpenTelemetry tracing will provide us invaluable insight in case things go wrong. We are going to get traces for the tekton controller activity and generating spans for tekton tasks to achieve an easier mental model to use for debugging.

## Decision

Tekton already natively supports [OpenTelemetry Distributed Tracing for Tasks and Pipelines](https://github.com/tektoncd/community/blob/main/teps/0124-distributed-tracing-for-tasks-and-pipelines.md), so no upstream changes are required.

## Consequences

A few environment variables will need to be set in the controller manifest of each AppStudio instance in order to enable tracing:

```
OTEL_EXPORTER_JAEGER_ENDPOINT
OTEL_EXPORTER_JAEGER_USER
OTEL_EXPORTER_JAEGER_PASSWORD
```

At this time, instrumenting individual steps within each task is not natively supported by Tekton, so this is an option that can be explored as a potential upstream contribution.

## Implementation

The AppStudio Tekton pipeline definition and tasks will require changes.