# Day 19: Design Video Streaming (YouTube/Netflix)

## Overview

**Topic**: Video streaming architecture at scale
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Day 18 completed
- Understanding of CDNs
- Basic video encoding knowledge

## Time Breakdown

- **Learn (20 min)**: Video streaming concepts
- **Design (30 min)**: Complete system
- **Reflect (10 min)**: Optimization strategies

## Video Streaming Concepts

### Video Processing Pipeline

1. **Upload**: Original video received
2. **Transcode**: Convert to multiple formats/resolutions
3. **Package**: Create streaming segments
4. **Store**: Save to object storage
5. **Distribute**: Push to CDN edge servers

### Streaming Protocols

| Protocol | Description                  | Use Case       |
| -------- | ---------------------------- | -------------- |
| HLS      | HTTP Live Streaming (Apple)  | iOS, Safari    |
| DASH     | Dynamic Adaptive Streaming   | Cross-platform |
| RTMP     | Real-Time Messaging Protocol | Live streaming |

### Adaptive Bitrate (ABR)

- Multiple quality levels (360p, 720p, 1080p, 4K)
- Client switches based on bandwidth
- Smooth playback experience

### Video Segments

- Video split into 2-10 second chunks
- Each chunk available in multiple qualities
- Manifest file lists all segments

## Design: YouTube-Scale Video Platform

### Requirements

- 2 billion users
- 500 hours video uploaded/minute
- Millions concurrent viewers
- Global availability

### Tasks

### Task 1: Upload Pipeline (10 min)

Design video upload flow:

1. **Upload Service**: Receive video
2. **Transcoding Service**: Multiple resolutions
3. **Storage**: Object storage (S3)
4. **Metadata Service**: Video info

**Transcoding outputs**:
| Resolution | Bitrate | File size (1hr) |
|------------|---------|-----------------|
| 360p | | |
| 720p | | |
| 1080p | | |
| 4K | | |

### Task 2: Streaming Architecture (15 min)

**Components**:

1. **Video Service**: Metadata, URLs
2. **CDN**: Edge delivery
3. **Origin Servers**: Source for CDN
4. **Manifest Generator**: HLS/DASH manifests

**Playback flow**:

1. Client requests video
2. Get manifest URL
3. Fetch manifest
4. Download segments from nearest CDN
5. Adaptive quality switching

### Task 3: CDN Strategy (10 min)

**Edge locations**: Global distribution

**Caching**:

- Popular videos: Cached everywhere
- Long tail: Pulled on demand
- Cold start: Pre-warm for expected viral content

**Cache hit target**: \_\_\_\_%

### Task 4: Live Streaming Addition (10 min)

Differences for live:

- Real-time transcoding
- Lower latency requirements
- No full manifest upfront

**Latency targets**:
| Type | Latency |
|------|---------|
| Traditional live | |
| Low-latency live | |
| Real-time (WebRTC) | |

### Task 5: Storage Estimation (5 min)

- 500 hours/minute uploaded
- Average video: 10 minutes
- Storage per minute of video (all qualities): ~500MB

**Daily storage**: **_
**Yearly storage**: _**

## Output Requirements

- [ ] Upload pipeline designed
- [ ] Streaming architecture drawn
- [ ] CDN strategy defined
- [ ] Live streaming differences noted
- [ ] Storage calculated

## Success Criteria

- [ ] Understand video processing pipeline
- [ ] Know streaming protocols
- [ ] Can design at YouTube scale
- [ ] Understand ABR and CDN role

## Next Steps

Tomorrow: **Day 20 - Design: Uber/Lyft** - Location-based services

## Social Post Template

"Day 19/31 System Design: Video Streaming (YouTube scale)! Upload → Transcode → Package → CDN → Play. HLS, DASH, adaptive bitrate. 500 hours/minute uploaded! #SystemDesign #VideoStreaming"

## Notes

_Your personal observations go here._

---
