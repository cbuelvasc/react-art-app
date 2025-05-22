# ReactArt App Documentation

## Project Overview

ReactArt is a React-based web application that creates a community platform for artists and art enthusiasts. The application is built using React 19 and Vite, featuring a modern authentication interface with a visually appealing design.

## Technology Stack

- **Frontend Framework**: React 19.1.0
- **Build Tool**: Vite 6.3.5
- **Testing Framework**: Vitest with React Testing Library
- **Code Quality Tools**: ESLint 9.25.0, Prettier 3.5.3

## Project Structure

```
react-art-app/
├── src/                   # Source code
│   ├── assets/            # Static assets like images
│   │   └── logo.png       # Application logo
│   ├── components/        # React components
│   │   ├── Header.jsx     # Application header component
│   │   ├── Header.css     # Styles for header component
│   │   └── AuthInputs.jsx # Authentication form component
│   ├── __tests__/         # Test files
│   │   └── setup.js       # Test configuration setup
│   ├── App.jsx            # Main application component
│   ├── App.test.jsx       # Tests for App component
│   ├── index.css          # Global styles
│   └── main.jsx           # Application entry point
├── public/                # Public assets
│   └── vite.svg           # Vite logo
├── .github/               # GitHub configuration
│   └── workflows/         # GitHub Actions workflows
│       └── deployment.yml # CI/CD pipeline for Docker image
├── doc/                   # Documentation
├── .gitignore             # Git ignore file
├── .prettierrc            # Prettier configuration
├── Dockerfile             # Docker configuration
├── eslint.config.js       # ESLint configuration
├── index.html             # HTML entry point
├── package.json           # Project dependencies and scripts
├── package-lock.json      # Dependency lock file
└── vite.config.js         # Vite configuration
```

## Core Components

### App Component
The main application component that renders the Header and authentication inputs.

### Header Component
Displays the application logo, title, and tagline:
- Logo image from assets
- "ReactArt" title
- "A community of artists and art-lovers" tagline

### AuthInputs Component
Manages user authentication with:
- Email input field with validation (must include '@')
- Password input field with validation (minimum 6 characters)
- "Create a new account" and "Sign In" buttons
- Form validation that triggers on submission

## Styling

The application uses a combination of:
- Global CSS in `index.css`
- Component-specific CSS files (e.g., `Header.css`)
- Inline conditional styling for form validation

The color scheme features warm orange and yellow gradients with dark authentication forms, creating a visually engaging user interface.

## Development Scripts

- `npm run dev`: Start development server with Vite
- `npm run build`: Build for production
- `npm run lint`: Run ESLint for code quality
- `npm run format`: Format code with Prettier
- `npm run test`: Run tests with Vitest
- `npm run preview`: Preview production build

## Docker

### Building the Docker image

To build a Docker image of the application, run:

```bash
docker build . -t "react-art-app:v1.0.0"
```

### Running the Docker container

To run the application in a Docker container, execute:

```bash
docker run -dp 3000:3000 react-art-app:v1.0.0
```

This will map port 3000 from the container to port 3000 on your host machine, allowing you to access the application at `http://localhost:3000`.

### GitHub Container Registry

The Docker image is also available in GitHub Container Registry. You can pull it with:

```bash
docker pull ghcr.io/cbuelvasc/react-art-app:latest
```

Or use a specific version by SHA:

```bash
docker pull ghcr.io/cbuelvasc/react-art-app:ab97ef11e77274b8596ceab6f8b4d3ce817dd444
```

To run the application using the image from GitHub Container Registry:

```bash
docker run -dp 3000:3000 ghcr.io/cbuelvasc/react-art-app:latest
```

The Docker image is automatically built and published to GitHub Container Registry through GitHub Actions whenever changes are pushed to the master branch.


## Testing

The application includes test files with Jest and React Testing Library for component testing.

## Deployment

The project can be built for production using the `npm run build` command, which generates optimized assets ready for deployment.
