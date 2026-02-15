# AI Learning Path Generator - Design

## 1. Architecture

Multi-layered system with Frontend (React), Backend (AWS Lambda/API Gateway), AI/ML Layer (Amazon Bedrock + adaptive algorithms), and Database (Amazon Aurora PostgreSQL).

**Goals**: Personalization, adaptability, scalability, modularity, agentic AI, intuitive UX

## 2. Technology Stack

### ☁️ AWS-Based Technology Stack

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

## 3. Core Components

**Frontend**: Auth, profiling wizard, roadmap dashboard, progress tracking, chatbot UI
**Backend**: API gateway, auth middleware, business logic, WebSocket for chat
**AI/ML**: LLM orchestration, prompt templates, tool-calling, adaptive algorithms
**Database**: PostgreSQL for user profiles, roadmaps, progress, chat history
**Agent Controller**: Decision engine, tool registry, context management, function call parser

## 4. Key Modules

**User Profiling**: Goal parsing, time calculator, learning style analyzer
**Roadmap Generation**: LLM prompt constructor, roadmap parser, resource recommender, timeline optimizer
**Progress Tracking**: Task completion tracker, velocity calculator, visualization
**Adaptive Learning**: Performance evaluator, difficulty adjuster, timeline recalculator
**Chatbot**: Conversation manager, intent classifier, tool executor (get_progress, update_roadmap, get_tasks, search_resources, schedule_task, explain_concept)

## 5. Data Flows

**Roadmap Generation**: User input → Profile creation → LLM prompt → Roadmap parsing → Database storage → UI display
**Adaptive Update**: Progress analysis → Performance evaluation → Decision rules → Roadmap modification → User notification
**Chatbot**: User message → Context prep → LLM processing → Tool execution → Response generation → Display

## 6. AI Design

**LLM Models**: GPT-4/Claude for roadmap generation, GPT-3.5/Claude Sonnet for chatbot
**Prompting**: System prompts with user context, structured output requirements
**Tool-Calling**: Function definitions with parameter validation, error handling
**Adaptation Rules**: Progress-based thresholds (high velocity accelerate, low velocity adjust, moderate maintain)

## 7. Database Schema

**users**: user_id, email, password_hash, full_name, created_at, last_login, is_active
**user_profiles**: profile_id, user_id, learning_goal, hours_per_day, target_completion_months
**roadmaps**: roadmap_id, user_id, version, roadmap_data (JSONB), status, created_at, is_current
**progress**: progress_id, user_id, roadmap_id, task_id, status, started_at, completed_at, time_spent_hours
**chat_history**: message_id, user_id, session_id, role, content, tool_calls (JSONB), timestamp
**adaptation_events**: event_id, user_id, roadmap_id, trigger_type, trigger_data (JSONB), modifications (JSONB)

## 8. API Endpoints

**Auth**: POST /api/auth/register, POST /api/auth/login
**Profile**: POST /api/profile, GET /api/profile/{user_id}
**Roadmap**: POST /api/roadmap/generate, GET /api/roadmap/{roadmap_id}, PUT /api/roadmap/{roadmap_id}
**Progress**: POST /api/progress/update, GET /api/progress/{user_id}
**Chat**: POST /api/chat/message, GET /api/chat/history/{session_id}

## 9. Performance & Security

**Caching**: Redis for profiles (1hr), roadmaps (30min), progress (5min), LLM responses (24hr)
**Async Processing**: Celery for roadmap generation, adaptive updates, batch operations
**Database**: Indexes on user_id, roadmap_id, session_id; JSONB indexing; connection pooling
**Auth**: JWT tokens (7-day expiry), bcrypt password hashing, rate limiting (100 req/min)
**Security**: TLS 1.3, input validation, CORS, API key management, RBAC (User/Admin/Mentor roles)

## 10. Future Enhancements

**Multi-Agent System**: Specialist agents (Python expert, ML specialist, career advisor) with coordinator
**Resume Analyzer**: Extract skills from resumes, auto-populate profiles
**GitHub Integration**: Analyze repos/commits to assess coding skills
**Community Features**: Peer matching, study groups, forums, collaborative projects
**Advanced Analytics**: Learning velocity trends, predictive completion, comparative benchmarking
**Mobile App**: iOS/Android with offline access, push notifications, voice chatbot
**Integrations**: LeetCode, Google Calendar, Notion
**Gamification**: Points, badges, levels, challenges, leaderboards
**Content Generation**: Auto-generate exercises, explanations, code examples, project ideas
