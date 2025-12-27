# Job Manager DEVision - Subsystem

**Live Demo:** [https://f4p1e.github.io/JM_Service_Demo/](https://f4p1e.github.io/JM_Service_Demo/)

## About
This project serves as a "Deep Dive" visualizer for the Staging (v2.4) environment of the Job Manager subsystem. It maps out the flow of data from the client through the API gateway, authentication layers, event bus, and various backend microservices.

Key capabilities include simulating traffic flow and a "Chaos Mode" to test how the system handles service failures.

## Architecture StackThe visualization displays a modern microservices architecture powered by the following technologies:

* **Frontend:** React.js (Browser/App Client)
* **API Gateway:** Kong GW (Handling `/api/v1/*` routes)
* **Message Broker:** Apache Kafka (Topic: `GLOBAL.EVENTS` with Zookeeper coordination)
* **Backend Services:** Java / Spring Boot
* **Databases & Storage:**
* PostgreSQL (`profiles_db`, `subs_db`, `ledger`)
* MongoDB (`jobs`)
* Redis (Queues)
* Pinecone (Vector Database for Matching)
* Elasticsearch (Search Indexing)



## Features
### 1. Interactive Architecture DiagramA visual graph connecting all system components, showing the relationship between the Client, Gateway, Auth Service, Kafka Bus, and downstream microservices.

### 2. Chaos Mode (Resilience Testing)Toggle specific microservices **OFFLINE** to simulate outages and observe system behavior. Available services to toggle include:

* **Company Svc** (Profile Manager)
* **Notify Svc** (Mail/SMS)
* **Sub Svc** (Subscription Plans)
* **Payment Svc** (Transactions)
* **Job Svc** (Job CRUD)
* **Match Svc** (Applicant Engine)
* **Search Svc** (Indexer)

### 3. Event Flow Simulation **`EXECUTE_EVENT_FLOW()`**: Triggers a simulated transaction or event sequence to visualize how data propagates through the system.
* **Payload Inspector**: A console window that displays real-time request/response payloads and traffic logs.

## Usage 1. Open the [Live Demo](https://f4p1e.github.io/JM_Service_Demo/).
2. Click **`EXECUTE_EVENT_FLOW()`** to watch a request travel through the system.
3. Under the **CHAOS MODE** panel, click any service (e.g., `PAYMENT_SVC`) to turn it **OFFLINE** (Red).
4. Re-run the event flow to see how the architecture handles the service failure (e.g., 503 Errors).

## Service Map

| Service | Responsibility | Database/Store |
| :--- | :--- | :--- |
| **Auth Service** | Authentication & Authorization | Redis |
| **Company Svc** | Profile Management | PostgreSQL |
| **Notify Svc** | Notifications (Email/SMS) | Redis |
| **Sub Svc** | Subscription Plans | PostgreSQL |
| **Payment Svc** | Transactions & Ledger | PostgreSQL |
| **Job Post Svc** | Job Creation & Management | MongoDB |
| **Match Svc** | Applicant Matching Engine | Pinecone (Vector) |
| **Search Svc** | Data Indexing & Search | Elasticsearch |
