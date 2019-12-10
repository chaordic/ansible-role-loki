# Loki: like Prometheus, but for logs.

Loki is a horizontally-scalable, highly-available, multi-tenant log aggregation system inspired by [Prometheus](https://prometheus.io/).
It is designed to be very cost effective and easy to operate.
It does not index the contents of the logs, but rather a set of labels for each log stream.

Compared to other log aggregation systems, Loki:

- does not do full text indexing on logs. By storing compressed, unstructured logs and only indexing metadata, Loki is simpler to operate and cheaper to run.
- indexes and groups log streams using the same labels you’re already using with Prometheus, enabling you to seamlessly switch between metrics and logs using the same labels that you’re already using with Prometheus.
- is an especially good fit for storing [Kubernetes](https://kubernetes.io/) Pod logs. Metadata such as Pod labels is automatically scraped and indexed.
- has native support in Grafana (needs Grafana v6.0).

A Loki-based logging stack consists of 3 components:

- `promtail` is the agent, responsible for gathering logs and sending them to Loki.
- `loki` is the main server, responsible for storing logs and processing queries.
- [Grafana](https://github.com/grafana/grafana) for querying and displaying the logs.

Loki is like Prometheus, but for logs: we prefer a multidimensional label-based approach to indexing, and want a single-binary, easy to operate system with no dependencies.
Loki differs from Prometheus by focussing on logs instead of metrics, and delivering logs via push, instead of pull.

## Configuring

The following variables are available to use, detailed description available [here](https://github.com/grafana/loki/tree/master/docs/configuration):

| Variable   	                            | Description                                       | Default Value |
|-------------------------------------------|---------------------------------------------------|---------------|
| loki\_version                             | What Loki version to use                          | v1.2.0        |
| loki\_path                                | Where to store Loki files                         | /opt/loki     |
| loki\_user                                | Run Loki with this user                           | loki          |
| loki\_group                               | Run Loki with this group                          | loki          |
| loki\_target                              | Which components to run                           | all           |
| loki\_listen\_port                        | Which port to run                                 | 9090          |
| loki\_enforce\_metric\_name               | Should every log have a metric?                   | false         |
| loki\_from\_date                          | When did this database schema version started     | 2019-12-01    |
| loki\_schema\_version                     | Which database schema version to use              | v10           |
| loki\_index\_prefix                       | Table name prefix                                 | loki\_        |
| loki\_index\_period                       | Index size                                        | 180h          |
| loki\_s3\_region                          | S3 Bucket region                                  | us-east-1     |
| loki\_s3\_bucket                          | S3 Bucket name                                    | loki          |
| loki\_dynamodb\_region                    | Dynamodb region                                   | us-east-1     |
| loki\_ingester\_chunk\_idle\_period       | Flush the chunk after time idle                   | 15m           |
| loki\_table\_manager\_retention\_deletes  | Should Loki delete the logs?                      | true          |
| loki\_table\_manager\_retention\_period   | Retention period of the logs                      | 720h          |
