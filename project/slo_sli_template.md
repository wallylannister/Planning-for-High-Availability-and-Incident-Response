# API Service

| Category     | SLI | SLO                                                                                                         |
|--------------|-----|-------------------------------------------------------------------------------------------------------------|
| Availability | The percentage of successful requests over the last 5m | 99%                                                                                                         |
| Latency      | 90% of requests finish within 100ms | 90% of requests below 100ms                                                                                 |
| Error Budget | Percentage of failed requests is below 20% over the last 7d | Error budget is defined at 20%. This means that 20% of the requests can fail and still be within the budget |
| Throughput   | More than 5 successful requests per second | 5 RPS indicates the application is functioning                                                              |
