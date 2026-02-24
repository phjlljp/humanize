## Getting started with the Configuration API

The Configuration API is the main interface for managing application settings in Terracotta. It handles more than simple key-value storage: it validates config values, propagates changes across nodes, and supports multiple sources.

### Features

The API has three modes: static, dynamic, and hybrid. It includes built-in schema validation and pushes change notifications in real time.

Configuration changes reach all connected nodes within milliseconds. The propagation engine handles 10,000 updates per second.

### Configuration modes

**Static mode** loads values at startup from environment variables, config files, and CLI arguments. You have to restart the service to pick up changes.

**Dynamic mode** is a runtime configuration layer. Values can be hot-reloaded without restarting, and every change is versioned with rollback support and an audit log.

**Hybrid mode** combines both. You mark which keys can change at runtime and which are fixed at startup.

### Setting up your first configuration

Initialization has three steps:

1. Define your schema (structure, types, defaults).
2. Register your sources (files, env vars, remote stores).
3. Subscribe to changes so your app gets callbacks when values update.

The learning curve is steeper than most config libraries, but it pays off once you're running multiple services that need consistent settings. Downtime from config drift drops significantly, and rollbacks become a one-line operation instead of a redeployment.
