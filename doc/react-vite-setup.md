# React Project Setup with Vite, Prettier and Vitest

## Introduction

Vite (French word for "quick", pronounced `/vit/`) is a build tool that provides a faster and leaner development experience for modern web projects. It consists of two major parts:

- A dev server with extremely fast Hot Module Replacement (HMR)
- A build command that bundles your code with Rollup, pre-configured to output highly optimized static assets for production

## Project Creation

```bash
# Create a new React project with Vite
npm create vite@latest
# Select React and JavaScript/TypeScript according to preference
cd project-name
npm install
npm run dev
```

## ESLint and Prettier Configuration

### Install Prettier

```bash
npm i -D -E prettier
```

Create `.prettierrc` file:

```json
{
  "semi": true,
  "singleQuote": true,
  "trailingComma": "all",
  "printWidth": 120,
  "tabWidth": 2,
  "useTabs": false,
  "arrowParens": "always",
  "bracketSpacing": true,
  "jsxBracketSameLine": false,
  "jsxSingleQuote": false
}
```

### Install plugins to avoid conflicts between ESLint and Prettier

```bash
npm i -D eslint-config-prettier eslint-plugin-prettier eslint-plugin-import eslint-plugin-react
```

### Configure ESLint (eslint.config.js)

```bash
# Create the ESLint configuration file
touch eslint.config.js
```

Add the following content to `eslint.config.js`:

```javascript
import js from '@eslint/js'
import globals from 'globals'
import reactHooks from 'eslint-plugin-react-hooks'
import reactRefresh from 'eslint-plugin-react-refresh'
import react from 'eslint-plugin-react'
import importPlugin from 'eslint-plugin-import'
import prettierConfig from 'eslint-config-prettier'

export default [
  { ignores: ['dist'] },
  prettierConfig,
  {
    files: ['**/*.{js,jsx}'],
    languageOptions: {
      ecmaVersion: 2020,
      globals: globals.browser,
      parserOptions: {
        ecmaVersion: 'latest',
        ecmaFeatures: { jsx: true },
        sourceType: 'module',
      },
    },
    settings: {
      react: {
        version: '18.2'
      }
    },
    plugins: {
      'react-hooks': reactHooks,
      'react-refresh': reactRefresh,
      'react': react,
      'import': importPlugin,
    },
    rules: {
      ...js.configs.recommended.rules,
      ...reactHooks.configs.recommended.rules,
      ...react.configs.recommended.rules,
      ...react.configs['jsx-runtime'].rules,
      'no-unused-vars': ['error', { varsIgnorePattern: '^[A-Z_]' }],
      'react-refresh/only-export-components': [
        'warn',
        { allowConstantExport: true },
      ],
      'import/newline-after-import': ['error', { count: 1 }],
    },
  },
]
```

### Add formatting script to package.json

```bash
# Add format script to package.json
npm pkg set scripts.format="prettier --write ./src"
```

### VS Code Configuration (`.vscode/settings.json`)

```bash
# Create VS Code settings directory and file
mkdir -p .vscode
touch .vscode/settings.json
```

Add the following content to `.vscode/settings.json`:

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnPaste": true,
  "editor.formatOnType": false,
  "editor.formatOnSave": true,
  "editor.formatOnSaveMode": "file",
  "files.autoSave": "onFocusChange"
}
```

## Testing Configuration with Vitest

### Install dependencies

```bash
npm i -D vitest jsdom @testing-library/jest-dom @testing-library/react
```

### Create test configuration file

```bash
# Create tests directory
mkdir -p src/__tests__
touch src/__tests__/setup.js
```

Add the following content to `src/__tests__/setup.js`:
```javascript
// jest-dom adds custom jest matchers for asserting on DOM nodes.
// allows you to do things like:
// expect(element).toHaveTextContent(/react/i)
// learn more: https://github.com/testing-library/jest-dom
import '@testing-library/jest-dom';
```

### Modify vite.config.js

Update your `vite.config.js` file with the following content:

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  test: {
    globals: true,
    environment: 'jsdom',
    setupFiles: ['src/__tests__/setup.js'],
  },
})
```

### Write an example test

```bash
# Create test file
touch src/App.test.jsx
```

Add the following content to `App.test.jsx`:
```javascript
import { describe, it, expect, test } from 'vitest';
import { render } from '@testing-library/react';
import App from './App';

test('demo', () => {
  expect(true).toBe(true);
});

describe('render', () => {
  it('renders the main page', () => {
    render(<App />);
    expect(true).toBeTruthy();
  });
});
```

### Add test script to package.json

```bash
# Add test script to package.json
npm pkg set scripts.test="vitest"
```

## Run the formatting and linting commands

```bash
# Format your code
npm run format

# Run the linter
npm run lint

# Run tests
npm test
```

## Final package.json Structure

```json
{
  "name": "react-art-app",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint .",
    "format": "prettier --write ./src",
    "test": "vitest",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^19.1.0",
    "react-dom": "^19.1.0"
  },
  "devDependencies": {
    "@eslint/js": "^9.25.0",
    "@testing-library/jest-dom": "^6.6.3",
    "@testing-library/react": "^16.3.0",
    "@types/react": "^19.1.2",
    "@types/react-dom": "^19.1.2",
    "@vitejs/plugin-react": "^4.4.1",
    "eslint": "^9.25.0",
    "eslint-config-prettier": "^10.1.5",
    "eslint-plugin-import": "^2.31.0",
    "eslint-plugin-prettier": "^5.4.0",
    "eslint-plugin-react": "^7.37.5",
    "eslint-plugin-react-hooks": "^5.2.0",
    "eslint-plugin-react-refresh": "^0.4.19",
    "globals": "^16.0.0",
    "jsdom": "^26.1.0",
    "prettier": "3.5.3",
    "vite": "^6.3.5",
    "vitest": "^3.1.4"
  }
}
```

## Final Verification

```bash
# Run all tests
npm test
```

Now you can use this project as a template for your next React applications.