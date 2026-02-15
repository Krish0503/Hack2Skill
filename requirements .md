# AI Personalized Learning Path Generator - Requirements

## 1. Project Overview

An intelligent learning system that creates customized educational roadmaps using LLMs and ML algorithms. Features include adaptive learning paths, progress tracking, and an agentic AI chatbot mentor with tool-calling capabilities.

**Target Users**: Career changers, students, professionals upskilling, self-learners

**Core Value**: Personalized learning paths with adaptive content and AI mentorship

## 2. Objectives & Success Metrics

**Primary Goals**: Personalization, adaptability, intuitive interface, agentic AI, progress tracking

**Key Metrics**: >95% roadmap completion, >4.0/5.0 satisfaction, <10s generation time, <2s chatbot response, >99.5% uptime, >60% 30-day retention

## 3. Functional Requirements Summary

### Core Features
- **Authentication**: Email/password registration, secure login, password reset, 7-day session timeout
- **User Profiling**: Career goals, study time, timeline specification
- **Roadmap Generation**: LLM-based personalized paths with 4-6 phases, 3-5 milestones per phase, daily task breakdown, resource recommendations, <10s generation
- **Progress Tracking**: Task status (not started/in progress/completed), timestamps, completion percentages, study streaks, notes
- **AI Chatbot**: Context-aware conversations with tool-calling (get_user_profile, get_current_roadmap, update_roadmap, update_progress), <2s response time
- **Dashboard**: Progress visualization, calendar view, weekly trends, overdue task highlights


## 4. Non-Functional Requirements

**Performance**: <10s roadmap generation (95%), <500ms API response (cached), <2s chatbot (90%), <1s dashboard load, 100+ concurrent users, <100ms DB queries (95%)

**Reliability**: 99.5% uptime, auto-failover, daily backups, <5min recovery, comprehensive error logging

**Usability**: Intuitive UI, clear error messages, responsive design (desktop/tablet/mobile), consistent UX, tooltips, keyboard navigation

**Maintainability**: Standard coding conventions, modular architecture, API documentation, structured logging, version control, 70%+ test coverage

**Compatibility**: Modern browsers (2-year window), PostgreSQL 12+, Python 3.9+, RESTful APIs (OpenAPI 3.0)

## 5. Technology Stack

#### 🎨 Frontend Layer
- React.js
- Amazon S3 (Static Website Hosting)
- Amazon CloudFront (Content Delivery Network)

#### ⚙️ Backend Layer
- Amazon API Gateway (REST API Management)
- AWS Lambda (Serverless Compute)
- Alternative (Container-based option):
  - Amazon ECS (Elastic Container Service)
  - AWS Fargate
  - AWS Elastic Beanstalk

#### 🗄 Database Layer
- Amazon Aurora PostgreSQL
- Amazon RDS for PostgreSQL

#### ⚡ Caching Layer
- Amazon ElastiCache for Redis

#### 🧵 Task Queue / Background Processing
- Amazon SQS (Simple Queue Service)
- AWS Lambda (Workers)
- AWS Step Functions (Workflow Orchestration)

#### 🤖 AI / ML Layer
- Amazon Bedrock (Access to Claude, Llama, Titan models)
- Amazon SageMaker (Model Training & Deployment)

#### 🔐 Authentication & Security
- Amazon Cognito (User Authentication & JWT Handling)
- AWS IAM (Identity and Access Management)
- AWS Secrets Manager

#### 💬 Real-Time Communication
- Amazon API Gateway WebSocket API
- AWS AppSync (GraphQL with Real-time Subscriptions)

#### 📊 Monitoring & Logging
- Amazon CloudWatch
- AWS X-Ray

#### 🌍 DevOps & Deployment
- AWS CodePipeline
- AWS CodeBuild
- AWS CodeDeploy

## 6. AI/ML Requirements

**LLM Integration**: OpenAI/Anthropic/open-source APIs, prompt templates, structured JSON parsing, fallback mechanisms, response caching (24h TTL), token monitoring, streaming support

**Progress Prediction**: Dropout probability, topic difficulty, completion time estimates using completion rate, study consistency, time efficiency

**Agentic Controller**: Tool selection/execution (get_user_profile, get_current_roadmap, update_roadmap, update_progress), JSON function parsing, parameter validation, error handling, context maintenance, safety guardrails

**Adaptive Algorithm**: Rule/ML-based roadmap adaptation considering completion velocity, time efficiency, applied at phase boundaries or weekly intervals

## 7. Database & API Requirements

**Schema**: Core tables (users, user_profiles, roadmaps, progress, chat_history, adaptation_events), UUID/auto-increment PKs, JSON/JSONB for roadmap data, timestamps, referential integrity

**Data Integrity**: NOT NULL, CHECK constraints (0-100 ranges), UNIQUE constraints, cascading deletes, transactions

**Performance**: Indexes on frequently queried columns, connection pooling (20-50), query optimization, pagination

**Backup**: Daily automated backups, 30-day retention, point-in-time recovery, quarterly restoration tests

**API Design**: RESTful (GET/POST/PUT/DELETE), JSON payloads, consistent naming (plural nouns, lowercase), standard HTTP status codes, versioned URLs (/api/v1/)

**Core Endpoints**: 
- Auth: register, login, logout, reset-password
- Profile: create, retrieve, update
- Roadmap: generate, retrieve, update, list by user
- Progress: update, retrieve summary, history
- Chat: message, history, clear session

**API Features**: Swagger/OpenAPI docs, rate limiting (100/min general, 20/min chat, 5/hr roadmap gen), 30s timeout, pagination (default 20, max 100), gzip compression (>1KB)

## 8. Security Requirements

**Authentication**: JWT (7-day expiration), bcrypt password hashing (12+ rounds), password complexity (8+ chars, upper/lower/number/special), rate limiting (5 attempts/15min), user authorization validation

**Data Protection**: HTTPS/TLS 1.3, encryption at rest, environment variables for secrets, SQL injection prevention, XSS protection, CSRF protection, log masking

**Privacy**: GDPR/CCPA compliance, data export, account deletion with purging, user consent, data anonymization

**API Security**: CORS whitelisting, payload schema validation, 10MB request limit, security event logging

**LLM Security**: Prompt injection sanitization, content filtering, spending limits, restricted tool-calling

## 9. Scalability Requirements

**Horizontal Scaling**: Stateless API design, multiple backend instances, external session storage (Redis), load balancer support

**Caching**: Redis for user profiles (1h TTL), roadmaps (30min), progress (5min), LLM responses (24h), cache-aside pattern, invalidation on updates

**Async Processing**: Celery task queue for roadmap generation, adaptive updates, email notifications, task status endpoints, retry with exponential backoff

**Database**: Read replicas, connection pooling, table partitioning (chat_history by date)

**Monitoring**: APM tracking (API response times, DB query performance, LLM latency, error rates, resource utilization), performance alerts, capacity planning logs

## 10. Future Enhancements

**Phase 2**: Multi-agent system with domain experts, skill gap detection from job descriptions, resume analyzer, GitHub integration, peer learning/study groups

**Phase 3**: Mobile apps (iOS/Android) with offline mode, gamification (points/badges/leaderboards), advanced analytics, learning platform integration (Coursera/Udemy/edX), video learning with note-taking

**Phase 4**: Multi-language support, voice interaction, VR learning environments, blockchain certification, AI-generated personalized content

## 11. Assumptions & Constraints

**Assumptions**: Reliable internet connectivity, basic computer literacy, LLM API availability, accurate user profiling input, English-speaking initial user base, access to learning resources, individual learners (not enterprise)

**Technical**: LLM API costs limit frequency, LLM response times (1-5s) impact responsiveness, token limits (128K) constrain context, chat history retention limited by storage costs, Python 3.9+ required, WebSocket support needed

**Business**: 8-12 week MVP timeline, $500/month infrastructure budget, 2-4 developer team, demonstrable prototype required

**Regulatory**: GDPR/CCPA compliance, regional data residency, terms of service and privacy policy required

**Operational**: Maintainable by 1-2 developers post-launch, minimal operational complexity, standard cloud platform deployment, CI/CD pipeline support

## 12. Success Criteria

**MVP**: Generate roadmaps for 3+ career goals, demonstrate adaptive learning, chatbot executes 4+ tool calls, real-time dashboard with charts, handle 10 concurrent users, complete end-to-end user journey

**User Acceptance**: 80% rate roadmap quality as good/excellent, 75% find chatbot helpful, 90% complete profiling without assistance, 10+ minute average session duration

**Technical**: 95% API responses meet SLA (<500ms cached), 99% uptime during testing, zero critical security vulnerabilities, 70%+ code coverage, 95% DB queries <100ms

---

**Document Version**: 1.0 | **Date**: 2026-02-14 | **Author**: System Architect