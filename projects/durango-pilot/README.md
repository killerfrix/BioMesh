# Durango Biodiversity Pilot

BioMesh's first scientific project.

## Goal

Create a reproducible dataset of botanical and mycological observations
from Durango using existing protocols and instruments, to discover which
variables are useful and what real instrumentation gaps exist.

## Why this project first

It lets us learn botany, mycology, sampling, protocols, calibration, and
databases within a bounded scope, and discover real problems before
investing in custom hardware.

## Hardware plan (no PCB yet)

```
ESP32 + basic sensor + breadboard + Wi-Fi → PC → CSV/JSON
```

First module: microclimate (temperature, relative humidity, pressure,
light). Then: soil. Then: imaging.

## Status

Pending start. Depends on `standards/mappings/` and `docs/ecosystem-map.md`
having at least a first pass so we know which standard/hardware to use
before buying or wiring anything.
