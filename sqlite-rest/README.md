# Wick SQLite REST App

Welcome to the Wick SQLite REST App, a sample project demonstrating how to use Wick to perform SQL queries on a SQLite engine and expose them through a RESTful HTTP API.

## Prerequisites

- [Wick](https://candle.dev/docs/wick/) installed on your system.
- SQLite installed and available in your PATH.

## Getting Started

To get this project up and running on your local machine, follow these steps:

### 1. Clone the Repository

```bash
git clone git@github.com:candlecorp/wick-apps.git
cd sqlite-rest
```

### 2. Set up Environment Variables

This project uses environment variables to configure and run the app. These variables are housed in the `.env` file in the root of the project. Before running the application, ensure you've set up the required variables.

### 3. Run the App

Run the Wick app with:

```bash
wick run app.wick
```
