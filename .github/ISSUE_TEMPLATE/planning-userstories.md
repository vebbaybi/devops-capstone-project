# Planning User Stories

## User Story 1: Set up the development environment

**As a** developer  
**I need** to set up a local Python Flask environment with all dependencies installed  
**So that** I can write microservice code and run unit tests locally

### Details and Assumptions

- The environment relies on Python 3 and the dependencies listed in `requirements.txt`.
- Execution is verified using the laboratory shell environment.

### Acceptance Criteria

```gherkin
Given a freshly cloned capstone repository
When I run pip install -r requirements.txt
Then all Flask and testing dependencies are installed without errors
And running the test suite returns a passing status
```

## User Story 2: Read an account from the service

**As an** account service consumer  
**I need** to retrieve a specific account by its ID  
**So that** I can view the details of an existing account

### Details and Assumptions

- Endpoint: `GET /accounts/<id>`
- Returns `200 OK` with JSON account data if found.
- Returns `404 NOT FOUND` if the account ID does not exist.

### Acceptance Criteria

```gherkin
Given an account with ID 1 exists in the database
When I send a GET request to "/accounts/1"
Then I receive a 200 OK status code
And the response contains the account details in JSON

Given an account with ID 9999 does not exist
When I send a GET request to "/accounts/9999"
Then I receive a 404 NOT FOUND status code
```

## User Story 3: Update an account in the service

**As an** account service consumer  
**I need** to update an existing account's details by its ID  
**So that** account records remain accurate

### Details and Assumptions

- Endpoint: `PUT /accounts/<id>`
- Accepts a JSON body containing the fields to update.
- Returns `200 OK` with the updated JSON payload.
- Returns `404 NOT FOUND` if the account does not exist.

### Acceptance Criteria

```gherkin
Given an account with ID 1 exists in the database
When I send a PUT request to "/accounts/1" with updated JSON data
Then I receive a 200 OK status code
And the account data in the database reflects the updated values
```

## User Story 4: Delete an account from the service

**As an** account service consumer  
**I need** to delete an account using its ID  
**So that** unwanted accounts are removed from the system

### Details and Assumptions

- Endpoint: `DELETE /accounts/<id>`
- Returns `204 NO CONTENT` after successful removal.

### Acceptance Criteria

```gherkin
Given an account with ID 1 exists in the database
When I send a DELETE request to "/accounts/1"
Then I receive a 204 NO CONTENT status code
And a subsequent GET request to "/accounts/1" returns a 404 NOT FOUND status code
```

## User Story 5: List all accounts in the service

**As an** account service consumer  
**I need** to retrieve a list of all accounts  
**So that** I can view every registered account in the system

### Details and Assumptions

- Endpoint: `GET /accounts`
- Returns `200 OK` with a JSON list of all accounts.
- Returns an empty array (`[]`) if no accounts exist.

### Acceptance Criteria

```gherkin
Given accounts exist in the database
When I send a GET request to "/accounts"
Then I receive a 200 OK status code
And the response contains a JSON list of all existing accounts
```

## User Story 6: Containerize the microservice using Docker

**As a** DevOps engineer  
**I need** to package the Flask account service into a Docker image  
**So that** it can run consistently in any containerized environment

### Details and Assumptions

- The image is built using the project's `Dockerfile`.
- Gunicorn/WSGI serves the Flask application on port `8080` (or `5000`).

### Acceptance Criteria

```gherkin
Given a Dockerfile exists in the project root directory
When I build the Docker image and start the container
Then the Flask application starts successfully inside the container
And HTTP requests return successful status codes
```

## User Story 7: Deploy the Docker image to Kubernetes

**As a** cloud engineer  
**I need** to deploy the Docker image to a Kubernetes cluster  
**So that** the account microservice runs with managed orchestration and external access

### Details and Assumptions

- The deployment uses Kubernetes `deployment.yaml` and `service.yaml` manifests.
- The target environment is the provided Kubernetes/OpenShift cluster.

### Acceptance Criteria

```gherkin
Given a published Docker image and valid Kubernetes manifests
When I apply the deployment and service manifests to the cluster
Then the account service pods transition to a Running status
And the service route exposes the microservice endpoints to HTTP traffic
```
