# Github Actions to AWS Elastic Beanstalk

This is a simple .NET 6.0 web API that provides basic arithmetic operations such as addition and subtraction. The API is built using minimal APIs and is set up for continuous deployment to AWS Elastic Beanstalk using GitHub Actions.

## Features

- **Addition**: Returns the sum of two integers.
- **Subtraction**: Returns the difference between two integers.

## Project Structure

### 1. `Program.cs`

This file contains the main code for the API:

- **Routes**:
  - `GET /`: Returns a "Hello World!" message.
  - `GET /add?num1=<int>&num2=<int>`: Returns the sum of `num1` and `num2`.
  - `GET /subtract?num1=<int>&num2=<int>`: Returns the difference between `num1` and `num2`.

- **Helper Methods**:
  - `string AddNumbers(int num1, int num2)`: Calculates the sum and returns a string message.
  - `string SubtractNumbers(int num1, int num2)`: Calculates the difference and returns a string message.

### 2. `.github/workflows/aws.yml`

This file defines a GitHub Actions workflow to build and deploy the application to AWS Elastic Beanstalk:

- **Triggers**:
  - The workflow is triggered on each push to the `main` branch.

- **Jobs**:
  - **Build**: 
    - Checks out the repository.
    - Sets up .NET 6.0.
    - Builds the project and publishes it to a folder named `site`.
    - Zips the contents of the `site` folder for deployment.
  - **Deploy**:
    - Deploys the zipped package to AWS Elastic Beanstalk using the `beanstalk-deploy` action.

## Getting Started

### Prerequisites

- [.NET 6.0 SDK](https://dotnet.microsoft.com/download/dotnet/6.0) should be installed on your machine.
- AWS Elastic Beanstalk setup for deployment.

### Running the API Locally

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/calculator-api.git
   cd calculator-api
   ```
2. Run the API:
   ```bash
   dotnet run
   ```
3. The API will be available at http://localhost:5000.

### Accessing the root endpoint:
  ```markdown
  curl http://localhost:5000/
  Response: Hello World!
  ```

### Performing addition:
  ```markdown
  curl http://localhost:5000/add?num1=5&num2=3
  Response: Summan av 5 och 3 är: 8
  ```

### Performing subtraction:
  ```markdown
  curl http://localhost:5000/subtract?num1=5&num2=3
  Response: Subtraktion av 5 och 3 är: 2
  ```

## Deploying to AWS
The project is configured for continuous deployment using GitHub Actions. Ensure you have the following GitHub secrets set up in your repository:
  ```markdown
  AWS_ACCESS_KEY_ID: Your AWS access key ID.
  AWS_SECRET_ACCESS_KEY: Your AWS secret access key.
  ```
On each push to the main branch, the workflow will automatically build the project and deploy it to your AWS Elastic Beanstalk environment.
