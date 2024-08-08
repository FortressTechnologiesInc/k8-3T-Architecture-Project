# Use Go 1.17 as base image
FROM golang:1.17 AS build

# Set the working directory
WORKDIR /app

# Copy Go module files
COPY go.mod go.sum ./

# Download dependencies
RUN go mod tidy

# Copy the rest of the application source code
COPY *.go ./

# Initialize Go module and get dependencies
RUN go get

# Build the Go application
RUN go install ./...

# Define the final stage
FROM golang:1.17

# Set the working directory
WORKDIR /app

# Copy the compiled binary from the build stage
COPY --from=build /go/bin/dispatch /app/

# Run the binary
CMD ["dispatch"]
