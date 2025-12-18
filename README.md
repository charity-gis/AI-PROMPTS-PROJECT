1. Title & Objective

Title: Building a Simple REST API with Go (Golang) – A Beginner's Toolkit

Chosen Technology: Go (Golang)

Why I Chose It:
I chose Go because it is a statically typed, compiled language known for its efficiency and built-in support for high-performance networking. Moving away from interpreted languages like Python, I wanted to explore how a "low-level" language handles web requests using its standard library without needing heavy frameworks.

End Goal:
To build, run, and test a minimalist Go application that serves a JSON health-check response at the /status endpoint.

2. Quick Summary of the Technology

Go (or Golang) is an open-source language developed by Google. It focuses on simplicity, reliability, and speed.

What is it? A statically typed, compiled language with a powerful standard library.

Where is it used? Cloud-native development (Docker/Kubernetes), microservices, and high-performance backend APIs.

Real-World Example: PayPal uses Go to handle billions of transactions because of its superior concurrency model.

2.5 Bonus: Comparison (Go vs. Python/Flask)

While Flask is excellent for rapid prototyping due to its dynamic nature and minimal boilerplate, Go offers significantly better performance and type safety. Go's standard library allows you to build a production-grade server without external dependencies, whereas Flask requires several third-party libraries (like Gunicorn or Marshmallow) to reach the same level of functionality and performance.

3. System Requirements

OS: Windows 10+, macOS, or Linux.

Editor: VS Code (with the official 'Go' extension).

Tooling: Go Compiler (v1.20+).

Terminal: PowerShell, CMD, or Bash.

4. Installation & Setup Instructions

Download: Visit go.dev/dl and download the .msi (Windows) or .pkg (Mac) installer.

Install: Run the installer and keep all default settings to ensure environment variables (PATH) are set automatically.

Verify: Open a terminal and type go version. You should see the version details.

Workspace Setup:

mkdir go-api-toolkit
cd go-api-toolkit
go mod init go-api-toolkit


5. Minimal Working Example (MWE)

File: main.go

package main

import (
	"encoding/json"
	"fmt"
	"net/http"
)

type Status struct {
	Message string `json:"status"`
}

func statusHandler(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	json.NewEncoder(w).Encode(Status{Message: "API is running"})
}

func main() {
	http.HandleFunc("/status", statusHandler)
	fmt.Println("Server starting on :8080...")
	http.ListenAndServe(":8080", nil)
}


Execution:

Run go run main.go.

Visit http://localhost:8080/status in your browser.

Expected Output: {"status":"API is running"}

6. AI Prompt Journal

Prompt Used

AI's Response Summary

Evaluation of Helpfulness

"Step-by-step guide to install Go on Windows for a beginner."

Provided MSI link and PATH verification steps.

High: Saved time searching through documentation.

"Write a Go REST API with one JSON endpoint using only standard library."

Provided the main.go structure with net/http and json.NewEncoder.

High: Explained the logic of structs and handlers.

"Explain the error 'listen tcp :8080: bind: address already in use'."

Explained port conflicts and how to kill tasks or change ports.

High: Critical for debugging during local testing.

Learning Reflection: Using AI allowed me to skip the "syntax frustration" phase. Instead of struggling with how Go handles imports, I could ask the AI to explain why Go uses modules, which helped me understand the project structure much faster.

7. Common Issues & Fixes

Error: go: go.mod file not found.

Fix: Run go mod init <name> in your project folder. Go requires this to manage dependencies since version 1.11.

Error: GetFileAttributesEx main.go: system cannot find file.

Fix: You are likely in the wrong directory or named the file incorrectly. Run dir (Windows) to check if main.go exists in your current folder.

Error: Port 8080 already in use.

Fix: Change the port in main.go (e.g., :8081) or close the application currently using that port.

8. References

Official Docs: go.dev/doc/

Interactive Tutorial: A Tour of Go

Comparison Resource: Go vs Python Performance Benchmarks





