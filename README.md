
# new

using a custom rust env from https://github.com/meta-introspector/platform-tools-agave-rust-solana

## latest experiment
```
export MALLOC_CONF=prof:true,lg_prof_interval:31,lg_prof_sample:1,prof_prefix:/home/mdupont/2025/05/27/agave-solana-validator/profiles/solana-test-validator/new/profile1/jeprofile
cargo run --bin solana-test-validator  -- --limit-ledger-size 0
./jeprof ./solana-test-validator ~/2025/05/27/agave-solana-validator/profiles/solana-test-validator/new/profile1/jeprofile.153462.0.i0.heap  --svg > test.svg



./jeprof ./solana-test-validator ~/2025/05/27/agave-solana-validator/profiles/solana-test-validator/new/profile1/jeprofile.164383.0.i0.heap




```
  
Other experiments

```
cargo run --bin solana-test-validator  --limit-ledger-size 0

``

export MALLOC_CONF=prof:true,lg_prof_interval:31,lg_prof_sample:1,prof_prefix:/home/mdupont/2025/05/27/agave-solana-validator/profiles/solana-test-validator/new/profile1/jeprofile

export MALLOC_CONF=prof:true,lg_prof_interval:25,lg_prof_sample:25,prof_prefix:/home/mdupont/2025/05/27/agave-solana-validator/profiles/solana-test-validator/new/profile1/jeprofile

export MALLOC_CONF=prof:true,lg_prof_interval:125,lg_prof_sample:25,prof_prefix:/home/mdupont/2025/05/27/agave-solana-validator/profiles/solana-test-validator/new/profile1/jeprofile



mdupont@mdupont-G470:~/2025/04/25/agave-solana-validator/target/debug$ ./jeprof  ~/2025/05/27/agave-solana-validator/profiles/solana-test-validator/jeprof.3789843.133510.i133510.heap --show_bytes

/home/mdupont/2024/08/05/jemalloc/bin/jeprof


## sources

https://clickhouse.com/docs/operations/allocation-profiling

using https://github.com/gimli-rs/addr2line.git
https://github.com/jemalloc/jemalloc/wiki/Use-Case%3A-Leak-Checking
https://github.com/jemalloc/jemalloc/wiki/Use-Case%3A-Heap-Profiling
https://github.com/0xdeafbeef/jeprofl
https://github.com/jemalloc/jemalloc/tree/dev
https://jemalloc.net/
https://www.polarsignals.com/blog/posts/2023/12/20/rust-memory-profiling


# old
<p align="center">
  <a href="https://solana.com">
    <img alt="Solana" src="https://i.imgur.com/0vfIMHo.png" width="250" />
  </a>
</p>

[![Solana crate](https://img.shields.io/crates/v/solana-core.svg)](https://crates.io/crates/solana-core)
[![Solana documentation](https://docs.rs/solana-core/badge.svg)](https://docs.rs/solana-core)
[![Build status](https://badge.buildkite.com/8cc350de251d61483db98bdfc895b9ea0ac8ffa4a32ee850ed.svg?branch=master)](https://buildkite.com/solana-labs/solana/builds?branch=master)
[![codecov](https://codecov.io/gh/solana-labs/solana/branch/master/graph/badge.svg)](https://codecov.io/gh/solana-labs/solana)

# Building

## **1. Install rustc, cargo and rustfmt.**

```bash
$ curl https://sh.rustup.rs -sSf | sh
$ source $HOME/.cargo/env
$ rustup component add rustfmt
```

When building the master branch, please make sure you are using the latest stable rust version by running:

```bash
$ rustup update
```

When building a specific release branch, you should check the rust version in `ci/rust-version.sh` and if necessary, install that version by running:
```bash
$ rustup install VERSION
```
Note that if this is not the latest rust version on your machine, cargo commands may require an [override](https://rust-lang.github.io/rustup/overrides.html) in order to use the correct version.

On Linux systems you may need to install libssl-dev, pkg-config, zlib1g-dev, protobuf etc.

On Ubuntu:
```bash
$ sudo apt-get update
sudo apt-get install libssl-dev libudev-dev pkg-config zlib1g-dev llvm clang cmake make libprotobuf-dev protobuf-compiler libclang-dev
```

On Fedora:
```bash
$ sudo dnf install openssl-devel systemd-devel pkg-config zlib-devel llvm clang cmake make protobuf-devel protobuf-compiler perl-core libclang-dev
```

## **2. Download the source code.**

```bash
$ git clone https://github.com/anza-xyz/agave.git
$ cd agave
```

## **3. Build.**

```bash
$ ./cargo build
```

> [!NOTE]
> Note that this builds a debug version that is **not suitable for running a testnet or mainnet validator**. Please read [`docs/src/cli/install.md`](docs/src/cli/install.md#build-from-source) for instructions to build a release version for test and production uses.

# Testing

**Run the test suite:**

```bash
$ ./cargo test
```

### Starting a local testnet

Start your own testnet locally, instructions are in the [online docs](https://docs.solanalabs.com/clusters/benchmark).

### Accessing the remote development cluster

* `devnet` - stable public cluster for development accessible via
devnet.solana.com. Runs 24/7. Learn more about the [public clusters](https://docs.solanalabs.com/clusters)

# Benchmarking

First, install the nightly build of rustc. `cargo bench` requires the use of the
unstable features only available in the nightly build.

```bash
$ rustup install nightly
```

Run the benchmarks:

```bash
$ cargo +nightly bench
```

# Release Process

The release process for this project is described [here](RELEASE.md).

# Code coverage

To generate code coverage statistics:

```bash
$ scripts/coverage.sh
$ open target/cov/lcov-local/index.html
```

Why coverage? While most see coverage as a code quality metric, we see it primarily as a developer
productivity metric. When a developer makes a change to the codebase, presumably it's a *solution* to
some problem.  Our unit-test suite is how we encode the set of *problems* the codebase solves. Running
the test suite should indicate that your change didn't *infringe* on anyone else's solutions. Adding a
test *protects* your solution from future changes. Say you don't understand why a line of code exists,
try deleting it and running the unit-tests. The nearest test failure should tell you what problem
was solved by that code. If no test fails, go ahead and submit a Pull Request that asks, "what
problem is solved by this code?" On the other hand, if a test does fail and you can think of a
better way to solve the same problem, a Pull Request with your solution would most certainly be
welcome! Likewise, if rewriting a test can better communicate what code it's protecting, please
send us that patch!
