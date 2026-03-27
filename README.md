# Disk Recovery Tool

## Overview
This repository contains a disk recovery tool with a C# frontend and a Rust backend. The tool aims to assist users in recovering lost or corrupted data from various types of storage devices.

## Project Structure
- `frontend/`: Contains the C# frontend application.
- `backend/`: Contains the Rust backend service.
- `README.md`: Project documentation.

## Setup Instructions
### Prerequisites
- .NET SDK (for the C# frontend)
- Rust (for the backend)

### Getting Started
1. Clone the repository:
   ```bash
   git clone https://github.com/289536014-bot/data.git
   cd data
   ```
2. Set up the frontend:
   ```bash
   cd frontend
   dotnet restore
   dotnet build
   ```
3. Set up the backend:
   ```bash
   cd ../backend
   cargo build
   ```
4. Run the applications as needed.
