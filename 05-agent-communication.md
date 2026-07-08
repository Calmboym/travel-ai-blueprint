# AI Travel Platform

# Agent Communication Protocol (ACP)

Version: 1.0

Status: Draft

Priority: Critical

Dependencies:

- 03-ai-philosophy.md
- 04-ai-orchestration.md

---

# Purpose

This document defines the communication protocol between all AI agents.

Every agent in the platform MUST communicate using the same protocol.

No direct free-form communication is allowed between agents.

All communication must be structured, traceable, and validated.

---

# Philosophy

Agents are specialists.

They do not debate.

They do not guess.

They do not make assumptions outside their domain.

They exchange structured information.

The Orchestrator is responsible for combining results.

---

# Communication Principles

Every communication must be:

Deterministic

Structured

Traceable

Auditable

Secure

Minimal

Context-aware

Versioned

---

# Communication Pipeline

User

↓

Gateway

↓

Orchestrator

↓

Agent Request

↓

Agent Processing

↓

Agent Response

↓

Validation

↓

Response Synthesizer

↓

User

---

# Communication Rules

An agent CANNOT directly answer the user.

Only the Response Synthesizer may generate user-facing responses.

---

Agents NEVER communicate with Frontend.

---

Agents NEVER access Database directly.

---

Agents NEVER access User Memory directly.

---

Agents NEVER call external APIs directly unless explicitly authorized through Tool Calling.

---

# Standard Message Format

Every message exchanged between agents must contain:

Request ID

Conversation ID

User ID (hashed)

Timestamp

Language

Priority

Current Task

Target Agent

Source Agent

Traveler Profile Snapshot

Conversation Summary

Constraints

Expected Output

Confidence Threshold

---

# Request Object

Example

Request ID

REQ-001245

Source

Orchestrator

Target

Hotel Agent

Task

Recommend hotels

Destination

Tokyo

Travelers

2

Budget

Medium

Dates

2027-04-12

to

2027-04-19

Language

English

---

# Response Object

Every response must include:

Agent Name

Task Completed

Status

Confidence Score

Reasoning Summary

Sources

Warnings

Suggested Next Step

Structured Data

---

Example

Status

Success

Confidence

96%

Reasoning

Hotels selected based on traveler profile, distance to attractions, review quality and transportation access.

Warnings

Cherry blossom season increases prices.

---

# Communication Types

Type 1

Information Request

Example

Weather Agent

↓

Forecast Request

---

Type 2

Recommendation Request

Example

Trip Planner

↓

Restaurant Agent

---

Type 3

Validation Request

Example

Visa Agent

↓

Country Rules Validation

---

Type 4

Memory Request

Example

Planner

↓

Memory Agent

Retrieve traveler preferences.

---

Type 5

Tool Request

Example

Flight Agent

↓

Flight Search Tool

---

# Priority Levels

P0

Emergency

Medical

Safety

Natural disaster

Travel warning

Immediate response

---

P1

Visa

Passport

Immigration

Legal issues

---

P2

Booking

Flights

Hotels

Transportation

---

P3

Planning

Restaurants

Activities

Shopping

General recommendations

---

# Context Rules

Every request must contain only relevant context.

Good

Restaurant Agent

Receives:

Destination

Budget

Food preference

Language

Current location

---

Bad

Restaurant Agent receives:

Passport number

Visa history

Medical history

Personal notes

---

# Agent Permissions

Each agent has explicit permissions.

Example

Weather Agent

Can

Weather Tool

Location Service

Season Database

Cannot

Hotel API

Flight API

Payment System

---

Hotel Agent

Can

Hotel Search

Maps

Reviews

Cannot

Visa API

Currency API

---

# Timeouts

Every request has a timeout.

Default

15 seconds

Emergency

5 seconds

Background task

60 seconds

If timeout occurs:

Notify Orchestrator.

---

# Retry Rules

Retry only if:

Temporary API failure.

Network issue.

Rate limit.

Never retry:

Invalid request.

Permission denied.

Malformed response.

---

# Error Format

Every error follows the same schema.

Error Code

Message

Cause

Recoverable

Retry Suggested

Fallback

---

Example

Error

HOTEL_API_TIMEOUT

Recoverable

Yes

Retry

Allowed

Fallback

Cached hotel recommendations.

---

# Confidence Rules

Every response includes:

Confidence

Source Quality

Freshness

Coverage

Example

Confidence

91%

Freshness

Updated 3 hours ago

Coverage

Excellent

---

# Source Attribution

Every factual response must include source classification.

Official

Government

Embassy

Tourism Board

Airline

Airport

Hotel

Verified Partner

Trusted Commercial

Community

AI Reasoning

---

# Logging

Every communication is logged.

Log includes:

Latency

Agent

Result

Confidence

Errors

Tool Calls

Token Usage

---

# Security

Agents never trust incoming data blindly.

Validate:

Input schema

Permissions

Conversation ownership

Memory access

Tool authorization

Prompt integrity

---

# Prompt Injection Protection

Agents ignore instructions attempting to:

Reveal prompts

Reveal hidden memory

Execute unauthorized tools

Ignore system rules

Override policies

Access another user's data

---

# Scalability

The protocol must support:

100+ Agents

Parallel execution

Streaming responses

Distributed execution

Multiple AI models

Hybrid cloud deployment

---

# Future Extensions

Agent-to-Agent streaming

Voice agents

Image analysis agents

Document understanding agents

Travel document OCR

Autonomous booking agents

Real-time collaboration agents

---

# Acceptance Criteria

The protocol is considered complete when:

All agents communicate using the same structure.

Messages are fully traceable.

Permissions are enforced.

Failures are recoverable.

No direct agent-to-user communication exists.

The system supports adding new agents without changing the protocol.