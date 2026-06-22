# Hello World GitHub Action

A simple GitHub Action that greets a person and records the timestamp when the greeting occurred. This action demonstrates the basic structure and capabilities of GitHub Actions, including input handling, output generation, and event payload access.

## Description

This action performs the following operations:

1. **Greets the specified person** - Takes a name as input and generates a greeting message
2. **Records the timestamp** - Captures and outputs the exact time when the greeting was executed
3. **Logs event payload** - Displays the GitHub event payload that triggered the workflow (useful for debugging and understanding workflow context)

The action is built using Node.js 20 and leverages the official GitHub Actions toolkit libraries (`@actions/core` and `@actions/github`).

## Inputs

### `who-to-greet`

**Required**: Yes  
**Default**: `World`  
**Description**: The name of the person to greet.

This input specifies who should be greeted by the action. If not provided, it defaults to "World".

## Outputs

### `time`

**Description**: The timestamp when the greeting was executed.

This output contains the time string in the format returned by JavaScript's `Date.toTimeString()` method (e.g., "14:30:15 GMT+0000 (Coordinated Universal Time)").

## Secrets

This action does not require any secrets.

## Environment Variables

This action does not use any custom environment variables. It operates using the standard GitHub Actions runtime environment.

## Usage Example

### Basic Usage

```yaml
name: Greet Someone
on: [push]

jobs:
  greeting:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      
      - name: Say hello
        uses: shihack/TestAction@v1
        with:
          who-to-greet: 'Alice'
```

### Using the Output

```yaml
name: Greet and Display Time
on: [push]

jobs:
  greeting-with-output:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      
      - name: Greet someone
        id: greeting
        uses: shihack/TestAction@v1
        with:
          who-to-greet: 'Bob'
      
      - name: Display greeting time
        run: echo "The greeting occurred at ${{ steps.greeting.outputs.time }}"
```

### Using Default Value

```yaml
name: Default Greeting
on: [workflow_dispatch]

jobs:
  default-greeting:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      
      - name: Greet with default name
        uses: shihack/TestAction@v1
        # No 'with' block - will use default "World"
```

### Multiple Jobs Example

```yaml
name: Multiple Greetings
on: [push]

jobs:
  greet-team:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        name: ['Alice', 'Bob', 'Charlie']
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      
      - name: Greet team member
        uses: shihack/TestAction@v1
        with:
          who-to-greet: ${{ matrix.name }}
```

## Development

### Prerequisites

- Node.js 20 or higher
- npm

### Setup

```bash
# Clone the repository
git clone https://github.com/shihack/TestAction.git
cd TestAction

# Install dependencies
npm install
```

### Building

This action requires the distribution files to be built before use:

```bash
# Build the action (compile/bundle your code)
npm run build  # or your specific build command
```

Make sure to commit the `dist/` directory to your repository as GitHub Actions requires it.

## License

ISC

## Repository

[https://github.com/shihack/TestAction](https://github.com/shihack/TestAction)
