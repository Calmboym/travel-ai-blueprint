# AI Travel Platform

# External Services & API Registry

Document ID: INT-001

Version: 1.0

Status: Final

Priority: Critical

Dependencies

- AI/tool-calling-architecture.md
- Engineering/technology-stack.md

---

# Purpose

This document defines the approved external services, APIs, and third-party integrations used by the platform.

Only services listed in this document may be integrated into the MVP.

Any additional provider requires an Architecture Decision Record (ADR).

---

# Provider Selection Principles

Every provider must satisfy most of the following:

- Reliable global coverage
- Official API
- Commercial usage allowed
- Stable documentation
- Good uptime
- Long-term maintenance
- GDPR-friendly where applicable
- Clear pricing
- Supports production workloads

---

# Integration Categories

The platform integrates with:

- Maps & Geocoding
- Flights
- Hotels
- Places
- Weather
- Currency
- Visa & Travel Advisories
- Transportation
- Events
- Translation
- Time Zones
- Authentication
- Email
- Analytics
- Error Monitoring

---

# Maps & Geocoding

Primary

Google Maps Platform

Purpose

Maps

Directions

Geocoding

Places

Distance Matrix

Autocomplete

Street View

Fallback

OpenStreetMap

Nominatim

Routing Engine

OSRM

Notes

Design the abstraction layer so providers can be replaced without changing business logic.

---

# Flights

Architecture

Aggregator-based

Recommended Providers

Amadeus

Future Support

Skyscanner (subject to commercial approval)

Duffel

Kiwi

Purpose

Search only during MVP.

Booking will be introduced in a later phase.

---

# Hotels

Recommended Providers

Booking.com Connectivity APIs (future commercial partnership)

Expedia Group APIs

Hotelbeds

The system must support multiple hotel providers.

Results should be normalized into a common internal schema.

---

# Places & Attractions

Primary

Google Places API

Fallback

OpenStreetMap

Internal curated datasets

Supported Information

Museums

Landmarks

Restaurants

Parks

UNESCO Sites

Tourist attractions

Ratings

Opening hours

Photos

---

# Weather

Primary

OpenWeather

Fallback

National weather services where available

Future

Commercial weather providers for premium users

---

# Currency

Primary

European Central Bank reference rates

Fallback

ExchangeRate APIs

Currency data must always include:

Timestamp

Base currency

Conversion source

---

# Visa & Entry Requirements

Preferred Sources

Official government immigration websites

Official embassy websites

Official foreign affairs ministries

The AI must never invent visa rules.

If no official source exists:

Clearly communicate uncertainty.

---

# Transportation

Supported Categories

Metro

Bus

Train

Taxi

Ride-hailing

Airport transfer

Ferry

Future

Real-time transit APIs

---

# Translation

Primary

LLM translation

Fallback

Dedicated translation APIs

User interface translations must be independent from AI translation.

---

# Time Zones

IANA Time Zone Database

Mandatory

Never rely on manually maintained timezone tables.

---

# Authentication

Supported Providers

Google

Apple

GitHub

Email + Password

Future

Microsoft

Facebook

Passkeys

---

# Email

Transactional Email

Provider abstraction required.

Examples

Verification

Password reset

Trip sharing

Notifications

---

# Analytics

Privacy-first analytics.

Avoid collecting unnecessary personal data.

Examples

Product analytics

Search analytics

Conversation metrics

Feature adoption

---

# Error Monitoring

Centralized monitoring.

Capture

Backend exceptions

Frontend exceptions

API failures

Tool failures

Slow responses

---

# Feature Flags

Support gradual rollout.

Examples

New AI models

New providers

Experimental itinerary planner

New recommendation algorithms

---

# Integration Abstraction Layer

Every external provider must be wrapped by an internal adapter.

Business logic must never call provider SDKs directly.

Example

HotelService

↓

Booking Adapter

↓

Expedia Adapter

↓

Hotelbeds Adapter

The rest of the application communicates only with HotelService.

---

# Provider Health

Each provider must expose:

Health status

Latency

Rate limit usage

Error rate

Last successful request

Availability

---

# Fallback Strategy

Every critical integration requires:

Primary provider

Secondary provider

Graceful degradation

Cached response (where appropriate)

---

# Secrets Management

API keys must be stored securely.

Never commit credentials.

Never expose provider credentials to the client.

Rotate secrets regularly.

---

# Cost Management

Monitor:

API usage

Quota

Cost per request

Monthly budget

Unexpected spikes

The Orchestrator should minimize expensive API calls whenever possible.

---

# Future Integrations

Flight booking

Hotel booking

Insurance

Car rental

Visa application assistance

Airport lounges

SIM / eSIM

Local payment methods

Train ticket booking

Event ticket booking

Travel insurance comparison

---

# Acceptance Criteria

The integration layer is complete when:

Providers are abstracted.

Fallbacks exist.

Business logic is provider-independent.

Secrets are protected.

Critical services have monitoring.

Provider replacement requires minimal code changes.