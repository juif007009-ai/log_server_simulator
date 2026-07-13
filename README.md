# Log Server Simulator

## Project Overview

The **Log Server Simulator** is a Python application that simulates multiple high-velocity branch servers for testing real-time log collection systems. It creates three independent TCP servers representing Swiggy branch locations (Chennai, Bangalore, and Mumbai). Once a client connects, each server continuously streams randomly generated log entries.

The simulator is designed for developers who want to test log harvesting, log parsing, regular expression validation, monitoring tools, and real-time data processing without requiring production infrastructure.

---

# Objectives

* Simulate multiple branch servers running simultaneously.
* Generate realistic log messages with timestamps.
* Stream logs continuously over TCP sockets.
* Simulate bursty traffic using random delays.
* Produce logs with different severity levels.
* Inject corrupted log entries to test parser robustness.
* Provide a realistic environment for log harvester applications.

---

# Technologies Used

* Python 3.x
* Socket Programming
* Multithreading
* Random Module
* DateTime Module
* TCP Networking

---

# Project Structure

```text
project/
│
├── log_server_simulator.py
├── README.md
```

---

# Branch Servers

The simulator starts three TCP servers.

| Branch           | Host      | Port |
| ---------------- | --------- | ---- |
| Swiggy Chennai   | 127.0.0.1 | 9001 |
| Swiggy Bangalore | 127.0.0.1 | 9002 |
| Swiggy Mumbai    | 127.0.0.1 | 9003 |

Each server runs independently in its own thread.

---

# Log Format

Every generated log follows a fixed pipe-separated format.

```text
YYYY-MM-DD HH:MM:SS | LEVEL | BRANCH_NAME | MESSAGE
```

Example:

```text
2026-07-13 13:40:10 | INFO | swiggy-chennai | Order#4521 placed successfully
2026-07-13 13:40:11 | ERROR | swiggy-mumbai | Payment gateway timeout for Order#7894
2026-07-13 13:40:12 | WARNING | swiggy-bangalore | Order#2356 delivery delayed by 10 minutes
```

This format makes it easy for log harvesters and regular expressions to parse the logs.

---

# Log Levels

The simulator randomly generates one of the following log levels:

* INFO
* WARNING
* ERROR
* DEBUG

Each level contains realistic order and delivery-related messages.

---

# Sample Log Messages

### INFO

* Order placed successfully
* Order picked up by delivery partner
* Order delivered to customer
* Restaurant accepted the order

### WARNING

* Delivery delayed
* Restaurant response time high
* High order volume detected

### ERROR

* Payment gateway timeout
* Restaurant unavailable
* GPS signal lost

### DEBUG

* Cache miss
* Database write retry

---

# Corrupted Log Injection

To simulate real-world scenarios, approximately **5%** of all generated entries are intentionally corrupted.

Example:

```text
CORRUPTED_LINE_NO_STRUCTURE_HERE
```

These malformed logs help verify that downstream applications correctly identify and reject invalid log entries.

---

# Multithreading

The application uses Python's `threading` module.

* One thread for each branch server.
* One additional thread for every connected client.
* All servers run concurrently.

This design allows multiple log streams to be generated simultaneously.

---

# Network Communication

The simulator uses TCP sockets.

**Server**

* Host: 127.0.0.1
* Ports: 9001, 9002, 9003

Clients can connect using any TCP socket implementation.

---

# Random Traffic Simulation

Instead of sending logs at a fixed interval, the simulator waits for a random duration between:

```text
0.05 seconds
to
0.40 seconds
```

This creates bursty traffic similar to production systems.

---

# How to Run

## Step 1

Ensure Python 3 is installed.

Check version:

```bash
python --version
```

---

## Step 2

Run the simulator.

```bash
python log_server_simulator.py
```

---

## Step 3

Expected output:

```text
All simulated branch servers are up.

[swiggy-chennai] listening on port 9001...
[swiggy-bangalore] listening on port 9002...
[swiggy-mumbai] listening on port 9003...
```

Keep this terminal running.

---

## Step 4

Start your log harvester or TCP client in another terminal.

Once connected, the simulator begins streaming logs automatically.

---

# Workflow

```text
Start Simulator
        │
        ▼
Create Three TCP Servers
        │
        ▼
Listen on Ports
        │
        ▼
Client Connects
        │
        ▼
Generate Random Logs
        │
        ▼
Send Logs Continuously
        │
        ▼
Inject Corrupted Logs Occasionally
        │
        ▼
Client Disconnects
        │
        ▼
Close Connection
```

---

# Expected Console Output

```text
All simulated branch servers are up.

[swiggy-chennai] listening on port 9001...
[swiggy-bangalore] listening on port 9002...
[swiggy-mumbai] listening on port 9003...

[swiggy-chennai] harvester connected, streaming logs...
```

---

# Applications

This simulator can be used for:

* Log harvesting
* Real-time log monitoring
* Socket programming practice
* Network programming assignments
* Regular expression validation
* Distributed systems testing
* Log analytics projects
* Monitoring dashboard development
* SIEM and security log testing
* Event streaming demonstrations

---

# Advantages

* Lightweight and easy to run.
* No external dependencies.
* Supports concurrent connections.
* Generates realistic log data.
* Simulates production-like traffic.
* Tests parser error handling using malformed logs.
* Simple, modular, and easy to extend.

---

# Future Enhancements

* Add SSL/TLS support.
* Store logs in files or databases.
* Support multiple simultaneous clients.
* Add configurable log generation rates.
* Generate logs in JSON format.
* Introduce additional log levels.
* Add REST API for monitoring.
* Dockerize the application.
* Export metrics for Prometheus/Grafana.
* Add command-line arguments for customization.

---

# Author

Developed as a Python socket programming project to simulate distributed log generation and test real-time log harvesting systems.
