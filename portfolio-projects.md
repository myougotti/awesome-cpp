# C++ Portfolio Projects

A curated set of buildable C++ project ideas — drawn from the categories in
[README.md](README.md) — that produce something concrete you can show off.
Each entry lists what you'll build, the skills it demonstrates, and which
sections of this list to mine for libraries.

Difficulty: 🟢 beginner · 🟡 intermediate · 🔴 advanced

- [Systems & Tooling](#systems--tooling)
- [Networking & Distributed](#networking--distributed)
- [Graphics, Games & Simulation](#graphics-games--simulation)
- [Compilers, Languages & VMs](#compilers-languages--vms)
- [Data, Storage & Search](#data-storage--search)
- [Audio, Image & Multimedia](#audio-image--multimedia)
- [Concurrency & Performance](#concurrency--performance)
- [AI / ML from Scratch](#ai--ml-from-scratch)
- [How to use this list](#how-to-use-this-list)

---

## Systems & Tooling

### 🟢 Command-line file utility (grep / wc / tree clone)
Reimplement a small Unix tool end-to-end. Argument parsing, file I/O, basic
regex, and clean error handling.
- Skills: idiomatic modern C++, RAII, `std::filesystem`, unit testing.
- Libraries: [CLI](README.md#cli), [Regular Expression](README.md#regular-expression).

### 🟡 JSON / YAML / TOML parser from scratch
Hand-roll a parser (recursive descent or table-driven) for one of the
formats. Compare your output against an existing library on a fuzz corpus.
- Skills: lexing/parsing, error recovery, allocator-aware containers.
- Libraries: compare against [JSON](README.md#json), [Yaml](README.md#yaml).

### 🟡 Static analyzer / linter for a tiny C subset
Walk an AST (Clang's LibTooling) and flag a handful of real bugs — null
deref, unchecked return, missing `override`. Ship as a CLI plus pre-commit
hook.
- Skills: AST traversal, pattern matching, build-system integration.
- Libraries: [Static Code Analysis](README.md#static-code-analysis), [Compiler](README.md#compiler).

### 🔴 Mini debugger (ptrace-based)
Single-step, breakpoints (int 3 patching), register/memory inspection, and
basic DWARF symbol resolution. Linux/x86-64.
- Skills: ELF/DWARF, ptrace, signals, low-level OS.
- Libraries: [Debugger](README.md#debugger), [Debug](README.md#debug).

---

## Networking & Distributed

### 🟢 HTTP/1.1 server (no framework)
Sockets only. Parse the request line + headers, serve static files, support
keep-alive and chunked transfer. Bench against nginx for a realistic number.
- Skills: BSD sockets, parsing, IO multiplexing (`epoll`/`kqueue`).
- Libraries: [Networking](README.md#networking), [Asynchronous Event Loop](README.md#asynchronous-event-loop).

### 🟡 Real-time chat server
TCP or WebSocket, multiple rooms, presence, message history. CLI client +
optional web client. Add TLS for bonus points.
- Skills: async I/O, protocol design, concurrency.
- Libraries: [Networking](README.md#networking), [Cryptography](README.md#cryptography).

### 🟡 BitTorrent client
Parse `.torrent` (bencode), talk to trackers, manage peers, handle piece
selection and rarest-first. Don't aim for full spec — stick to BEP 3.
- Skills: binary protocols, state machines, scheduling.
- Libraries: [BitTorrent](README.md#bittorrent), [Networking](README.md#networking).

### 🔴 Raft- or Paxos-based replicated KV store
Three-node cluster, leader election, log replication, snapshot + log
compaction. Drive with Jepsen-style fault injection.
- Skills: distributed systems, persistence, deterministic testing.
- Libraries: [Networking](README.md#networking), [Database](README.md#database), [Concurrency](README.md#concurrency).

---

## Graphics, Games & Simulation

### 🟢 Conway's Game of Life (with a real UI)
Use Dear ImGui or SFML. Adjustable speed, drag-to-paint, save/load patterns
(RLE format). It's small but a great showcase of clean architecture.
- Skills: game loop, separation of model/view, file formats.
- Libraries: [GUI](README.md#gui), [Graphics](README.md#graphics).

### 🟡 2D game (Tetris / Asteroids / Snake)
Pick one and finish it: menus, scoring, sound, particles. Polish matters —
juicy feedback is what makes the demo memorable.
- Skills: ECS or simple OOP, asset pipeline, audio mixing.
- Libraries: [Game Engine](README.md#game-engine), [Audio](README.md#audio), [Graphics](README.md#graphics).

### 🟡 Software ray tracer ("Ray Tracing in One Weekend" → ...the Next Week)
Spheres, materials, BVH, motion blur, textures, volumes. Output PPM, then
add a viewer.
- Skills: linear algebra, performance tuning, multithreading.
- Libraries: [Math](README.md#math), [Image Processing](README.md#image-processing).

### 🔴 Mini 3D engine (OpenGL / Vulkan)
Forward renderer with PBR materials, IBL, shadow maps, glTF loading, and an
ImGui scene editor. Stop before you build a full engine — stop at "I can
load a scene and inspect it."
- Skills: GPU APIs, shader authoring, scene graphs, asset pipelines.
- Libraries: [Graphics](README.md#graphics), [Game Engine](README.md#game-engine), [Physics](README.md#physics).

### 🔴 Rigid-body physics from scratch
Broadphase + narrowphase collision, constraints, sequential-impulse solver.
Demo with falling stacks and a 2D platformer character controller.
- Skills: numerical methods, debugging non-determinism.
- Libraries: [Physics](README.md#physics), [Math](README.md#math).

---

## Compilers, Languages & VMs

### 🟡 CHIP-8 emulator
A weekend project that teaches you emulation properly: opcodes, timers,
display, input. Add a debugger window with disassembly.
- Skills: bit-twiddling, timing, emulator architecture.
- Libraries: [Virtual Machines](README.md#virtual-machines), [GUI](README.md#gui).

### 🟡 NES or GameBoy emulator
Bigger commitment; hugely impressive when it boots a real ROM. Plenty of
test ROMs and reference docs.
- Skills: cycle accuracy, mappers, audio synthesis.
- Libraries: [Virtual Machines](README.md#virtual-machines), [Audio](README.md#audio).

### 🟡 Lox / Monkey-style interpreter (tree-walking)
Follow *Crafting Interpreters* but write it in modern C++ with `std::variant`
visitors instead of OOP.
- Skills: lexing, parsing, evaluation, closures, GC basics.
- Libraries: [Scripting](README.md#scripting), [Compiler](README.md#compiler).

### 🔴 Bytecode VM + compiler for a small language
Stack VM, register allocation for locals, mark-and-sweep GC, FFI to C. If
you go further: a single-pass JIT with [asmjit].
- Skills: codegen, GC, calling conventions.
- Libraries: [Virtual Machines](README.md#virtual-machines), [Compiler](README.md#compiler).

[asmjit]: https://github.com/asmjit/asmjit

---

## Data, Storage & Search

### 🟡 Embedded key-value store (mini Redis / mini LevelDB)
Pick a flavor: in-memory with AOF persistence (Redis-style) or LSM-tree on
disk (LevelDB-style). Add a wire protocol so `redis-cli` or a custom CLI can
talk to it.
- Skills: data structures, durability, crash recovery.
- Libraries: [Database](README.md#database), [Containers](README.md#containers), [Serialization](README.md#serialization).

### 🟡 Full-text search engine
Inverted index, tokenization, BM25 ranking, snippet generation. Ingest a
Wikipedia dump for a real demo.
- Skills: information retrieval, mmap, on-disk formats.
- Libraries: [Database](README.md#database), [Image Processing](README.md#image-processing) (for OCR demos).

### 🔴 SQL query engine (read-only)
Parse a SQL subset, plan it (rule-based optimizer), execute over CSV/Parquet
files. Volcano-style iterators or vectorized — pick one and justify it.
- Skills: query planning, columnar formats, codegen.
- Libraries: [Database](README.md#database), [CSV](README.md#csv), [Compiler](README.md#compiler).

---

## Audio, Image & Multimedia

### 🟢 Audio visualizer
FFT a microphone or file stream, render bars / waveform / spectrogram.
Looks great in a portfolio video.
- Skills: DSP basics, real-time graphics, ring buffers.
- Libraries: [DSP](README.md#dsp), [Audio](README.md#audio), [Graphics](README.md#graphics).

### 🟡 Image processing pipeline / mini Photoshop
Layers, blend modes, non-destructive filters (blur, sharpen, levels), undo
stack. Make it scriptable.
- Skills: pixel math, command pattern for undo, color spaces.
- Libraries: [Image Processing](README.md#image-processing), [GUI](README.md#gui).

### 🔴 Software synthesizer / DAW-lite
Oscillators, envelopes, filters, MIDI in, low-latency audio out. Sequence a
short demo track to ship with the project.
- Skills: real-time audio, lock-free queues, plugin formats (VST/CLAP).
- Libraries: [Audio](README.md#audio), [DSP](README.md#dsp).

---

## Concurrency & Performance

### 🟢 Thread pool + futures library
Work-stealing deque, `submit` returning `std::future`, cancellation tokens.
Benchmark against `std::async` and `tbb::task_group`.
- Skills: atomics, memory ordering, lock-free data structures.
- Libraries: [Concurrency](README.md#concurrency).

### 🟡 Custom allocator suite
Bump, pool, slab, and a small-object allocator. Plug into STL containers
and benchmark on realistic workloads (parser, ECS, JSON).
- Skills: allocator API, fragmentation analysis, profiling.
- Libraries: [Memory Allocation](README.md#memory-allocation).

### 🟡 Async runtime / coroutine scheduler
C++20 coroutines, an `io_uring` or `epoll` reactor, timers, cancellation. A
real "tokio for C++" sized down to weekend scope.
- Skills: coroutines, executors, async cancellation.
- Libraries: [Asynchronous Event Loop](README.md#asynchronous-event-loop), [Concurrency](README.md#concurrency).

---

## AI / ML from Scratch

### 🟡 Neural network library (CPU)
Tensors, autograd, SGD/Adam, train MNIST to >97%. No PyTorch — but compare
your speed to it honestly.
- Skills: numerical stability, SIMD, cache-friendly code.
- Libraries: [Machine Learning](README.md#machine-learning), [Math](README.md#math), [Scientific Computing](README.md#scientific-computing).

### 🔴 Tiny LLM inference engine
Load a small open-weights model (e.g. TinyLlama / Pythia-160M), implement
the transformer forward pass, KV cache, and a sampler. CPU is fine — speed
is a stretch goal.
- Skills: GEMM, quantization, memory layout.
- Libraries: [Machine Learning](README.md#machine-learning), [Math](README.md#math).

---

## How to use this list

1. **Pick one project, not three.** Portfolio impact comes from polish — a
   finished Tetris beats three half-built engines.
2. **Define done before starting.** Write the README first: what it does,
   how to build, a screenshot or asciinema. Reverse-engineer the scope from
   that.
3. **Mine [README.md](README.md) for libraries** in the linked sections —
   but be honest about what you wrote yourself vs. pulled in. "Built on
   SDL + Dear ImGui" is fine; "wrote a renderer" should mean you wrote one.
4. **Write tests and a benchmark.** Both are differentiators in interviews.
5. **Ship a demo.** GIF, video, or live link. If a recruiter has to clone
   and build to see it, they won't.

Contributions welcome — open a PR adding a project idea (with the same
shape: difficulty, one-paragraph scope, skills, libraries section links).
