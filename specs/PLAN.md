# Implementation Plan: Photo Album Organization System

**Branch**: `001-build-application-help` | **Date**: 2026-04-19 | **Spec**: [specs/001-build-application-help/spec.md](specs/001-build-application-help/spec.md)
**Input**: Feature specification from `/specs/001-build-application-help/spec.md`

## Summary

Build a photo organization backend and web interface using Next.js 16 (App Router) and Supabase. The system allows users to create flat-structure photo albums, group them chronologically, and reorder them via drag-and-drop. Business logic resides in service-layer functions, with API schema validation at the route boundary.

## Technical Context

**Language/Version**: TypeScript 5.x, Node.js 22.x  
**Primary Dependencies**: Next.js 16, Supabase Client SDK (@supabase/supabase-js), Zod (schema validation), Dnd-kit (drag-and-drop)  
**Storage**: Supabase PostgreSQL (Albums, Photos, UserProfiles)  
**Testing**: Integration tests (Playwright) covering API endpoints; unit tests for service-layer logic  
**Target Platform**: Web (Next.js App Router)  
**Project Type**: Web Application  
**Performance Goals**: &lt;200ms API response for album fetches  
**Constraints**: Flat album structure (no nesting), Supabase Auth mandated  
**Scale/Scope**: Initial implementation for single-user photo management; potential for multi-user scaling.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- [x] **Code Quality**: Business logic isolated in `src/services/`. No route handler logic.
- [x] **Testing Requirements**: Integration tests planned for all public API endpoints.
- [x] **Error Handling**: Boundary validation using Zod. All errors return machine-readable codes.
- [x] **Performance Constraints**: N/A
- [x] **UX Consistency**: N/A

## Project Structure

### Documentation (this feature)

```text
specs/001-build-application-help/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
└── tasks.md
```

### Source Code

```text
src/
├── app/             # Next.js 16 App Router (Routes + UI)
├── services/        # Service-layer logic (Albums, Photos, Organization)
├── lib/             # Database (Supabase client), Schema Validation (Zod)
├── components/      # UI (Drag-and-drop tiles, Album previews)
└── types/           # Shared TypeScript interfaces
```

**Structure Decision**: Web application structure utilizing Next.js 16 App Router with dedicated service and data access layers.

## Complexity Tracking

&gt; N/A - No constitution violations identified.

---

## Phased Delivery Plan

### Phase 0: Research &amp; Data Modeling
- Define Supabase SQL schema: `albums` (id, user_id, title, date, sort_order, created_at), `photos` (id, album_id, url, created_at).
- Map API contracts (Zod schemas).

### Phase 1: Service Layer &amp; Database
- Implement `AlbumService` (CRUD, ordering logic).
- Implement `PhotoService` (Upload, association).
- Setup Supabase Auth middleware.

### Phase 2: API &amp; Validation
- Implement Route Handlers (`app/api/...`) with Zod boundary validation.
- Implement error middleware to ensure machine-readable codes.

### Phase 3: UI Implementation
- Build Album grid and photo tile view.
- Integrate `dnd-kit` for drag-and-drop reordering.
- Implement optimistic UI updates for reordering.

### Phase 4: Integration Testing
- Write Playwright tests for full CRUD flows and reordering persistence.

## Risks
- **Drag-and-Drop Latency**: Reordering persistence needs to be performant to avoid perceived lag; mitigated via optimistic updates.
- **Data Consistency**: Maintaining `sort_order` sequence across concurrent updates (will use PostgreSQL transaction locking).