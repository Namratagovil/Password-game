Password Challenge Game
Overview
A Luma-inspired password challenge game (inspired by neal.fun/password-game) where users must craft a continuous password (no spaces) that satisfies all 20 progressively revealed rules. Built as a single-page frontend app with dark/light theme support.

Architecture
- Frontend-only game logic - no database or backend API needed
- Express server serves the static frontend
- All rule validation happens client-side in client/src/lib/passwordRules.ts

Key Files
- client/src/pages/PasswordGame.tsx - Main game page with all UI components, theme toggle, collapsible groups
- client/src/lib/passwordRules.ts - 20 rule definitions with validation functions
- client/src/index.css - CSS custom properties for dark/light theme (--game-* variables)
- client/src/App.tsx - Router setup

Design System
- Themes: Dark mode (#14161C bg) and Light mode (#F4F5F7 bg) with sun/moon toggle
- All colors use CSS custom properties (--game-*) defined in :root (light) and .dark (dark)
- Dark accents: Anakiwa blue (#A9C9FF), Shakespeare blue (#53ADD2)
- Light accents: Blue (#2E78B5), Darker blue (#1B6AAA)
- Success: Emerald green for passed rules
- Error indicators: Amber dot for failing rules
- Current rule: Blue highlight with "Current" badge and pulse animation
- Typography: Inter (sans), Geist Mono (mono)
- Glassmorphism: Backdrop blur on sticky header and input zone
- Theme persists via localStorage key pw-game-theme

Features
- Progressive disclosure: Rules unlock as previous ones are satisfied
- Collapsible groups: 4 groups (The Basics, Complexity, External Data, The Endgame) with expand/collapse
- Current rule focus: First failing rule highlighted with auto-scroll and auto-expand of its group
- Restart modal: Confirmation dialog before resetting
- Success screen: Confetti animation when all 20 rules pass
- Dark/Light toggle: Sun/Moon icon in header, right side

Dependencies
- Standard shadcn/ui component library
- No database required

Rules Engine
- Rules are progressively disclosed - the next rule appears only when all previous rules pass. 20 rules across 4 groups: The Basics (1-5), Complexity (6-10), External Data (11-15), The Endgame (16-20).

Key rule implementation details:
- Continuous password: No spaces; all rules work via substring matching (no word boundaries)
Roman numerals: Only sequences of 2+ chars (/[IVXLCDM]{2,}/g) so single letters like L in "Luma" are ignored
Chess moves: No \b word boundaries so inline moves like Nf3 are detected
Everything else: Uses includes() for substring matching
