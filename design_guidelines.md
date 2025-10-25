# Community Knowledge Bot - Design Guidelines

## Design Approach

**Selected Approach**: Design System-inspired (Material Design + Linear aesthetics)
**Rationale**: This is a utility-focused application where efficiency, clarity, and usability are paramount. Users need quick access to information through an intuitive chat interface and straightforward knowledge base management.

**Key Design Principles**:
- Information clarity and hierarchy
- Conversational, approachable interface
- Efficient task completion
- Trust through transparency (source references)

---

## Typography System

**Font Families** (via Google Fonts):
- Primary: Inter (interface, chat messages, buttons)
- Mono: JetBrains Mono (code snippets, technical content)

**Hierarchy**:
- Page Titles: text-3xl md:text-4xl, font-bold
- Section Headers: text-xl md:text-2xl, font-semibold
- Chat Messages: text-base, font-normal
- Bot Responses: text-base, font-normal, leading-relaxed
- Metadata/Timestamps: text-xs md:text-sm, font-medium
- Source References: text-sm, font-medium
- Button Text: text-sm md:text-base, font-semibold

---

## Layout System

**Spacing Primitives**: Tailwind units of **2, 4, 6, 8, 12, 16**
- Micro spacing (gaps, paddings): 2, 4
- Component spacing: 6, 8
- Section spacing: 12, 16

**Grid Structure**:
- Main chat container: max-w-5xl mx-auto
- Sidebar (knowledge base): w-64 md:w-80
- Chat messages: max-w-3xl
- Knowledge cards: Grid with grid-cols-1 md:grid-cols-2 lg:grid-cols-3

---

## Component Library

### Navigation & Header
**Top Navigation Bar**:
- Fixed position with backdrop blur
- Height: h-16
- Contains: Logo/branding (left), knowledge base toggle (center), user menu (right)
- Padding: px-4 md:px-8
- Border: border-b with subtle divider

### Chat Interface (Primary Component)

**Chat Container**:
- Two-column layout on desktop: sidebar (optional toggle) + main chat area
- Full-screen on mobile with drawer-based sidebar
- Main chat area: flex flex-col with header, messages area, input at bottom

**Message Bubbles**:
- User messages: Align right, rounded-2xl rounded-tr-md, px-4 py-3, max-w-2xl
- Bot messages: Align left, rounded-2xl rounded-tl-md, px-4 py-3, max-w-2xl
- Spacing between messages: space-y-4
- Include avatar (user) or bot icon (8x8 or 10x10)

**Source Reference Cards** (attached to bot messages):
- Appear below bot response
- Compact card design: rounded-lg, p-3, border
- Display: Document icon + title + snippet preview
- Hover state: subtle lift effect (shadow-sm to shadow-md)
- Click to expand full document context

**Chat Input Area**:
- Fixed at bottom of chat container
- Multi-line textarea with auto-expand (max 4-5 lines)
- Height: min-h-[48px]
- Padding: p-4
- Rounded: rounded-xl
- Send button: Icon button (paper plane/send) positioned absolute right
- Border: border with focus ring

**Typing Indicator**:
- Animated three-dot pattern
- Same styling as bot message bubble
- Display: flex items-center gap-1

### Knowledge Base Management

**Sidebar/Panel**:
- Collapsible on mobile, persistent on desktop
- Sections: "Recent Conversations", "Knowledge Base", "Settings"
- Scrollable content area with custom scrollbar styling

**Knowledge Base Cards**:
- Grid layout: grid gap-4
- Card structure: rounded-lg, p-4, border
- Elements per card:
  - Document type icon (top-left, 12x12)
  - Title (text-base font-semibold)
  - Preview text (text-sm, 2-line clamp)
  - Metadata footer (text-xs, uploaded date, file size)
  - Action menu (three dots, top-right)

**Upload Component**:
- Drag-and-drop zone: Dashed border (border-2 border-dashed), rounded-xl
- Minimum height: min-h-[200px]
- Center-aligned upload icon and text
- Support multiple file types indicator
- Progress bar during upload: h-2 rounded-full

**Document Viewer Modal**:
- Full-screen overlay with backdrop blur
- Content area: max-w-4xl mx-auto, rounded-xl
- Header: Document title + close button
- Body: Scrollable content with proper typography
- Footer: Source info + actions (edit, delete)

### Forms & Inputs

**Text Input Fields**:
- Height: h-12
- Padding: px-4
- Border radius: rounded-lg
- Border: border with focus ring (ring-2)
- Label: text-sm font-medium, mb-2

**Search Bar** (for knowledge base):
- Height: h-10
- Padding: pl-10 pr-4 (space for search icon)
- Rounded: rounded-full
- Icon: Absolute positioned left, 16x16

### Buttons

**Primary CTA** (Send, Upload, Save):
- Height: h-10 md:h-12
- Padding: px-6 md:px-8
- Rounded: rounded-lg
- Font: text-sm md:text-base font-semibold

**Secondary** (Cancel, Back):
- Same dimensions as primary
- Border variant

**Icon Buttons** (Menu, Close, More):
- Size: w-10 h-10
- Rounded: rounded-lg
- Centered icon: 20x20

### Data Display

**Conversation History List**:
- List items: p-3, rounded-lg
- Hover state with background change
- Elements: Timestamp (text-xs), preview text (text-sm, 1-line clamp)
- Active conversation: Highlighted with border-l-4

**Stats/Metrics** (if dashboard view):
- Card grid: grid-cols-1 md:grid-cols-3 gap-6
- Each card: p-6, rounded-xl, border
- Metric number: text-3xl font-bold
- Label: text-sm

### Loading States

**Skeleton Loaders**:
- Message skeleton: h-16 rounded-2xl, animate-pulse
- Card skeleton: h-32 rounded-lg, animate-pulse
- Use for initial load and data fetching

**Spinners**:
- Circular spinner for inline loading (16x16 or 20x20)
- Use sparingly, prefer skeleton loaders

### Empty States

**No Conversations**:
- Centered illustration placeholder (robot/document icon, 64x64)
- Heading: "Start a Conversation"
- Description text: "Ask anything about [Community Name]"
- CTA button

**No Documents**:
- Upload icon (48x48)
- Heading + description
- Upload button

---

## Icons

**Library**: Heroicons (via CDN)
**Usage**:
- Navigation: home, document-text, cog-6-tooth
- Chat: paper-airplane, user-circle, sparkles (AI)
- Knowledge Base: folder, document-duplicate, cloud-arrow-up
- Actions: ellipsis-vertical, trash, pencil-square, magnifying-glass
- States: check-circle, exclamation-circle, information-circle

---

## Animations

**Minimal, purposeful animations**:
- Message appearance: Subtle fade-in from bottom (duration-200)
- Typing indicator: Bounce animation on dots
- Modal/drawer transitions: Slide and fade (duration-300)
- Hover states: Transform scale-[1.02] (duration-150)

**No** scroll-based animations, parallax effects, or decorative motion.

---

## Images

**Hero Section** (Landing/Welcome Screen - before chat):
- Large hero image: Illustration or photo representing community/knowledge sharing
- Dimensions: Full viewport width, h-[400px] md:h-[500px]
- Overlay: Gradient overlay for text readability
- CTA buttons on hero: Implement with backdrop-blur-sm backgrounds

**Image Descriptions**:
1. **Hero Image**: Modern illustration of people collaborating, sharing knowledge, or a stylized representation of AI/chat interaction. Warm, welcoming, professional aesthetic.
2. **Empty State Illustrations**: Simple, minimalist icon-style illustrations (robot for chat, document stack for knowledge base)
3. **Avatar Placeholders**: Generic user silhouettes or initial-based avatars

**Placement**:
- Hero: Top of landing page only (not in chat interface)
- Empty states: Centered in respective sections
- Avatars: Left of user messages, bot icon for AI responses