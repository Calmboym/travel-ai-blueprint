# AI Travel Platform

# Approved Technology Stack

Version: 1.0

Status: Draft

Priority: Critical

---

# Purpose

This document defines the ONLY approved technology stack for the project.

Claude (or any implementation AI) MUST NOT replace technologies unless explicitly approved.

Architectural consistency is more important than personal preference.

---

# Guiding Principles

Technology choices prioritize:

- Long-term maintainability
- Strong ecosystem
- Excellent documentation
- Scalability
- Performance
- AI integration
- Developer experience
- Open standards
- Community adoption

---

# Frontend

Framework

Next.js (App Router)

Reason

- Excellent SEO
- Server Components
- Streaming support
- Internationalization
- Mature ecosystem

---

Language

TypeScript

Mandatory.

JavaScript is NOT allowed.

---

Styling

Tailwind CSS

Reason

Utility-first

Excellent scalability

Large ecosystem

---

UI Components

shadcn/ui

Reason

Accessible

Customizable

No vendor lock-in

---

Icons

Lucide

---

Animations

Framer Motion

Used only where meaningful.

Avoid unnecessary animations.

---

Forms

React Hook Form

Validation

Zod

---

State Management

Server State

TanStack Query

Client State

Zustand

Avoid Redux unless future complexity requires it.

---

Internationalization

next-intl

Must support:

RTL

LTR

Locale switching

---

Maps

Primary

Google Maps

Secondary

OpenStreetMap

Architecture must allow provider switching.

---

# Backend

Language

Python

Mandatory.

---

Framework

FastAPI

Reason

Async

Performance

OpenAPI

Type safety

Excellent AI ecosystem

---

Validation

Pydantic

---

ORM

SQLAlchemy 2.x

---

Migrations

Alembic

---

Authentication

JWT

OAuth2

Google Login

Apple Login

GitHub Login

Future providers must be pluggable.

---

Background Jobs

Celery

Broker

Redis

---

API Style

REST first.

GraphQL may be added later.

---

# Database

Primary Database

PostgreSQL

Mandatory.

---

Caching

Redis

Mandatory.

---

Vector Search

Qdrant

Reason

Fast

Scalable

AI-native

Replaceable via abstraction layer.

---

Blob Storage

Cloud storage provider

Never store user files inside database.

---

# AI Layer

Provider Abstraction

Mandatory.

Never couple business logic to one LLM.

Supported Providers

OpenAI

Anthropic

Google Gemini

Future local models

---

Prompt Management

Centralized prompt registry.

No hardcoded prompts.

---

Embeddings

Provider abstraction.

Not tied to one vendor.

---

Memory

Separate service.

Not embedded inside conversation logic.

---

RAG

Hybrid search

Vector + Metadata + Keyword

---

# DevOps

Containerization

Docker

Mandatory.

---

Reverse Proxy

Traefik or NGINX

Decision deferred until deployment phase.

---

CI/CD

GitHub Actions

---

Infrastructure as Code

Future phase.

---

# Observability

Logging

Structured JSON logs.

---

Monitoring

OpenTelemetry

---

Error Tracking

Sentry

---

Metrics

Prometheus compatible.

---

# Security

Secrets

Environment variables only.

Never hardcode secrets.

---

HTTPS

Mandatory.

---

Rate Limiting

Mandatory.

---

Input Validation

Mandatory for every endpoint.

---

# Testing

Unit Tests

Mandatory.

---

Integration Tests

Mandatory.

---

End-to-End Tests

Playwright

---

# Coding Standards

Backend

PEP 8

Strict typing

---

Frontend

ESLint

Prettier

Strict TypeScript

---

# Performance Targets

First Contentful Paint

< 2 seconds

---

Largest Contentful Paint

< 2.5 seconds

---

API Average Response

< 300 ms (excluding AI generation)

---

# Forbidden Technologies

The following technologies are NOT allowed without architectural approval:

- jQuery
- Plain JavaScript (frontend)
- Flask
- Django
- MongoDB (primary database)
- Redux (initial MVP)
- Hardcoded SQL
- Inline CSS
- Hardcoded prompts
- Business logic inside React components

---

# Future Review

This document must be reviewed before every major release.

Technology changes require an Architecture Decision Record (ADR).

No implementation may deviate from this document without an approved ADR.