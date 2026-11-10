# Bazel package graph

The first child-owned Bazel package in this historical Sui fork is `//crates/prometheus-closure-metric`. It builds the existing library from `src/lib.rs` and runs `//crates/prometheus-closure-metric:closure_metric_test`, the existing test of a closure-backed Prometheus gauge and label. The module uses the repository's Rust 1.70 toolchain version and exact `anyhow`, `prometheus`, and `protobuf` versions from its Cargo.lock. No Sui node, SDK, framework, network, or chain fixture is an input.

With Bazel 8.7.0 available, run from the repository root:

```bash
bazel test //crates/prometheus-closure-metric:closure_metric_test --jobs=2 --local_resources=memory=2048
```

Cargo remains the native full-workspace build. This target covers one small package, not the rest of the Sui fork. A dependency or source change needs a reviewed module update and fresh local and remote qualification.
