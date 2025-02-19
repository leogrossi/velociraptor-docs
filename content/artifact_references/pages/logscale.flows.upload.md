---
title: LogScale.Flows.Upload
hidden: true
tags: [Server Event Artifact]
---

This server side event monitoring artifact waits for new artifacts
to be collected from endpoints and automatically posts those to a
LogScale (formerly Humio) ingestion endpoint.


```yaml
name: LogScale.Flows.Upload
description: |
  This server side event monitoring artifact waits for new artifacts
  to be collected from endpoints and automatically posts those to a
  LogScale (formerly Humio) ingestion endpoint.

type: SERVER_EVENT

parameters:
  - name: ingestApiBase
    description: API Base Url for LogScale server
    type: string
    default: https://cloud.community.humio.com/api
  - name: ingestToken
    description: Ingest token for API
    type: string
  - name: tagFields
    description: Comma-separated list of field names to use as tags in the message; Can be renamed with <oldname>=<newname>.
    default:
    type: string
  - name: numThreads
    description: Number of threads to start up to post events
    type: int
    default: 1
  - name: httpTimeout
    description: Timeout (in seconds) for http connection attempts
    type: int
    default: 10
  - name: batchingTimeoutMs
    description: Timeout to batch events prior to sending
    type: int
    default: 30000
  - name: eventBatchSize
    description: Count of events to batch prior to sending
    type: int
    default: 2000
  - name: statsInterval
    description: Interval to post statistics to log (in seconds, 0 to disable)
    type: int
    default: 600
  - name: debug
    description: Enable verbose logging
    type: bool
    default: false
  - name: ArtifactNameRegex
    default: .
    type: regex
    description: Only upload these artifacts to elastic

sources:
  - query: |
      LET completions = SELECT * FROM watch_monitoring(
             artifact="System.Flow.Completion")
             WHERE Flow.artifacts_with_results =~ ArtifactNameRegex

      LET documents = SELECT * FROM foreach(row=completions,
          query={
             SELECT * FROM foreach(
                 row=Flow.artifacts_with_results,
                 query={
                     SELECT *, _value AS Artifact,
                            timestamp(epoch=now()) AS timestamp,
                            ClientId, Flow.session_id AS FlowId
                     FROM source(
                        client_id=ClientId,
                        flow_id=Flow.session_id,
                        artifact=_value)
                 })
          })

      SELECT * FROM logscale_upload(
          query=documents,
          apibaseurl=ingestApiBase,
          ingest_token=ingestToken,
          threads=numThreads,
          tag_fields=split(string=tagFields, sep=","),
          batching_timeout_ms=batchingTimeoutMs,
          event_batch_size=eventBatchSize,
          http_timeout=httpTimeout,
          debug=debug,
          stats_interval=statsInterval)

```
