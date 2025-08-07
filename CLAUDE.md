# Retro Reader - Project Context for Claude

## Project Overview
Retro Reader is a React Native application designed for reading retro game guides, particularly from sources like GameFAQs for consoles like Super Nintendo. The app focuses on providing an optimal reading experience for ASCII-based guides that are typically 10,000+ lines long with ~90 character width formatting.

This project also serves as a demonstration of mobile CI/CD best practices, emphasizing curated commits, code decoupling, and comprehensive testing.

## Technical Architecture

### Core Principles
- **Functional Reactive Programming**: Immutable data structures, pure functions, avoid OOP
- **Dependency Injection**: Interface-based design with injected implementations
- **Separation of Concerns**: Highly decoupled modules for testability and maintainability
- **Test-Driven Development**: Simple, readable unit tests with 100% critical path coverage

### Technology Stack
- **Framework**: React Native with TypeScript
- **State Management**: Redux Toolkit or Zustand (functional approach)
- **Navigation**: React Navigation
- **Storage**: AsyncStorage for local data, SQLite for guide content
- **Testing**: Jest (unit), Detox or Maestro (UI)
- **Linting**: ESLint with strict configuration
- **CI/CD**: GitHub Actions for both iOS and Android

## Code Standards

### General Guidelines
- NO inline comments - use descriptive function and variable names instead
- Prefer composition over inheritance
- Use TypeScript strict mode
- Functional components only (no class components)
- Custom hooks for reusable logic
- Immutable state updates

### File Structure
```
src/
├── domain/           # Business logic interfaces
├── infrastructure/   # External service implementations
├── presentation/     # UI components and screens
├── application/      # Use cases and orchestration
├── shared/          # Shared utilities and types
└── tests/           # Test files mirroring src structure
```

### Testing Requirements
- Unit tests for all business logic
- Integration tests for data flows
- UI tests for critical user journeys
- No skipped or commented tests allowed
- Test files should be highly readable with clear descriptions

## CI/CD Pipeline

### Build Requirements
1. **Linting**: Must pass strict ESLint rules
2. **Type Checking**: TypeScript compilation with strict mode
3. **Unit Tests**: 100% pass rate required
4. **UI Tests**: Critical path coverage
5. **Build Artifacts**: 
   - iOS: Built via GitHub Actions free tier
   - Android: Built via GitHub Actions using custom Docker image with Android SDK

### Docker Image for Android Builds
The project includes a Dockerfile that creates an image with:
- Android SDK
- Required build tools
- React Native dependencies
- Node.js environment

## Feature Implementation Guidelines

### Guide Storage System
- Guides stored as structured data (not raw text)
- Support for metadata (title, system, author, version)
- Efficient indexing for large documents
- Import/export in multiple formats

### Reading Experience
- Monospace font rendering for ASCII art preservation
- Smooth scrolling for long documents
- Bookmark system with categories
- Current position tracking (persisted between sessions)
- Dynamic font sizing based on viewport

### Screen Adaptation
- Support for multiple screen configurations
- Special handling for foldable devices
- Orientation-specific settings
- Font size preferences per screen type

### Collections/Folders
- Hierarchical organization structure
- Support for mixed content types:
  - Text guides
  - Image links (maps, charts)
  - Web links
  - Related guide references

## Development Workflow

### Commit Standards
- Conventional commits format (feat:, fix:, docs:, etc.)
- Atomic commits (one logical change per commit)
- Comprehensive commit messages
- No WIP commits in main branch

### Branch Strategy
- `main`: Production-ready code
- `develop`: Integration branch
- `feature/*`: Feature development
- `fix/*`: Bug fixes
- `release/*`: Release preparation

### Pull Request Requirements
- All CI checks must pass
- Code review required
- Update relevant documentation
- Include test coverage

## Commands

### Development
```bash
npm run start          # Start Metro bundler
npm run ios           # Run iOS app
npm run android       # Run Android app
npm run test          # Run unit tests
npm run test:watch    # Run tests in watch mode
npm run lint          # Run ESLint
npm run typecheck     # Run TypeScript compiler
npm run test:e2e:ios  # Run iOS UI tests
npm run test:e2e:android # Run Android UI tests
```

### Build
```bash
npm run build:ios     # Build iOS release
npm run build:android # Build Android release
```

## Current Development Focus

### Phase 1: Infrastructure Setup
- Initialize React Native project with TypeScript
- Configure development environment
- Setup CI/CD pipeline
- Implement core architecture patterns

### Phase 2: Core Features
- Guide storage and management
- Basic reader implementation
- Bookmark system

### Phase 3: Advanced Features
- Collections/folders
- Import/export functionality
- Multi-screen support

### Phase 4: Polish
- Performance optimization
- Accessibility features
- UI/UX refinements

## Known Constraints
- Large guide files (10k+ lines) require efficient rendering
- ASCII art must maintain formatting
- Monospace font is essential
- Must work offline (no server dependency)

## Testing Scenarios

### Critical User Journeys
1. Import a guide from file
2. Navigate to specific bookmark
3. Resume reading from last position
4. Export guide collection
5. Switch between screen configurations

### Performance Benchmarks
- Guide load time < 2 seconds
- Smooth scrolling at 60 FPS
- Memory usage < 100MB for typical guide
- Battery efficient for long reading sessions

## Architecture Decisions

### Why Functional Reactive Programming?
- Predictable state management
- Easier testing with pure functions
- Better debugging with immutable data
- Natural fit for React Native

### Why Dependency Injection?
- Testability through mocking
- Flexibility to swap implementations
- Clear separation of concerns
- Easier to maintain and extend

### Why Strict Linting?
- Consistent code style
- Catch errors early
- Enforce best practices
- Reduce code review overhead

## Future Considerations
- Cloud sync capabilities
- Social features (sharing bookmarks)
- Guide annotations
- Theme customization beyond font size
- Tablet-optimized layouts