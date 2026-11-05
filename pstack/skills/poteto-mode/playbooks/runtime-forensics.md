### Runtime forensics

**You own the diagnosis. Instrument the live process, don't theorize from source.** The deliverable is a cited diagnosis, not a fix.

1. Capture the live signal on the matching surface via the control skill: a CPU profile for a spinning process, a heap snapshot for a leak, a CDP trace for a visual glitch. A real artifact, not a guess. On mobile, the signal is the device crash report (`.ips`) plus the app's own MetricKit and crash-reporter events. Check the report's hardware model and incident time against the reported incident before reading it. A `0x8BADF00D` watchdog kill is not a crash: crash dashboards file it elsewhere (or not at all), and MetricKit delivers it on the next launch, stamped with the delivery time.
2. Reduce the artifact to the smoking gun: the function on the hot path, the retainer chain from the leaked object to a GC root, the loop firing without input. Parse large artifacts in a subagent (the **guard-the-context-window** principle skill), keep the reduced finding in the main thread. Pick each subagent's reasoning level and fast or standard speed for the job, per the Subagents section.
3. Prove the mechanism before believing it. Inject instrumentation via CDP eval on the running process, or hotfix the live code without reloading, to confirm the hypothesis cheaply. A claim that something is absent from your own repo ("nothing reports X", "no step uploads Y") is a mechanism claim too: quote the grep beside it before any inference rests on it.
4. Map the finding back to source: file, symbol, the line that allocates or schedules.
5. Throughput checkpoint stays one line: `throughput checkpoint: n/a, read-only forensics`.

**Reply:** the signal captured, the reduced finding, how you proved the mechanism, the source location, artifact paths. Say which reported incident the artifact belongs to, and whether the originally reported symptom is still unexplained. No fix unless asked. Hand back to Bug fix or Perf once the cause is known.
