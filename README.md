## Rundeck_Exporter

Rundeck Metrics Exporter for Prometheus.

This exporter uses the prometheus_client and requests Python module to expose Rundeck metrics found in:

 * RUNDECK_URL/*api_version*/system/info
 * RUNDECK_URL/*api_version*/metrics/metrics

 Where *version* represents the Rundeck API version, like: 31,32,33,34,etc.

 This code was tested on Rundeck API version 31.

## Metrics

All metrics are exported with **rundeck_** prefix.

## Dependencies

* A Rundeck token with permissions to make API requests
* The following python modules:
```
pip install prometheus-client requests cachetools
```

## Usage

Rundeck token must be passed as a environment variable (RUNDECK_TOKEN) to work.

The rundeck_exporter supports the following paramenters:

```
$ ./rundeck_exporter.py -h

Rundeck Metrics Exporter

optional arguments:
  -h, --help            show this help message and exit
  --debug               Enable debug mode.
  --host RUNDECK_EXPORTER_HOST
                        Host binding address. Default: 127.0.0.1.
  --port RUNDECK_EXPORTER_PORT
                        Host binding port. Default: 9620.
  --rundeck.url RUNDECK_URL
                        Rundeck Base URL [ REQUIRED ].
  --rundeck.skip_ssl    Rundeck Skip SSL Cert Validate.
  --rundeck.api.version RUNDECK_API_VERSION
                        Default: 34.
  --rundeck.projects.executions
                        Get projects executions metrics.
  --rundeck.projects.filter RUNDECK_PROJECTS_FILTER [RUNDECK_PROJECTS_FILTER ...]
                        Get executions only from listed projects (delimiter = space).
  --rundeck.projects.executions.cached RUNDECK_PROJECTS_EXECUTIONS_CACHED
                        Cache requests for project executions metrics query.
  --rundeck.cached.requests.ttl RUNDECK_CACHED_REQUESTS_TTL
                        Rundeck cached requests expiration time. Default: 120
```

Optionally, it's possible to pass the following environment variables to the rundeck_exporter:

| Variable | Options |  Description |
| ------ | ------ | ------ |
| RUNDECK_EXPORTER_DEBUG | <ul><li>True</li><li>False (default)</li></ul> | Enable debug mode |
| RUNDECK_EXPORTER_HOST | Default: 127.0.0.1 | Binding address. |
| RUNDECK_EXPORTER_PORT | Default: 9620 | Binding port. |
| RUNDECK_URL (required) | | Rundeck base URL |
| RUNDECK_TOKEN (required) | | Rundeck access token |
| RUNDECK_API_VERSION | Default: 31 | Rundeck API version. |
| RUNDECK_SKIP_SSL | <ul><li>True</li><li>False (default)</li></ul> | Skip SSL certificate check. |
| RUNDECK_PROJECTS_EXECUTIONS | <ul><li>True</li><li>False (default)</li></ul> | Get projects executions metrics. |
| RUNDECK_PROJECTS_FILTER | [] | Get executions only from listed projects. |
| RUNDECK_PROJECTS_EXECUTIONS_CACHE | <ul><li>True</li><li>False (default)</li></ul> | Cache requests for project executions metrics query. |
| RUNDECK_CACHED_REQUESTS_TTL | Default: 120 | Rundeck cached requests expiration time. |

Example output:

```
$ curl -s http://127.0.0.1:9620

...
# HELP rundeck_system_info Rundeck system info
# TYPE rundeck_system_info gauge
rundeck_system_info{apiversion="35",base="/home/rundeck",build="3.2.8-20200608",buildGit="v3.2.8-20200608-0-g7e632f5",node="prod-sgh-rundeck-deploy-6f64c8d9ff-vrd6t",serverUUID="0be6f979-5964-4e7d-9805-bb7cd87e3362",version="3.2.8-20200608"} 1.0
# HELP rundeck_system_stats_uptime_since Rundeck system stats
# TYPE rundeck_system_stats_uptime_since gauge
rundeck_system_stats_uptime_since 1.596636096102e+012
# HELP rundeck_system_stats_scheduler_running Rundeck system stats
# TYPE rundeck_system_stats_scheduler_running gauge
rundeck_system_stats_scheduler_running 4.0
# HELP rundeck_system_stats_scheduler_threadPoolSize Rundeck system stats
# TYPE rundeck_system_stats_scheduler_threadPoolSize gauge
rundeck_system_stats_scheduler_threadPoolSize 200.0
# HELP rundeck_system_stats_threads_active Rundeck system stats
# TYPE rundeck_system_stats_threads_active gauge
rundeck_system_stats_threads_active 265.0
# HELP rundeck_dataSource_connection_pingTime Rundeck gauges metrics
# TYPE rundeck_dataSource_connection_pingTime gauge
rundeck_dataSource_connection_pingTime 0.0
# HELP rundeck_scheduler_quartz_runningExecutions Rundeck gauges metrics
# TYPE rundeck_scheduler_quartz_runningExecutions gauge
rundeck_scheduler_quartz_runningExecutions 4.0
# HELP rundeck_services_AuthorizationService_sourceCache_evictionCount_total Rundeck gauges metrics
# TYPE rundeck_services_AuthorizationService_sourceCache_evictionCount_total counter
rundeck_services_AuthorizationService_sourceCache_evictionCount_total 0.0
# HELP rundeck_services_AuthorizationService_sourceCache_hitCount_total Rundeck gauges metrics
# TYPE rundeck_services_AuthorizationService_sourceCache_hitCount_total counter
rundeck_services_AuthorizationService_sourceCache_hitCount_total 6.704229e+06
# HELP rundeck_services_AuthorizationService_sourceCache_loadExceptionCount_total Rundeck gauges metrics
# TYPE rundeck_services_AuthorizationService_sourceCache_loadExceptionCount_total counter
rundeck_services_AuthorizationService_sourceCache_loadExceptionCount_total 0.0
# HELP rundeck_services_AuthorizationService_sourceCache_missCount_total Rundeck gauges metrics
# TYPE rundeck_services_AuthorizationService_sourceCache_missCount_total counter
rundeck_services_AuthorizationService_sourceCache_missCount_total 75.0
# HELP rundeck_services_NodeService_nodeCache_evictionCount_total Rundeck gauges metrics
# TYPE rundeck_services_NodeService_nodeCache_evictionCount_total counter
rundeck_services_NodeService_nodeCache_evictionCount_total 0.0
# HELP rundeck_services_NodeService_nodeCache_hitCount_total Rundeck gauges metrics
# TYPE rundeck_services_NodeService_nodeCache_hitCount_total counter
rundeck_services_NodeService_nodeCache_hitCount_total 1138.0
# HELP rundeck_services_ProjectManagerService_fileCache_evictionCount_total Rundeck gauges metrics
# TYPE rundeck_services_ProjectManagerService_fileCache_evictionCount_total counter
rundeck_services_ProjectManagerService_fileCache_evictionCount_total 0.0
# HELP rundeck_services_ProjectManagerService_fileCache_hitCount_total Rundeck gauges metrics
# TYPE rundeck_services_ProjectManagerService_fileCache_hitCount_total counter
rundeck_services_ProjectManagerService_fileCache_hitCount_total 8864.0
# HELP rundeck_services_ProjectManagerService_fileCache_loadExceptionCount_total Rundeck gauges metrics
# TYPE rundeck_services_ProjectManagerService_fileCache_loadExceptionCount_total counter
rundeck_services_ProjectManagerService_fileCache_loadExceptionCount_total 0.0
# HELP rundeck_services_ProjectManagerService_fileCache_missCount_total Rundeck gauges metrics
# TYPE rundeck_services_ProjectManagerService_fileCache_missCount_total counter
rundeck_services_ProjectManagerService_fileCache_missCount_total 622.0
# HELP rundeck_services_ProjectManagerService_projectCache_evictionCount_total Rundeck gauges metrics
# TYPE rundeck_services_ProjectManagerService_projectCache_evictionCount_total counter
rundeck_services_ProjectManagerService_projectCache_evictionCount_total 3667.0
# HELP rundeck_services_ProjectManagerService_projectCache_hitCount_total Rundeck gauges metrics
# TYPE rundeck_services_ProjectManagerService_projectCache_hitCount_total counter
rundeck_services_ProjectManagerService_projectCache_hitCount_total 226848.0
# HELP rundeck_scheduler_quartz_scheduledJobs Rundeck counters metrics
# TYPE rundeck_scheduler_quartz_scheduledJobs gauge
rundeck_scheduler_quartz_scheduledJobs 4.0
# HELP rundeck_services_AuthorizationService_systemAuthorization_evaluateMeter_total Rundeck meters metrics
# TYPE rundeck_services_AuthorizationService_systemAuthorization_evaluateMeter_total counter
rundeck_services_AuthorizationService_systemAuthorization_evaluateMeter_total 18134.0
# HELP rundeck_services_AuthorizationService_systemAuthorization_evaluateSetMeter_total Rundeck meters metrics
# TYPE rundeck_services_AuthorizationService_systemAuthorization_evaluateSetMeter_total counter
rundeck_services_AuthorizationService_systemAuthorization_evaluateSetMeter_total 27496.0
# HELP rundeck_services_ExecutionService_executionFailureMeter_total Rundeck meters metrics
# TYPE rundeck_services_ExecutionService_executionFailureMeter_total counter
rundeck_services_ExecutionService_executionFailureMeter_total 94.0
# HELP rundeck_services_ExecutionService_executionJobStartMeter_total Rundeck meters metrics
# TYPE rundeck_services_ExecutionService_executionJobStartMeter_total counter
rundeck_services_ExecutionService_executionJobStartMeter_total 366.0
# HELP rundeck_services_ExecutionService_executionStartMeter_total Rundeck meters metrics
# TYPE rundeck_services_ExecutionService_executionStartMeter_total counter
rundeck_services_ExecutionService_executionStartMeter_total 366.0
# HELP rundeck_services_ExecutionService_executionSuccessMeter_total Rundeck meters metrics
# TYPE rundeck_services_ExecutionService_executionSuccessMeter_total counter
rundeck_services_ExecutionService_executionSuccessMeter_total 268.0
# HELP rundeck_api_requests_requestTimer_total Rundeck timers metrics
# TYPE rundeck_api_requests_requestTimer_total counter
rundeck_api_requests_requestTimer_total 39419.0
# HELP rundeck_project_execution_info Rundeck Project aic-helloworld-ansible-playbook Executions
# TYPE rundeck_project_execution_info gauge
rundeck_project_execution_info{date_ended="1596219761000",date_started="1596219760000",id="1623097",job_average_duration="20260",job_id="helloworld-ansible-playbook-job-test",job_name="Job Test",status="failed"} 1.0
# HELP rundeck_project_execution_info Rundeck Project bdh-oracle_install_client Executions
# TYPE rundeck_project_execution_info gauge
rundeck_project_execution_info{date_ended="1594847962000",date_started="1594847743000",id="1082818",job_average_duration="317410",job_id="dfd6d2aa-5159-46db-a0c5-0b9a8aa04527",job_name="Client Oracle Install",status="succeeded"} 1.0
# HELP rundeck_project_execution_info Rundeck Project tbs-servcom_install Executions
# TYPE rundeck_project_execution_info gauge
rundeck_project_execution_info{date_ended="1596808008000",date_started="1596807999000",id="1631438",job_average_duration="10956",job_id="servcom_install",job_name="Servcom Client Install",status="succeeded"} 1.0
....
```

#### Running in Docker

```
docker build -t rundeck_exporter .

docker run --rm -d -p 9620:9620 -e RUNDECK_TOKEN=$RUNDECK_TOKEN rundeck_exporter \
--host 0.0.0.0 \
--rundeck.url https://rundeck.test.com \
--rundeck.skip_ssl
```

## Changelog

`v1.0.0`:
* Initial release

`v1.1.0`:
* Support for environment variables
* Better excpetions treatment

`v1.1.1`:
* Fix metrics collection bug

`v1.2.0`:
* Add new params:
  * --debug: Enable debug mode
  * --rundeck.projects.executions: Get projects executions metrics
  * --rundeck.projects.filter: Get executions only from listed projects (delimiter = space)
  * --rundeck.projects.executions.limit: Limit project executions metrics query. Default: 20
  * --rundeck.cached.requests.ttl: Rundeck cached requests (by now, only for rundeck.projects.executions) expiration time. Default: 120
* Add code improvements
* Add cachetools to pip install on Dockerfile
* Add logging module to replace print calls
* Add better error handling
* Change args location, now located at class RundeckMetricsCollector

`v2.0.0`:
* Fix json response validation
* Add param --rundeck.projects.executions.cache and env RUNDECK_PROJECTS_EXECUTIONS_CACHE
* Add counter metrics rundeck_services_[services,controllers,api,web]_total
* Remove all gauge metrics rundeck_[services,controllers,api,web]...{type="..."}
* Remove metrics rundeck_system_stats_[cpu,memory,uptime_duration]...
* Remove --rundeck.token param. Need RUNDECK_TOKEN env now.
* Remove --rundeck.projects.executions.limit
* Remove rundeck_node label from all metrics
