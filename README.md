# lingshu-gpu-gateway

Netty RPC gateway for LingShu GPU pool.

## Architecture

Reuses lingshu-cloud-basic `NetServer` + `AbstractChannelHandler`:

```
GpuGatewayChannelHandler (interestPackageTypes = {100, 101, 102})
  ↓
GpuTaskService (local Spring bean)
  ↓
Scheduler (via local RPC in MVP, gRPC in v0.5)
```

## MVP scope (STORY-2-1)

- Long connection pool with heartbeat
- Per-business + per-Pod quota enforcement
- L4 routing rules
- Bypass JVM direct calls in MVP (call `GpuTaskService` bean)

## Deferred to hardening

mTLS, RBAC, audit log, custom 5xx error codes.
