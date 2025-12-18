# 🚀 Building a Simple REST API with Go (Golang) – A Beginner's Toolkit

This toolkit is a beginner-friendly guide to getting started with **Go (Golang)**. It documents the journey of learning the technology using generative AI prompts, building a functional REST API, and resolving common development bottlenecks.

---

## 🎯 Title & Objective

* **Title:** Go API Toolkit: From Zero to a Functional REST Endpoint
* **Chosen Technology:** Go (Golang)
* **Objective:** Harness the power of AI to learn the Go environment and build a minimalist API that returns a JSON health check endpoint (`/status`).

---

## 📝 Quick Summary of the Technology

**Go** is a statically typed, compiled programming language designed at Google.

* **What it is:** A language focused on simplicity, performance, and built-in concurrency
* **Where it’s used:** Backend systems, cloud infrastructure (Docker, Kubernetes), microservices
* **Real-world example:** Uber uses Go to power thousands of microservices due to its low latency and high execution speed

### 💡 Bonus: Go vs. Python (Flask)

Unlike Flask, which is a micro-framework relying on external dependencies and an interpreter, Go uses a powerful standard library (`net/http`) and compiles to a single binary. This makes Go faster, more memory-efficient, and well-suited for high-scale applications where performance and reliability are critical.

---

## 💻 System Requirements

* **OS:** Windows 10/11, macOS, or Linux
* **Editor:** VS Code (recommended with the official Go extension)
* **Tooling:** Go Compiler ([https://go.dev/dl](https://go.dev/dl))

---

## 🛠️ Installation & Setup Instructions

### Install Go

Download the installer for your OS and follow the default steps.

### Verify Installation

```bash
go version
```

### Initialize the Project

```bash
mkdir go-api-toolkit
cd go-api-toolkit
go mod init go-api-toolkit
```

---

## 🏃 Minimal Working Example (MWE)

### File: `main.go`

```go
package main

import (
	"encoding/json" // Package for encoding and decoding JSON
	"fmt"           // Package for formatted I/O
	"net/http"      // Package for HTTP client and server implementations
)

// Status defines the structure for our JSON response.
type Status struct {
	Message string `json:"status"`
}

// statusHandler handles incoming HTTP requests to the /status endpoint.
func statusHandler(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	response := Status{Message: "API is running"}
	err := json.NewEncoder(w).Encode(response)
	if err != nil {
		http.Error(w, "Error encoding JSON", http.StatusInternalServerError)
	}
}

func main() {
	http.HandleFunc("/status", statusHandler)
	port := ":8080"
	fmt.Printf("Server starting on http://localhost%s...\n", port)
	err := http.ListenAndServe(port, nil)
	if err != nil {
		fmt.Printf("Critical Error: %v\n", err)
	}
}
```

### How to Run

```bash
go run main.go
```

### Test the API

```bash
curl http://localhost:8080/status
```

**Expected Output:**

```json
{"status":"API is running"}
```

---

## 🧠 AI Prompt Journal

| Prompt                                                   | AI Response Summary                                  | Evaluation                       |
| -------------------------------------------------------- | ---------------------------------------------------- | -------------------------------- |
| Step-by-step guide to install Go on Windows              | Provided installation links and PATH configuration   | ⭐⭐⭐⭐☆ Made setup effortless      |
| Minimal Go REST API with one JSON endpoint               | Provided working example using `net/http` and `json` | ⭐⭐⭐⭐⭐ Great starting point       |
| Explain `listen tcp :8080: bind: address already in use` | Identified port conflict and provided resolution     | ⭐⭐⭐⭐⭐ Solved a blocker instantly |
| How to initialize Go modules for a new folder?           | Provided `go mod init` command                       | ⭐⭐⭐⭐☆ Essential for modern Go    |

---

## ⚠️ Common Issues & Expected Exceptions

| Issue / Exception          | Root Cause                           | How to Resolve                                 |
| -------------------------- | ------------------------------------ | ---------------------------------------------- |
| `go: command not found`    | Go not in system PATH                | Restart terminal or reinstall Go               |
| `address already in use`   | Port 8080 already occupied           | Change port (e.g. `:8081`) or stop the process |
| `no go.mod file found`     | Go modules not initialized           | Run `go mod init go-api-toolkit`               |
| `cannot find file main.go` | Running command from wrong directory | `cd` into the correct folder                   |
| `failed to encode JSON`    | Malformed struct or tags             | Verify struct tags and data types              |

---

## 📚 References

* Official Go Documentation: [https://go.dev/doc/](https://go.dev/doc/)
* Go by Example: [https://gobyexample.com](https://gobyexample.com)
* Learn Go with Tests
