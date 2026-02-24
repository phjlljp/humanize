## Getting Started With The Configuration API

The Configuration API serves as the primary interface for managing application settings in Terracotta. It's not just a simple key-value store — it's a comprehensive system for handling configuration at scale.

### Key Features And Capabilities

It's important to note that the API offers three distinct modes of operation — **static**, **dynamic**, and **hybrid** — each designed for different deployment scenarios. The system features built-in validation, supports schema definitions, and provides real-time change notifications.

Worth noting is that configuration changes propagate across all connected nodes within milliseconds. The propagation engine boasts a throughput of 10,000 updates per second — making it suitable for even the most demanding environments.

### Configuration Modes

- **Static Mode:** Static mode serves as the default configuration approach, loading values at startup from environment variables, config files, and command-line arguments. Changes require a restart.
- **Dynamic Mode:** Dynamic mode functions as a runtime configuration layer, enabling hot-reloading of values without service interruption. It supports versioning, rollback, and audit logging.
- **Hybrid Mode:** Hybrid mode represents a combination of both approaches, allowing developers to designate which keys are mutable at runtime and which remain fixed.

### Setting Up Your First Configuration

It's crucial to remember that initialization follows a three-step process. First, define your schema — this establishes the structure, types, and defaults. Second, register your sources — the API supports files, environment variables, and remote stores. Third, subscribe to changes — your application receives callbacks when values update.

The API stands as a flexible, powerful, and extensible foundation for configuration management. It should be noted that while the learning curve may seem steep, the long-term benefits — reduced downtime, consistent environments, and simplified deployments — make it a worthwhile investment.
