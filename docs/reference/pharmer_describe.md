---
title: Pharmer Describe
menu:
  docs_{{ .version }}:
    identifier: pharmer-describe
    name: Pharmer Describe
    parent: reference
menu_name: docs_{{ .version }}
section_menu_id: reference
---
## pharmer describe



### Synopsis



```
pharmer describe [flags]
```

### Options

```
  -h, --help   help for describe
```

### Options inherited from parent commands

```
      --alsologtostderr                  log to standard error as well as files
      --analytics                        Send analytical events to Google Guard (default true)
      --config-file string               Path to Pharmer config file
      --env string                       Environment used to enable debugging (default "prod")
      --kubeconfig string                Paths to a kubeconfig. Only required if out-of-cluster.
      --log_backtrace_at traceLocation   when logging hits line file:N, emit a stack trace (default :0)
      --log_dir string                   If non-empty, write log files in this directory
      --logtostderr                      log to standard error instead of files (default true)
      --master --kubeconfig              (Deprecated: switch to --kubeconfig) The address of the Kubernetes API server. Overrides any value in kubeconfig. Only required if out-of-cluster.
      --stderrthreshold severity         logs at or above this threshold go to stderr (default 2)
  -v, --v Level                          log level for V logs
      --vmodule moduleSpec               comma-separated list of pattern=N settings for file-filtered logging
```

### SEE ALSO

* [pharmer](/docs/reference/pharmer.md)	 - Pharmer by Appscode - Manages farms
* [pharmer describe cluster](/docs/reference/pharmer_describe_cluster.md)	 - Describe a Kubernetes cluster

