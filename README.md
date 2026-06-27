# au-paradigm | warning: this module is still experimental

Paradigm / archetype: cpp::memory-allocator

A small, focused C++ archetype that demonstrates a memory allocator paradigm for use in projects or as a template to build custom allocators. This repository provides the skeleton, examples, and tests needed to implement and evaluate allocators that conform to modern C++ allocator concepts.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Design](#design)
- [Usage](#usage)
- [Build and Test](#build-and-test)
- [Examples](#examples)
- [Contributing](#contributing)
- [License](#license)

## Overview

This project is an archetype for implementing C++ memory allocators. It focuses on clean design, testability, and clear API boundaries so you can adapt the pattern to custom allocation strategies (pool allocator, arena, bump allocator, segregated free lists, etc.). It targets modern C++ (C++17/C++20) and aims to be small and easy to integrate.

## Features

- Minimal, well-documented allocator interface
- Example allocator implementations and usage patterns
- Unit tests demonstrating correctness and basic performance checks
- CMake-based build for easy integration into existing projects

## Design

The repository is organized to separate conceptual parts:

- src/ — Core allocator implementation(s) and helper utilities
- include/ — Public header(s) exposing allocator API and C++ templates
- examples/ — Small example programs showing how to use the allocator
- tests/ — Unit tests and validation code
- docs/ — Design notes, rationale, and benchmarks (optional)

The allocator follows the Modern C++ allocator concept:
- allocate / deallocate for raw memory management
- construct / destroy for object lifetime management (if offered)
- Traits and templates so the allocator can plug into STL containers when appropriate

Design goals:
- Clarity and simplicity over micro-optimization
- Easy substitution of strategies
- Safety where possible (bounds checks in debug, RAII wrappers)

## Usage

Integrate the allocator into your project by either:
- Adding this repository as a submodule, or
- Copying the headers and implementation into your codebase, or
- Linking against a built static/shared library produced by this repo.

Typical usage with an std container (when adaptor provided):

```cpp
#include "<put it in a file>/init.hpp" // path to allocator header

// Example: use with std::vector if allocator adheres to allocator_traits
using namespace au;    // | my paradigm is within au project
prd_t mem(1024);       // | this opens a huge memory chunk that paradigm can use,

any_p say = mem.to_open(12); memset(say, "hello_world", 11);
// | to_open(len)       - allocate a region of byte
// | re_open(ptr, len)  - reallocate to a new region of memory
// | co_open(ptr, len)  - resize the ptr if it possible
mem.shut(say); // | once it need to close the ptr.
