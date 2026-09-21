AI-Driven Festival Notification & Workflow System
An automated, event-driven backend service designed to streamline festival-based marketing campaigns for Airbnb customers in India. The system leverages autonomous AI agents, secure authentication, and a human-in-the-loop approval workflow before triggering multi-channel notifications.

🏗️ System Architecture & Workflow
Authentication & Security (Master User Setup):

Upon sign-up, a unique Master User profile is initialized.

Authentication is handled via JWT (JSON Web Tokens) signed with a secure secret key, ensuring authorized access across all internal service requests.

Automated Festival Scheduling & Caching:

A scheduled background job runs at the beginning of every month to check for upcoming Indian festivals within a 15–23 day window.

Spring Caching (@Cacheable) is implemented to store static festival dates and query responses, optimizing performance and eliminating redundant external network calls.

Integrates with external providers (such as Google API/Calendar clients) via a clean interface-driven service pattern, designed for easy extension to alternative providers.

Event Streaming (Kafka Producer-Consumer):

Once a festival falling within the 10-day threshold is identified, an event is pushed to a Kafka Producer.

A dedicated Kafka Consumer picks up the event asynchronously to decouple heavy processing from the scheduling thread.

AI-Powered Content Generation & LangGraph Workflow:

Festival details and fixed Airbnb pricing/discount configurations are packaged and sent via synchronous REST templates to an AI Agent.

Built using LangGraph, the workflow incorporates a strict Human-in-the-Loop approval mechanism:

The AI agent uses customized system prompts to draft personalized marketing copy containing pre-stored pricing rules and discount schemes.

The generated draft is sent to the Master User via WhatsApp for review.

The workflow pauses execution state until explicit approval or decline is received from the Master User.

Multi-Channel Notification Dispatch:

Upon manual approval by the Master User, the system triggers the notification pipeline.

Supports multi-channel communication including SMS, Email, and WhatsApp.

Integrates with Evolution API (an open-source WhatsApp API) alongside Redis for state management, enabling high-throughput delivery of text content paired with promotional media and festival imagery directly to customers.

🛠️ Tech Stack & Core Concepts
Backend: Java, Spring Boot, Microservices, REST APIs, Kafka (Producer-Consumer)

Security & State: JWT Authentication, Redis

AI & Workflow: Python, LangGraph, LLM Agents, Prompt Engineering, LangGraph Human-in-the-Loop States

External APIs & Integrations: Evolution API (WhatsApp), Google Festival/Calendar APIs, Spring @Cacheable
