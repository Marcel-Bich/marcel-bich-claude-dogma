# Accessibility Rules (Optional)

<applicability>
**When to apply:** End-user-facing web applications only.
**Skip for:** CLI tools, backend services, internal tools.
</applicability>

<rules>
1. **Mobile-First** - Design for smallest viewport (320px) first, enhance for larger.
2. **Touch targets** - Minimum 44x44px for touch-interactive elements.
3. **Keyboard navigation** - All interactive elements reachable via keyboard.
4. **ARIA labels** - Screen reader support for non-semantic elements.
5. **Color contrast** - Minimum 4.5:1 for text, 3:1 for large text.
6. **Alt text** - All meaningful images need descriptive alt text.
7. **Focus visible** - Focus indicator must be visible on all interactive elements.
</rules>

For details see `GUIDES/accessibility.md`
