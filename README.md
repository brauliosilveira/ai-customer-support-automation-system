# AI Customer Support Automation System

A multi-agent customer support and lead-handling system built on top of a customized Chatwoot deployment, designed to automate intake, qualification, routing, FAQ resolution, and meeting scheduling across WhatsApp conversations.

This repository is presented as a public portfolio case study for recruiters, hiring managers, and founders evaluating senior full-stack product work. It highlights the system architecture, agent orchestration strategy, support automation workflows, and infrastructure decisions behind the project while keeping the full source code private for commercial and security reasons.

## Executive Summary

This project was built to automate one of the most operationally expensive parts of business communication: handling inbound WhatsApp conversations from both existing customers and campaign-generated leads.

The system combined:

- a customized Chatwoot instance as the support interface;
- WhatsApp connectivity through Evolution API;
- multi-agent orchestration through n8n;
- OpenAI-powered decision-making using `gpt-4o-mini`;
- PostgreSQL and Redis in the messaging stack;
- Supabase for user management and vector-based FAQ retrieval;
- Google Calendar and Google Meet integration for appointment scheduling.

The goal was not just to respond automatically, but to route each conversation into the right business workflow:

- customer support and department handoff;
- campaign lead qualification;
- meeting booking;
- FAQ resolution through knowledge retrieval.

The result was an AI-enabled support and sales-assistance system that connected conversation intake, triage, routing, scheduling, and knowledge access inside one operational flow.

## Why This Project Matters

Many businesses do not need "just a chatbot." They need a system that can:

- understand who is starting the conversation;
- distinguish customers from campaign-generated leads;
- decide what operational path should happen next;
- route the conversation to the correct person, team, or automation branch;
- answer common questions from a knowledge base;
- book meetings without human back-and-forth.

This project was built to solve exactly that.

Instead of a single prompt-based assistant, the system used a multi-agent approach with specialized responsibilities and explicit routing logic.

## What I Built

- A customized Chatwoot-based support operation with kanban workflow adaptations
- WhatsApp conversation handling through Evolution API
- A multi-agent orchestration flow built in n8n
- OpenAI-powered intent analysis and routing
- Lead qualification automation for campaign traffic
- Customer-intake routing for support and operational requests
- Meeting scheduling through Google Calendar and Google Meet
- FAQ resolution using vector search on Supabase
- Knowledge ingestion from Google Docs stored in Google Drive
- Human handoff logic for sector- or person-based routing
- Infrastructure deployment on a VPS using Portainer, PostgreSQL, and Redis

## Multi-Agent Design

This project was designed as a true multi-agent system, with each agent handling a focused part of the workflow.

### 1. Main agent

The main agent was responsible for understanding the conversation at intake and deciding which downstream agent should take over.

Its role was orchestration, not deep task execution.

### 2. SDR agent

The SDR agent handled leads coming from campaigns.

Its objective was to:

- qualify the lead;
- follow meeting-booking criteria;
- move the lead toward scheduling;
- trigger the appropriate scheduling flow when ready.

### 3. Reception agent

The reception agent handled inbound conversations from existing customers or operational inquiries.

Its job was to identify the request and route the conversation in a humanized way to the correct person or department.

### 4. Scheduling agent

The scheduling agent handled appointment logistics, including:

- in-person meetings;
- Google Meet meetings;
- calendar slot coordination;
- meeting-link generation.

### 5. FAQ agent

The FAQ agent queried a vector knowledge base stored with Supabase and answered recurring questions using content sourced from Google Docs.

This allowed the system to give grounded answers rather than relying only on generic model responses.

## Core Workflows

### Customer vs. lead identification

One of the most important parts of the system was distinguishing whether the inbound conversation came from:

- an existing customer;
- or a lead generated through campaigns.

That distinction changed the entire downstream logic.

If the user was a customer, the system attempted to identify the correct destination person or sector based on the request and client-specific context.

If the user was a campaign lead, the system moved into SDR-style qualification and scheduling behavior.

### Support routing

For customer conversations, the system used business-specific logic to determine where the conversation should go next.

This made the AI layer operationally useful rather than merely conversational.

### Lead qualification and scheduling

For campaign leads, the system could qualify intent and move directly into scheduling, integrating with Google Calendar and generating Google Meet links when required.

### FAQ retrieval

For repeated questions, the system could consult a Supabase-backed vector knowledge base populated from Google Docs stored in Drive.

This made the assistant more grounded and more maintainable for ongoing knowledge updates.

## Technical Architecture

At a high level, the platform combined a conversation layer, an orchestration layer, an AI layer, and an infrastructure layer.

### Conversation layer

- Chatwoot
- customized support UI with kanban workflow adaptations
- WhatsApp channel through Evolution API

### Orchestration layer

- n8n workflows coordinating multi-agent logic
- task-specific branching based on conversation classification
- integrations with calendar and knowledge components

### AI layer

- OpenAI API
- `gpt-4o-mini`
- agent specialization by workflow responsibility

### Data and support systems

- PostgreSQL
- Redis
- Supabase for user management
- Supabase vector storage for FAQ retrieval
- Google Docs and Drive as editable knowledge sources

### Scheduling and meeting integrations

- Google Calendar
- Google Meet link creation

### Deployment layer

- VPS deployment
- Portainer-based container management

## Technical Flow

### 1. Inbound conversation arrives via WhatsApp

The user starts a conversation through WhatsApp, which is connected to the system through Evolution API and surfaced inside the customized Chatwoot environment.

### 2. Intake classification

The main agent analyzes the message and determines whether the conversation should be routed to:

- SDR logic;
- reception/routing logic;
- FAQ retrieval logic;
- or scheduling logic.

### 3. Specialized agent execution

The selected agent takes over the workflow based on the conversation type and operational objective.

### 4. Business action

Depending on the route, the system may:

- direct the user to the correct team or person;
- answer a recurring question from the knowledge base;
- qualify a lead;
- schedule a meeting;
- generate a Google Meet link.

### 5. Human handoff or resolution

The conversation ends either with resolution by automation or with a structured handoff to a human team member.

## Key Engineering Decisions

### Use a multi-agent model instead of a single general-purpose assistant

This made the system easier to reason about operationally. Each agent had a clear responsibility instead of forcing one assistant to do everything poorly.

### Keep the support interface inside a proven open-source platform

Using Chatwoot as the conversation layer allowed the system to leverage an existing support environment while customizing workflow behavior where needed.

### Separate orchestration from the communication UI

The Chatwoot layer handled conversation management, while n8n handled flow orchestration and agent branching. This kept responsibilities clearer and made the system more modular.

### Ground FAQ responses in retrieved content

Using Supabase vector retrieval and Google Docs as source material reduced hallucination risk and made knowledge updates much easier for non-developers.

### Automate business outcomes, not just responses

The real value of the system was not automatic messaging alone. It was the ability to route, qualify, schedule, and operationalize conversations.

## Historical Context

This project is no longer fully live in its original automated form. Today, I build AI agents directly in code rather than using n8n as the orchestration layer.

That said, this project still has strong portfolio value because it demonstrates:

- real-world multi-agent design;
- support automation architecture;
- business-process orchestration;
- AI-assisted lead handling;
- retrieval-based FAQ workflows;
- pragmatic deployment and infrastructure decisions.

The Chatwoot + kanban portion remains an important part of the system history and product evolution.

## Why This Project Matters

This project demonstrates:

- full-stack product thinking across support UX, orchestration, AI, and infrastructure;
- practical multi-agent system design;
- operational automation for customer support and sales intake;
- AI routing tied to business workflows rather than generic chat behavior;
- knowledge-retrieval integration for grounded answers;
- real scheduling automation tied to lead conversion;
- infrastructure ownership across VPS, containers, databases, and support tooling.

It also shows a practical business skill: turning inbound messaging into a structured, automatable operating system for support and revenue workflows.

## Stack

- Chatwoot
- Evolution API
- n8n
- OpenAI API
- `gpt-4o-mini`
- PostgreSQL
- Redis
- Supabase
- Supabase vector database / retrieval workflows
- Google Drive
- Google Docs
- Google Calendar
- Google Meet
- VPS deployment
- Portainer

## High-Level Architecture

```text
WhatsApp Conversations
        |
        v
 Evolution API
        |
        v
 Customized Chatwoot
        |
        v
 n8n Orchestration Layer
        |
        +--> Main Agent
        +--> SDR Agent
        +--> Reception Agent
        +--> Scheduling Agent
        +--> FAQ Agent
        |
        +--> OpenAI gpt-4o-mini
        +--> Supabase user and vector data
        +--> Google Calendar / Meet
        +--> Google Docs knowledge source
        |
        v
 Human Handoff or Automated Resolution
```

## Demo and Media

This case study is best supported by screenshots showing the conversation layer, routing logic, and scheduling/FAQ outcomes.

- `Chatwoot Workspace - Customized Support Operations`
- `Kanban View - Conversation Flow Management`
- `Multi-Agent Routing - Intake and Handoff Logic`
- `Lead Qualification - SDR Automation Flow`
- `FAQ Retrieval - Knowledge-Based Answers`
- `Scheduling Flow - Google Calendar and Meet Integration`

## About This Repository

This is a public portfolio case study for full-stack, AI automation, support systems, orchestration, and SaaS-focused roles.

The complete source code, internal integrations, secrets, and infrastructure details remain private for commercial and security reasons.

## My Role

I designed and implemented the automation system behind the project, including:

- multi-agent workflow design;
- support and lead-routing logic;
- AI orchestration through n8n;
- FAQ retrieval design with vector search;
- scheduling automation;
- infrastructure deployment and system integration;
- product customization on top of Chatwoot.

## Contact

If you would like a live walkthrough or want to discuss AI support systems, multi-agent orchestration, automation architecture, or full-stack roles, feel free to reach out.
