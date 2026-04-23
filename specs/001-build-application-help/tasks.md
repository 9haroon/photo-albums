---
description: "Task list for Photo Album Organization System"
---

# Tasks: Photo Album Organization System

**Input**: Design documents from `/specs/001-build-application-help/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

## Phase 1: Setup

- [ ] T001 Initialize Next.js 16 project structure per implementation plan
- [ ] T002 [P] Install dependencies: @supabase/supabase-js, zod, dnd-kit
- [ ] T003 [P] Configure TypeScript, ESLint, and Prettier

## Phase 2: Foundational

- [ ] T004 Setup Supabase database schema (SQL migrations for albums, photos)
- [ ] T005 [P] Setup Supabase authentication client in src/lib/supabase.ts
- [ ] T006 [P] Create Zod base schemas in src/lib/schemas.ts
- [ ] T007 Configure Next.js API route handlers directory in src/app/api/
- [ ] T008 Implement error middleware for machine-readable codes in src/lib/error-handler.ts

## Phase 3: User Story 1 - Create and Populate Photo Albums (Priority: P1)

**Goal**: Enable creating albums and adding photos for tile preview.

- [ ] T009 [P] [US1] Create Album entity/interface in src/types/album.ts
- [ ] T010 [P] [US1] Create Photo entity/interface in src/types/photo.ts
- [ ] T011 [US1] Implement AlbumService (CRUD) in src/services/album.service.ts
- [ ] T012 [US1] Implement PhotoService (Upload/Association) in src/services/photo.service.ts
- [ ] T013 [US1] Implement POST /api/albums handler in src/app/api/albums/route.ts
- [ ] T014 [US1] Implement POST /api/photos handler in src/app/api/photos/route.ts
- [ ] T015 [US1] Build Album grid component in src/components/AlbumGrid.tsx
- [ ] T016 [US1] Build Photo tile preview component in src/components/PhotoTile.tsx

## Phase 4: User Story 2 - Organize Albums by Chronological Grouping (Priority: P2)

**Goal**: Automatically group albums by date headers.

- [ ] T017 [US2] Update AlbumService to support date-based grouping query in src/services/album.service.ts
- [ ] T018 [US2] Implement date-grouping logic in frontend UI state in src/components/AlbumDashboard.tsx

## Phase 5: User Story 3 - Reorder Albums via Drag-and-Drop (Priority: P3)

**Goal**: Enable drag-and-drop album reordering.

- [ ] T019 [US3] Add sort_order field update method to AlbumService in src/services/album.service.ts
- [ ] T020 [US3] Implement PATCH /api/albums/reorder handler in src/app/api/albums/reorder/route.ts
- [ ] T021 [US3] Integrate dnd-kit for AlbumGrid in src/components/AlbumGrid.tsx
- [ ] T022 [US3] Implement optimistic UI update for reordering in src/components/AlbumDashboard.tsx

## Phase 6: Polish & Cross-Cutting Concerns

- [ ] T023 [P] Add documentation updates in specs/README.md
- [ ] T024 Perform code cleanup and type validation across all services
- [ ] T025 Run final build and lint check

---

## Dependencies & Execution Order

- **Foundational (Phase 2)**: BLOCKS all user stories.
- **User Stories (Phase 3-5)**: Can start after Phase 2.
- **Order**: P1 (US1) → P2 (US2) → P3 (US3) for incremental delivery.
