# Day 22: Design Google Docs - Real-time Collaboration

## Overview

**Topic**: Real-time collaborative editing
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Day 21 completed
- Understanding of WebSockets
- Conflict resolution concepts

## Time Breakdown

- **Learn (20 min)**: Collaboration algorithms
- **Design (30 min)**: Complete system
- **Reflect (10 min)**: Trade-off analysis

## Real-time Collaboration Concepts

### The Challenge

Multiple users editing same document simultaneously:

- Edits happen concurrently
- Network latency varies
- Users expect real-time sync

### Approaches

**Operational Transformation (OT)**:

- Transform operations based on concurrent changes
- Used by Google Docs
- Complex but battle-tested

**Conflict-free Replicated Data Types (CRDT)**:

- Data structures that merge automatically
- Eventually consistent
- Used by Figma

### OT Example

User A types "Hello" at position 0
User B deletes character at position 2

If B's operation arrives first at A:

- Transform A's insert: still position 0
- Result: "Hello" then delete at position 2 → "Helo"

### WebSocket Architecture

- Persistent connections for real-time
- Server broadcasts changes
- Client applies transformations

## Design: Google Docs Clone

### Requirements

- Real-time collaborative editing
- Support 100+ concurrent editors
- Offline support with sync
- Version history
- Comments and suggestions

### Tasks

### Task 1: Data Model (10 min)

Design document structure:

```
Document:
  - doc_id: uuid
  - title: string
  - owner_id: uuid
  - created_at: timestamp

Operations:
  - op_id: uuid
  - doc_id: uuid
  - user_id: uuid
  - type: insert|delete|format
  - position: int
  - content: string
  - timestamp: timestamp
  - version: int
```

### Task 2: Real-time Architecture (15 min)

**Components**:

1. **Document Service**: CRUD operations
2. **Collaboration Service**: Handle real-time edits
3. **WebSocket Gateway**: Manage connections
4. **OT Engine**: Transform operations
5. **Storage**: Document persistence

**Flow**:

1. User connects via WebSocket
2. Load document, join session
3. User makes edit
4. Send operation to server
5. Server transforms if needed
6. Broadcast to all users
7. Clients apply operation

### Task 3: Conflict Resolution (10 min)

**OT Transformation Rules**:

| Op1         | Op2         | Transform         |
| ----------- | ----------- | ----------------- |
| Insert at 5 | Insert at 3 | Op1 position += 1 |
| Insert at 5 | Delete at 3 | Op1 position -= 1 |
| Delete at 5 | Insert at 3 | Op1 position += 1 |
| Delete at 5 | Delete at 5 | Op1 becomes no-op |

### Task 4: Offline Support (10 min)

**Strategy**:

1. Cache document locally
2. Queue operations offline
3. On reconnect: sync with server
4. Handle conflicts

**Merge strategy**: ******\_\_\_******

### Task 5: Version History (5 min)

- Store operations or snapshots?
- How to reconstruct past versions?
- Storage efficiency?

## Output Requirements

- [ ] Data model designed
- [ ] Real-time architecture drawn
- [ ] Conflict resolution rules defined
- [ ] Offline support planned
- [ ] Version history approach

## Success Criteria

- [ ] Understand OT/CRDT concepts
- [ ] Can design real-time collaboration
- [ ] Know WebSocket architecture
- [ ] Handle offline and conflicts

## Next Steps

Tomorrow: **Day 23 - Design: Dropbox** - File sync at scale

## Social Post Template

"Day 22/31 System Design: Google Docs! Operational Transformation for concurrent editing, WebSocket for real-time, offline support with sync. Collaboration is complex! #SystemDesign #RealTime"

## Notes

_Your personal observations go here._

---
