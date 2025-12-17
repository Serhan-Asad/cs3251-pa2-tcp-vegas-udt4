# TCP Vegas Congestion Control (UDT4 CCC)

This project implements the congestion avoidance behavior of **TCP Vegas** inside the **UDT4 Configurable Congestion Control (CCC)** framework.

Vegas is a **delay-based** congestion control algorithm: instead of waiting for packet loss, it monitors **RTT increases** to detect queue build-up early and adjusts the congestion window (CWND) proactively.

## What I Implemented
- Implemented Vegas-style congestion avoidance in `Vegas::onACK()` using RTT feedback.
- Tracked **Base RTT** (minimum RTT observed) and compared it to current RTT.
- Computed:
  - **Expected throughput** (using Base RTT)
  - **Actual throughput** (using current RTT and in-flight data)
  - `diff = expected - actual`
- Updated **CWND** per ACK using Vegas thresholds:
  - If `diff < alpha` → increase CWND (underutilizing)
  - If `diff > beta` → decrease CWND (congestion/queueing)
  - Else → keep CWND steady
- Tuned Vegas parameters (`alpha`, `beta`, linear increase factor) to balance throughput and RTT stability.

## Tech Stack
- C/C++ (UDT4 framework)
- UDT4 CCC interface

## Project Layout
- `src/cc.h` — Vegas congestion control implementation (main file edited)

## Build / Run
This repo is based on the provided UDT4/PA2 framework. To run it, follow the course-provided build instructions for the PA2 harness/environment.

> Note: I intentionally do not include course PDFs/handouts in this repository.

## Key Concepts Demonstrated
- Transport-layer congestion control
- RTT measurement and queueing delay inference
- Congestion window (CWND) tuning
- Throughput vs latency trade-offs
