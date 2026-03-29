# NoBrainer

NoBrainer is a real-time collaborative brainstorming platform that enables teams to brainstorm, organize, and upvote ideas effortlessly. Built from scratch with Elixir and Phoenix LiveView for blazing-fast performance and seamless WebSocket-based updates.

## Features

- **Quick Setup**: Get started in under 5 minutes
- **Real-time Collaboration**: Live updates as team members contribute and upvote ideas
- **Anonymous Participation**: No registration required - invite participants with just a link
- **Idea Clustering**: Organize ideas with custom labels and tags
- **Lane Organization**: Drag-and-drop Kanban-style lanes for prioritization
- **File Attachments**: Secure, encrypted file uploads to S3-compatible storage
- **AI-Powered Ideas**: Generate ideas using OpenAI-compatible LLM APIs
- **Link Previews**: Automatic previews for shared URLs
- **Comments**: Threaded discussions on individual ideas
- **Export Options**: Export brainstorming data to HTML or CSV
- **Internationalization**: German, English, and Italian language support
- **GDPR Compliant**: Automatic data cleanup after 30 days

## Use Cases

- Brainstorming new business initiatives
- Problem-solving sessions
- Team ideation workshops
- Quick decision-making polls

## Tech Stack

- **Language**: Elixir 1.17
- **Framework**: Phoenix 1.7.21 with LiveView
- **Real-time**: Phoenix Channels with WebSocket
- **Database**: PostgreSQL with Ecto
- **Storage**: S3-compatible object storage with Vault encryption
- **AI Integration**: OpenAI and OpenAI-compatible APIs
- **Deployment**: Docker & Docker Compose
- **Testing**: ExUnit with FactoryBot

## Architecture

The application follows a clean separation of concerns:

```
lib/
├── NoBrainer/              # Core business logic (contexts)
│   ├── brainstormings.ex        # Brainstorming session management
│   ├── ideas.ex                 # Idea CRUD and positioning
│   ├── lanes.ex                 # Kanban lane organization
│   ├── accounts.ex              # User management
│   ├── comments.ex              # Idea discussions
│   ├── attachments.ex           # File handling with encryption
│   └── services/                # S3 storage, vault encryption
├── NoBrainer_web/          # Web layer
│   ├── router.ex                # Route definitions
│   ├── live/                    # LiveView components
│   └── controllers/             # HTTP controllers
```

## Getting Started

### Prerequisites

- Elixir 1.17+
- Phoenix Framework 1.7+
- PostgreSQL 14+
- Docker & Docker Compose

### Development Setup

```bash
# Start Docker Compose
docker compose up --build -d

# Setup database
docker compose exec app mix ecto.setup

# Start the server
docker compose exec app mix phx.server

# Access at http://localhost:4000
```

### Running Tests

```bash
docker compose exec app mix test
```

### Code Quality

```bash
# Format code
mix format

# Run linter
mix credo

# Check formatting
mix format --check-formatted
```

## Environment Variables

Key configuration options:

- `DATABASE_URL` - PostgreSQL connection string
- `MW_FEATURE_BRAINSTORMING_REMOVAL_AFTER_DAYS` - Auto-delete old brainstorms (default: 30)
- `MW_FEATURE_IDEA_FILE_UPLOAD` - Enable/disable file uploads
- `OBJECT_STORAGE_*` - S3-compatible storage configuration
- `VAULT_ENCRYPTION_KEY_BASE64` - Encryption key for file storage
- `MW_AI_ENABLED` - Enable AI-powered idea generation
- `MW_AI_API_KEY` - OpenAI API key
- `MW_DEFAULT_LOCALE` - Default language (en/de/it)

## Feature Highlights

### Real-time Updates

Phoenix LiveView provides sub-second updates across all connected clients. When someone adds or upvotes an idea, everyone sees it instantly without page refreshes.

### AI Integration

Leverage large language models to generate initial ideas based on your brainstorming topic:

```env
MW_AI_ENABLED=true
MW_AI_API_KEY=your-api-key
MW_AI_API_MODEL=gpt-4o-mini
```

### Secure File Storage

Files are encrypted client-side before upload using AES-256-GCM, ensuring data privacy even from cloud storage administrators.

### GDPR Compliance

Automatic cleanup jobs remove brainstorming sessions older than the configured retention period, reducing compliance burden.

## Production Deployment

```bash
# Copy environment template
cp .env.prod.default .env.prod

# Configure your production settings
# Edit .env.prod with database, SSL, and storage settings

# Start production services
docker compose --file docker-compose-prod.yml --env-file .env.prod up -d --build
```

## License

MIT License - see [LICENSE](LICENSE) for details.
