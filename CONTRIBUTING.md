# Contributing to Smart Crop Technologies

Thank you for considering contributing to Smart Crop Technologies! We welcome contributions from developers, designers, farmers, and agriculture enthusiasts worldwide.

## 🌾 How Can I Contribute?

### 🐛 Reporting Bugs

If you find a bug, please create an issue with:
- Clear title and description
- Steps to reproduce
- Expected vs actual behavior
- Screenshots if applicable
- Your environment (OS, browser, Node version)

### 💡 Suggesting Features

We love new ideas! Open an issue with:
- Feature description
- Use case / problem it solves
- Mockups or examples (if applicable)
- Why farmers would benefit

### 🔧 Code Contributions

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Make your changes**
   - Follow code style (ESLint + Prettier)
   - Add tests if applicable
   - Update documentation
4. **Commit with clear messages**
   ```bash
   git commit -m "Add: Feature description"
   ```
5. **Push to your fork**
   ```bash
   git push origin feature/amazing-feature
   ```
6. **Open a Pull Request**

## 📝 Code Style Guide

### TypeScript
- Use TypeScript for all new files
- Define proper interfaces and types
- Avoid `any` type

### React Components
```tsx
// Good
interface Props {
  title: string;
  count: number;
}

export default function MyComponent({ title, count }: Props) {
  return <div>{title}: {count}</div>;
}
```

### Naming Conventions
- Components: PascalCase (`MyComponent.tsx`)
- Files: camelCase (`myUtil.ts`)
- CSS classes: kebab-case (`my-class`)
- Constants: UPPER_SNAKE_CASE (`API_URL`)

### Code Organization
- One component per file
- Group related files in folders
- Keep components small and focused
- Extract reusable logic to hooks or utils

## 🧪 Testing

- Write tests for new features
- Ensure existing tests pass
- Run `npm test` before submitting PR

## 📚 Documentation

- Update README.md if changing setup
- Add JSDoc comments for complex functions
- Update API documentation for new endpoints
- Include examples in comments

## 🎨 Design Guidelines

- Follow existing UI patterns
- Use Tailwind utility classes
- Maintain mobile-first approach
- Ensure accessibility (WCAG AA)
- Test on multiple devices

## 🌍 Internationalization

When adding new text:
```typescript
// Add to lib/i18n.ts
const translations = {
  en: { newKey: 'English text' },
  hi: { newKey: 'हिंदी पाठ' },
};
```

## 🚀 Pull Request Process

1. Update README.md with details of changes
2. Update version numbers (if applicable)
3. PR will be merged after:
   - Code review approval
   - All tests passing
   - No conflicts with main branch

## 🏷️ Commit Message Format

Use semantic commit messages:
- `Add:` New feature
- `Fix:` Bug fix
- `Update:` Change existing feature
- `Remove:` Remove feature
- `Docs:` Documentation only
- `Style:` Code formatting
- `Refactor:` Code restructuring
- `Test:` Adding tests
- `Chore:` Maintenance tasks

Example:
```
Add: Image upload progress indicator

- Added progress bar component
- Integrated with upload API
- Updated upload page UI
```

## 💬 Community

- Be respectful and inclusive
- Help others learn
- Share knowledge
- Celebrate diversity

## 📧 Contact

Questions? Reach out:
- GitHub Issues
- Email: contribute@smartcrop.tech

## 🙏 Recognition

Contributors will be:
- Listed in README.md
- Mentioned in release notes
- Part of our community

Thank you for helping farmers! 🌾💚
