# Prototype Claude

**A BIG NOTE OF CAUTION WHEN READING THIS:** This entire project is a work in progress. There are inconsistencies and things that need changing. So please read it with a BIG pinch of salt. I am not an engineer, so an even BIGGER pinch of salt is recommended. 🔥🔥🔥

A practice project to improve prototyping skills using v0.dev. The goal is to create a functional prototype that closely resembles the [Claude.ai](https://claude.ai/) interface, with realistic interactions backed by local state management.

## Project Objectives

This prototype aims to:
- Create a visually accurate clone of the Claude.ai interface
- Implement "feels-like-real" functionality using Zustand for state management and local storage
- Support light and dark mode theme switching
- Define clean data interfaces that could easily be migrated to a backend database

## Features

The prototype will include the following pages:
- Chat Page: primary interaction screen
- Chats Page: lists all chats
- Project view: a project contains multiple chats
- Projects list: lists all projects
- Settings page: profile and display settings light/dark
- Shared slide-out drawer navigation throughout

## Technology Stack

- Next.js as the React framework
- Tailwind CSS for styling
- shadcn/ui for component library
- Zustand for state management
- Local storage for data persistence (managed by Zustland)

## Success Criteria

### Prototype Quality
- ✅ A plausible clone of the Claude.ai interface
- ✅ It "feels like real" thanks to state management with local storage
- ✅ Supports theme switching (light/dark mode)
- ✅ Provides realistic interface interactions

### Workflow Effectiveness
- ✅ Proven what is optimal to include in initial app creation prompt
- ✅ Established what documentation is useful to use (PRD, tracking docs, etc.) in project folder`docs/`
- ✅ The workflow is repeatable on a new prototype of another website, and it works with minimal change

### Code Quality
- ✅ Centralised theming implementation using Tailwind and shadcn/ui (once place to change everything)
- ✅ Well-organised, modular UI components (so they can be somewhat useful to handing off to engineers)
- ✅ Clean data interfaces that would facilitate database migration
- ✅ Consistent state management patterns using Zustand

## Development Approach

The entire UI will be generated using v0.dev, which provides a starting point with Next.js, Tailwind, and shadcn/ui components. The prototype will be purely frontend-focused with no actual AI functionality, but will maintain the illusion of a working product through effective state management.

Local storage will be used to persist:
- User data
- User preferences
- Chat history
- Project data