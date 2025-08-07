# Overview

This is an educational RSA cryptography application that provides an interactive platform for learning and experimenting with RSA encryption. The application features RSA key generation, message encryption/decryption with step-by-step mathematical visualizations, educational tools for understanding cryptographic concepts, and real-time encrypted messaging capabilities. It's designed to bridge the gap between theoretical cryptography education and practical implementation.

# User Preferences

Preferred communication style: Simple, everyday language.

# System Architecture

## Frontend Architecture
The frontend is built with React and TypeScript using Vite as the build tool. The application follows a component-based architecture with a clear separation of concerns:

- **UI Framework**: React with TypeScript for type safety and better developer experience
- **Styling**: Tailwind CSS with shadcn/ui components for consistent design system
- **State Management**: React Query (@tanstack/react-query) for server state management and local React state for UI state
- **Routing**: Wouter for lightweight client-side routing
- **Form Handling**: React Hook Form with Zod validation for type-safe form validation

The application uses a tabbed interface design with distinct sections for key generation, encryption/decryption, educational tools, and secure chat. Components are organized into feature-based modules with reusable UI components from the shadcn/ui library.

## Backend Architecture
The backend follows a Node.js Express server architecture with TypeScript:

- **Server Framework**: Express.js with TypeScript for API endpoints and middleware
- **WebSocket Support**: Native WebSocket implementation for real-time chat functionality
- **Session Management**: Express sessions with PostgreSQL storage for authentication state
- **Authentication**: Dual authentication system supporting both Replit OAuth and manual email/password authentication
- **API Design**: RESTful endpoints for user management and HTTP upgrade to WebSocket for real-time features

The server implements a storage abstraction layer that separates business logic from database operations, making it easier to test and maintain.

## Data Storage
The application uses PostgreSQL as the primary database with Drizzle ORM for type-safe database operations:

- **Database**: PostgreSQL (configured for Neon serverless in production)
- **ORM**: Drizzle ORM with schema-first approach for type safety
- **Migrations**: Drizzle Kit for database schema management
- **Connection**: Connection pooling using Neon serverless driver for scalability

The database schema includes tables for users, chat rooms, messages, RSA keys, and session storage. The design supports both authenticated user sessions and RSA key persistence.

## Authentication and Authorization
The application implements a flexible authentication system that supports multiple authentication methods:

- **OAuth Integration**: Replit OAuth using OpenID Connect for seamless integration within the Replit environment
- **Manual Authentication**: Email/password authentication with bcrypt for password hashing
- **Session Management**: Server-side session storage in PostgreSQL with secure cookie configuration
- **Authorization**: Middleware-based route protection with user context injection

The authentication system gracefully handles both authenticated and unauthenticated states, allowing users to use educational features without authentication while requiring login for chat functionality.

## Real-time Communication
WebSocket implementation provides real-time chat capabilities with RSA encryption:

- **Protocol**: Native WebSocket with custom message protocol
- **Message Types**: Support for room joining/leaving, chat messages, and user presence
- **Encryption**: Client-side RSA encryption of messages using user-generated keys
- **Connection Management**: Automatic reconnection logic and connection state management

The WebSocket server maintains user sessions and room memberships, enabling features like user presence indicators and message broadcasting within chat rooms.

# External Dependencies

## Database Services
- **Neon Database**: Serverless PostgreSQL hosting with connection pooling
- **Environment Configuration**: Requires DATABASE_URL environment variable for database connection

## Authentication Services
- **Replit OAuth**: OpenID Connect integration for Replit-based authentication
- **Session Secret**: Requires SESSION_SECRET environment variable for session encryption

## Development Tools
- **Vite**: Frontend build tool with React plugin and development server
- **ESBuild**: Backend bundling for production deployment
- **TypeScript**: Type checking and compilation for both frontend and backend

## UI and Styling
- **Radix UI**: Headless UI components for accessibility and customization
- **Tailwind CSS**: Utility-first CSS framework for styling
- **Lucide React**: Icon library for consistent iconography

## Cryptography Libraries
- **Custom RSA Implementation**: Educational RSA implementation for demonstration purposes (not suitable for production cryptography)
- **bcrypt**: Password hashing for manual authentication

## WebSocket Implementation
- **Native WebSocket**: Browser WebSocket API for client-side real-time communication
- **ws**: Node.js WebSocket library for server-side WebSocket handling

The application is designed to run in both development and production environments with appropriate configuration for each. The Replit-specific features are conditionally loaded based on environment detection.