🚀 Building a Simple REST API with Go (Golang)

This project demonstrates a minimalist Go application that exposes a single RESTful endpoint (/status) using Go's standard library (net/http). This codebase serves as the Minimal Working Example (MWE) for the "Go (Golang) Beginner's Toolkit."

🎯 Project Goal

The primary goal is to successfully build and run a minimalist Go API that provides a basic health check:

Endpoint: GET /status

Response: {"status": "API is running"}

🛠️ Setup and Installation

Prerequisites

You must have the Go Compiler and Runtime installed on your system (Windows, macOS, or Linux).

1. Project Initialization

Clone this repository or create a new folder:

mkdir go-api-toolkit
cd go-api-toolkit





Initialize Go Modules for dependency management (this creates the required go.mod file):

go mod init go-api-toolkit





🏃 Execution (Minimal Working Example)

The core application logic is contained in the single file, main.go.

1. Run the Server

Execute the application directly from your terminal:

go run main.go





Expected Console Output:

Server starting on :8080...





2. Test the Endpoint

While the server is running, open a separate terminal window and use curl to test the API endpoint:

curl http://localhost:8080/status





Expected API Response:

{"status":"API is running"}





📂 Code Reference (main.go)

(The complete code for main.go is provided below for reference, utilizing the standard net/http and encoding/json packages.)

package main

import (
	"encoding/json" 
	"fmt"
	"net/http"    
)

// Define the structure for our JSON response
type Status struct {
	Status string `json:"status"` 
}

// Handler function for the /status endpoint
func statusHandler(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	response := Status{Status: "API is running"}
	
	err := json.NewEncoder(w).Encode(response)
	if err != nil {
		http.Error(w, "Failed to encode JSON", http.StatusInternalServerError)
	}
}

func main() {
	http.HandleFunc("/status", statusHandler)
	fmt.Println("Server starting on :8080...")
	
	err := http.ListenAndServe(":8080", nil)
	if err != nil {
		fmt.Printf("Server failed to start: %v\n", err)
	}
}



