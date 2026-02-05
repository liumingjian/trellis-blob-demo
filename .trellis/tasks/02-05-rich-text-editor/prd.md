# Tiptap Rich Text Editor Integration

## Phase
Phase 1 - MVP (Article Management)

## Goal
Integrate Tiptap editor for article content with basic formatting capabilities.

## Requirements
- WYSIWYG editing experience
- Basic text formatting (headings, bold, italic, lists)
- Link insertion
- Clean HTML output

## Acceptance Criteria
- [ ] Tiptap editor component created
- [ ] Toolbar with formatting buttons
- [ ] Headings (H1, H2, H3) support
- [ ] Bold, italic, underline formatting
- [ ] Ordered and unordered lists
- [ ] Link insertion with URL input
- [ ] Content outputs clean HTML
- [ ] Editor state controlled via props
- [ ] Placeholder text when empty

## Technical Notes
- Use @tiptap/react and @tiptap/starter-kit
- Add @tiptap/extension-link for links
- Style toolbar with shadcn/ui buttons
- Sanitize HTML output before storage

## Dependencies
- setup-nextjs-project

## Files to Create
- `src/components/editor/tiptap-editor.tsx`
- `src/components/editor/editor-toolbar.tsx`
- `src/components/editor/editor.css`
