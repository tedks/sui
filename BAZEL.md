# Bazel package graph

The first child-owned Bazel package in this historical Sui fork is `//crates/prometheus-closure-metric`. It builds the existing library from `src/lib.rs` and runs `//crates/prometheus-closure-metric:closure_metric_test`, the existing test of a closure-backed Prometheus gauge and label. The module uses the repository's Rust 1.70 toolchain version and exact `anyhow`, `bytes`, `lazy_static`, `prometheus`, and `protobuf` versions from its Cargo.lock. The native `workspace-hack` dependency activates `anyhow/backtrace`, `bytes/serde`, and `lazy_static/spin_no_std` in this closure; the Bazel specs carry those features directly while leaving the rest of the workspace graph outside this target. No Sui node, SDK, framework, network, or chain fixture is an input.

The current crate resolution is scoped to x86_64 Linux. With Bazel 8.7.0 available on that platform, run from the repository root:

```bash
bazel test //crates/prometheus-closure-metric:closure_metric_test --jobs=2 --local_resources=memory=2048
```

Cargo remains the native full-workspace build. This target covers one small package, not the rest of the Sui fork. A dependency or source change needs a reviewed module update and fresh local and remote qualification.
