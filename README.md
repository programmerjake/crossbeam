# Crossbeam: support for concurrent programming

[![Build Status](https://travis-ci.org/crossbeam-rs/crossbeam.svg?branch=master)](https://travis-ci.org/crossbeam-rs/crossbeam)
[![License](https://img.shields.io/badge/license-MIT%2FApache--2.0-blue.svg)](https://github.com/crossbeam-rs/crossbeam)
[![Cargo](https://img.shields.io/crates/v/crossbeam.svg)](https://crates.io/crates/crossbeam)
[![Documentation](https://docs.rs/crossbeam/badge.svg)](https://docs.rs/crossbeam)

Crossbeam supports concurrent programming, especially focusing on memory
management, synchronization, and non-blocking data structures.

Crossbeam consists of several submodules:

 - `atomic` for **enhancing `std::sync` API**. `AtomicConsume` provides
   C/C++11-style "consume" atomic operations (re-exported from
   [`crossbeam-utils`]). `ArcCell` provides atomic storage and retrieval of
   `Arc`.

 - `utils` and `thread` for **utilities**, re-exported from [`crossbeam-utils`].
   The "scoped" thread API in `thread` makes it possible to spawn threads that
   share stack data with their parents. The `utils::CachePadded` struct inserts
   padding to align data with the size of a cacheline. This crate also seeks to
   expand the standard library's few synchronization primitives (locks,
   barriers, etc) to include advanced/niche primitives, as well as userspace
   alternatives.

 - `epoch` for **memory management**, re-exported from [`crossbeam-epoch`].
   Because non-blocking data structures avoid global synchronization, it is not
   easy to tell when internal data can be safely freed. The crate provides
   generic, easy to use, and high-performance APIs for managing memory in these
   cases. We plan to support other memory management schemes, e.g. hazard
   pointers (HP) and quiescent state-based reclamation (QSBR).

 - **Concurrent data structures** which are non-blocking and much superior to
   wrapping sequential ones with a `Mutex`. Crossbeam currently provides
   channels (re-exported from [`crossbeam-channel`]), deques
   (re-exported from [`crossbeam-deque`]), queues, and stacks. Ultimately the
   goal is to also include bags, sets and maps.

# Usage

To use Crossbeam, add this to your `Cargo.toml`:

```toml
[dependencies]
crossbeam = "0.4"
```

For examples of what Crossbeam is capable of, see the [documentation][docs].

[docs]: https://docs.rs/crossbeam/
[`crossbeam-epoch`]: https://github.com/crossbeam-rs/crossbeam-epoch
[`crossbeam-utils`]: https://github.com/crossbeam-rs/crossbeam-utils
[`crossbeam-channel`]: https://github.com/crossbeam-rs/crossbeam-channel
[`crossbeam-deque`]: https://github.com/crossbeam-rs/crossbeam-deque
