# Debugging LND

1. [Overview](debugging_lnd.md#overview)
2. [Debug Logging](debugging_lnd.md#debug-logging)
3. [Capturing pprof data with `lnd`](debugging_lnd.md#capturing-pprof-data-with-lnd)

## Overview

`lnd` ships with a few useful features for debugging, such as a built-in profiler and tunable logging levels. If you need to submit a bug report for `lnd`, it may be helpful to capture debug logging and performance data ahead of time.

## Debug Logging

You can enable debug logging in `lnd` by passing the `--debuglevel` flag. For example, to increase the log level from `info` to `debug`:

```text
⛰  lnd --debuglevel=debug
```

You may also specify logging per-subsystem, like this:

```text
⛰  lnd --debuglevel=<subsystem>=<level>,<subsystem2>=<level>,...
```

## Capturing pprof data with `lnd`

`lnd` has a built-in feature which allows you to capture profiling data at runtime using [pprof](https://golang.org/pkg/runtime/pprof/), a profiler for Go. The profiler has negligible performance overhead during normal operations \(unless you have explicitly enabled CPU profiling\).

To enable this ability, start `lnd` with the `--profile` option using a free port.

```text
⛰  lnd --profile=9736
```

Now, with `lnd` running, you can use the pprof endpoint on port 9736 to collect runtime profiling data. You can fetch this data using `curl` like so:

```text
⛰  curl http://localhost:9736/debug/pprof/goroutine?debug=1
...
```

