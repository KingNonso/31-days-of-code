# Day 23: Design Dropbox - File Sync

## Overview

**Topic**: File synchronization at scale
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Day 22 completed
- Understanding of distributed storage
- File system basics

## Time Breakdown

- **Learn (20 min)**: File sync concepts
- **Design (30 min)**: Complete system
- **Reflect (10 min)**: Optimization strategies

## File Sync Concepts

### Challenges

- Large files (GBs)
- Many files (millions)
- Bandwidth efficiency
- Conflict handling
- Multiple devices

### Key Techniques

**Chunking**:

- Split files into fixed-size chunks (4MB)
- Only sync changed chunks
- Deduplication across users

**Delta Sync**:

- Send only differences
- Efficient for large files with small changes

**Content-Addressable Storage**:

- Chunks identified by hash
- Same content → same hash → stored once

### Sync Strategies

- **Full sync**: Copy everything
- **Incremental sync**: Only changes
- **Bidirectional sync**: Changes go both ways

## Design: Dropbox Clone

### Requirements

- Sync files across devices
- Share files/folders
- 500M users, 2PB stored
- Handle large files efficiently
- Work offline

### Estimations

- 500M users × avg 2GB = 1PB storage
- Peak sync: 10M files/day
- Average file: 100KB

### Tasks

### Task 1: Architecture Overview (10 min)

**Components**:

1. **Sync Client**: Desktop/mobile app
2. **API Service**: Metadata operations
3. **Notification Service**: Real-time updates
4. **Chunk Service**: Handle file chunks
5. **Metadata DB**: File/folder info
6. **Block Storage**: Actual file chunks (S3)

### Task 2: File Upload Flow (10 min)

**Steps**:

1. Client detects file change
2. Split file into 4MB chunks
3. Hash each chunk
4. Check which chunks exist (dedup)
5. Upload only new chunks
6. Update metadata with chunk list
7. Notify other devices

**Design the flow diagram**

### Task 3: Sync Protocol (10 min)

**Metadata**:

```
File:
  - file_id: uuid
  - path: string
  - chunks: [chunk_hash, ...]
  - version: int
  - modified_at: timestamp

Chunk:
  - chunk_hash: sha256
  - size: int
  - storage_path: string
```

**Sync algorithm**:

1. Get local file list with versions
2. Get server file list with versions
3. Compare: local_only, server_only, conflict
4. Download/upload as needed

### Task 4: Conflict Resolution (10 min)

**Conflict scenarios**:

- Same file edited on two devices offline
- File deleted on one, edited on other

**Resolution strategy**:

- Keep both versions
- Rename: "file (conflicted copy)"
- User decides

### Task 5: Optimization (10 min)

**Bandwidth**:

- Compression before upload
- Delta sync for large files
- LAN sync (device-to-device)

**Storage**:

- Deduplication (same chunks across users)
- Compression
- Tiered storage (hot/cold)

## Output Requirements

- [ ] Architecture with all components
- [ ] Upload flow designed
- [ ] Sync protocol defined
- [ ] Conflict resolution strategy
- [ ] Optimizations documented

## Success Criteria

- [ ] Understand chunking and dedup
- [ ] Can design file sync system
- [ ] Know conflict handling
- [ ] Understand optimization strategies

## Next Steps

Tomorrow: **Day 24 - Design: Payment System** - Financial transactions

## Social Post Template

"Day 23/31 System Design: Dropbox! Chunking (4MB), delta sync, deduplication. Upload only changed chunks. 500M users, 2PB storage. File sync is harder than it looks! #SystemDesign #FileSync"

## Notes

_Your personal observations go here._

---
