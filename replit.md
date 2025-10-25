# Community Knowledge Bot

## Overview

Community Knowledge Bot is an AI-powered Q&A assistant that provides instant answers about community information, events, and products. Users can upload documents and FAQs to build a knowledge base, which the AI uses to answer questions through an intelligent chatbot interface. The application features a conversational chat interface with source attribution and a knowledge base management system.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React 18+ with TypeScript and Vite as the build tool

**Routing**: Wouter for lightweight client-side routing

**UI Component System**: 
- Shadcn/ui components with Radix UI primitives
- Tailwind CSS for styling with custom design system
- Design philosophy follows Material Design and Linear aesthetics for clarity and efficiency
- Custom CSS variables for theming (light/dark mode support)
- Typography system uses Inter for interface elements and JetBrains Mono for code

**State Management**:
- TanStack Query (React Query) for server state management
- Local React state for UI interactions
- Query invalidation pattern for data synchronization

**Key Pages**:
- Home: Landing page with hero image and call-to-action
- Chat: Main conversational interface with sidebar for conversation history
- Knowledge: Document management interface for uploading and managing knowledge base
- Not Found: 404 error page

**Component Structure**:
- Reusable UI components in `client/src/components/ui/`
- Feature-specific components (ChatMessage, ChatSidebar, KnowledgeDocCard, etc.)
- Empty state components for better UX

### Backend Architecture

**Runtime**: Node.js with Express.js

**Language**: TypeScript with ES modules

**API Design**: RESTful API with the following endpoints:
- `GET /api/knowledge` - Fetch all knowledge documents
- `POST /api/knowledge` - Create new knowledge document
- `DELETE /api/knowledge/:id` - Delete knowledge document
- `GET /api/conversations` - Fetch all conversations
- `POST /api/chat` - Send message and get AI response
- `GET /api/messages/:conversationId` - Fetch messages for a conversation

**Business Logic**:
- Document-based knowledge retrieval using simple text matching
- OpenAI GPT-5 integration for generating contextual answers
- Source attribution to link answers back to knowledge base documents
- Conversation management with automatic title generation

**Development Features**:
- Vite middleware integration for HMR in development
- Request/response logging middleware
- Error handling and validation with Zod schemas

### Data Storage

**Database**: PostgreSQL via Neon serverless driver

**ORM**: Drizzle ORM with type-safe schema definitions

**Schema Design**:
- `knowledge_docs`: Stores uploaded documents, FAQs, and text content
  - Fields: id, title, content, type, fileSize, createdAt
  - Types supported: 'document', 'faq', 'text'
  
- `conversations`: Chat conversation threads
  - Fields: id, title (auto-generated), createdAt
  - Supports multiple concurrent conversations
  
- `messages`: Individual chat messages
  - Fields: id, conversationId, content, role, sources, createdAt
  - Roles: 'user' or 'assistant'
  - Sources array links to knowledge document IDs

**Migration Strategy**: Drizzle Kit for schema migrations with `db:push` command

**Connection Management**: Connection pooling via Neon's serverless WebSocket support

### External Dependencies

**AI Service**: OpenAI API
- Model: GPT-5 (latest as of August 2025)
- Usage: Question answering with context from knowledge base
- Fallback: Graceful error handling when API key not configured
- System prompt ensures answers stay grounded in provided documents

**Database Service**: Neon Serverless PostgreSQL
- WebSocket-based connection for serverless compatibility
- Environment variable: `DATABASE_URL`
- Automatic connection pooling

**Third-Party UI Libraries**:
- Radix UI: Accessible component primitives (dialogs, dropdowns, tooltips, etc.)
- Embla Carousel: Carousel functionality
- date-fns: Date formatting and manipulation
- Lucide React: Icon library
- cmdk: Command palette component

**Styling Dependencies**:
- Tailwind CSS: Utility-first CSS framework
- class-variance-authority: Component variant management
- tailwind-merge & clsx: Class name utilities

**Form Handling**:
- React Hook Form: Form state management
- Zod: Schema validation
- @hookform/resolvers: Integration between React Hook Form and Zod

**Development Tools**:
- Replit-specific plugins for dev banner, cartographer, and runtime error overlay
- ESBuild for production builds
- TSX for TypeScript execution in development

**Typography**: Google Fonts (Inter and JetBrains Mono) loaded via CDN

**Session Management**: Potential for connect-pg-simple PostgreSQL session store (dependency present but not actively used in codebase)