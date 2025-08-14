# Retro Reader - Project Context for Claude

## Project Overview
Retro Reader is a React Native application designed for reading retro game guides, particularly from sources like GameFAQs for consoles like Super Nintendo. The app focuses on providing an optimal reading experience for ASCII-based guides.

This project also serves as a demonstration of mobile CI/CD best practices, emphasizing curated commits, code decoupling, and comprehensive testing.

## Technical Architecture

### Core Principles
- **Functional Reactive Programming**: Immutable data structures, pure functions, avoid OOP
- **Dependency Injection**: Interface-based design with injected implementations
- **Separation of Concerns**: Highly decoupled modules for testability and maintainability
- **Test-Driven Development**: Simple, readable unit tests with 100% critical path coverage

### Technology Stack
- **Framework**: React Native with TypeScript
- **State Management**: Zustand (functional approach, lightweight)
- **Navigation**: React Navigation
- **Storage**: AsyncStorage for local data, SQLite for guide content
- **Testing**: Jest (unit), Maestro (UI)
- **Linting**: ESLint with strict configuration
- **Code Formatting**: Prettier for consistent formatting
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
│   ├── guide.ts
│   └── guide.test.ts # Test files co-located with source
├── infrastructure/   # External service implementations  
├── presentation/     # UI components and screens
├── application/      # Use cases and orchestration
└── shared/          # Shared utilities and types
```

### Testing Requirements
- Unit tests for all business logic
- Integration tests for data flows
- UI tests for critical user journeys
- No skipped or commented tests allowed
- Test files should be highly readable with clear descriptions
- Test files co-located with source files (*.test.ts, *.spec.ts)

## CI/CD Pipeline

### Build Requirements
1. **Linting**: Must pass strict ESLint rules
2. **Code Formatting**: Prettier check must pass
3. **Type Checking**: TypeScript compilation with strict mode
4. **Unit Tests**: 100% pass rate required
5. **UI Tests**: Critical path coverage with Maestro
6. **Build Artifacts**: 
   - iOS: Built via GitHub Actions free tier
   - Android: Built via GitHub Actions using custom Docker image with Android SDK

### Docker-in-Docker Architecture for Android Builds
The project uses a Docker-in-Docker (DinD) approach with two separate images:

**1. Android SDK Image:**
- Android SDK only
- Build tools and platform tools
- Minimal footprint for SDK operations

**2. React/Node Image:**
- Node.js environment
- React Native dependencies  
- Build toolchain

The GitHub Action uses DinD as the entry container, allowing artifacts built by the Node image to be available to the Android image for final APK generation.

## Feature Implementation Guidelines

### Guide Storage System
- Guides stored as structured data (not raw text)
- Support for metadata (title, game, system, author)
- Efficient indexing for large documents
- Import/export json

### Reading Experience
- Monospace font rendering for ASCII art preservation
- Smooth scrolling for long documents
- Bookmark system with categories
- Current position tracking (persisted between sessions)
- Dynamic font sizing based on viewport

### Screen Adaptation
- Support for multiple screen configurations
- Special handling multiple viewports (eg foldable phones, orientation)
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
- Atomic commits (one logical change per commit)
- Comprehensive commit messages
- No WIP commits

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
npm run format        # Run Prettier
npm run format:check  # Check Prettier formatting
npm run typecheck     # Run TypeScript compiler
npm run test:e2e:ios  # Run iOS UI tests
npm run test:e2e:android # Run Android UI tests
```

### Release
```bash
npm run release:ios     # Build iOS release
npm run release:android # Build Android release
```

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
- Guide load time < 1 seconds
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
- Sync capabilities
- Social features (sharing bookmarks)
- Guide annotations
- Theme customization beyond font size
- Tablet-optimized layouts
- Table of Contents detection and bookmark generation
