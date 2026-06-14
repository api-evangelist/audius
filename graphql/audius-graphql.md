# Audius GraphQL Schema

This directory contains a conceptual GraphQL schema for the [Audius](https://audius.co/) decentralized music streaming platform, derived from the [Audius REST API](https://docs.audius.org/developers/api).

## Overview

Audius exposes a public REST API for querying tracks, users, playlists, search, streaming, and blockchain-layer data across its decentralized network. This schema translates those capabilities into a GraphQL type system covering the full breadth of the platform.

## Schema File

- `audius-schema.graphql` — Full GraphQL schema with 60+ named types.

## Type Categories

### Scalars
- `DateTime`, `URL`, `JSON`

### Enums
- `TrackGenre` — All supported music genres (Electronic, Hip-Hop/Rap, Jazz, etc.)
- `TrackMood` — Mood descriptors (Peaceful, Energizing, Aggressive, etc.)
- `PlaylistType` — PLAYLIST or ALBUM
- `ReactionType` — HEART, FIRE, SAD, REPOST
- `TrendingTimeRange` — DAY, WEEK, MONTH, ALL_TIME
- `FeedFilter` — ALL, ORIGINAL, REPOST
- `ExploreType` — TOP_TRACKS, UNDERGROUND, FEEL_GOOD_TRACKS, etc.
- `TransactionStatus` — PENDING, CONFIRMED, FAILED
- `NFTChain` — ETH, SOL

### Interfaces
- `Node` — Base interface with `id`
- `Timestamped` — `createdAt` / `updatedAt` fields

### Track Types
| Type | Description |
|------|-------------|
| `Track` | Root track node with sub-field resolvers |
| `TrackDetails` | Full track metadata (title, genre, mood, counts, user) |
| `TrackTitle` | Isolated title and permalink |
| `TrackArtwork` | Multi-resolution artwork URLs |
| `TrackGenreInfo` | Genre enum and label |
| `TrackMoodInfo` | Mood enum and label |
| `TrackDuration` | Duration in seconds and formatted string |
| `TrackPlayCount` | Play count per track |
| `TrackFavoriteCount` | Favorite/save count per track |
| `TrackRepostCount` | Repost count per track |
| `TrackTags` | List of string tags for a track |
| `TrackActivity` | Aggregated activity metrics with timestamp |
| `TrackSegment` | Audio segment with multihash and duration |
| `RemixDetails` | Tracks that this track remixes |
| `FieldVisibility` | Per-field visibility flags |

### Playlist Types
| Type | Description |
|------|-------------|
| `Playlist` | Root playlist node |
| `PlaylistDetails` | Full playlist metadata |
| `PlaylistArtwork` | Multi-resolution artwork URLs |
| `PlaylistTrack` | Track within a playlist with metadata |

### Album Types
| Type | Description |
|------|-------------|
| `Album` | Root album node |
| `AlbumDetails` | Full album metadata including UPC |
| `AlbumTracks` | Ordered list of tracks within an album |

### User Types
| Type | Description |
|------|-------------|
| `User` | Root user node |
| `UserDetails` | Full user profile data |
| `UserHandle` | Isolated handle and verification |
| `UserBio` | Bio, website, and donation URL |
| `UserLocation` | User's declared location |
| `UserBadges` | Verified, deactivated, and feature flags |
| `UserProfilePicture` | Multi-resolution profile picture URLs |
| `UserCoverPhoto` | Cover photo URLs |
| `FollowerDetails` | Paginated follower list for a user |
| `FollowingDetails` | Paginated following list for a user |

### Feed Types
| Type | Description |
|------|-------------|
| `Feed` | Root feed for a user |
| `FeedDetails` | Paginated feed items with filter |
| `FeedItem` | Individual feed entry (track, playlist, or user action) |
| `FeedActivity` | Activity record tied to a feed item |

### Explore Types
| Type | Description |
|------|-------------|
| `Explore` | Root explore node by type |
| `ExploreDetails` | Details for an explore category |
| `ExplorePlaylist` | Playlist with rank and score in explore |

### Trending Types
| Type | Description |
|------|-------------|
| `Trending` | Root trending node |
| `TrendingDetails` | Details for a trending query |
| `TrendingTrack` | Track with rank, score, genre, and time range |
| `TrendingPlaylist` | Playlist with rank, score, and time range |

### Stream Types
| Type | Description |
|------|-------------|
| `Stream` | Root stream node for a track |
| `StreamDetails` | Stream availability and auth requirements |
| `StreamURL` | Resolved stream URL with expiry |

### Resolve Type
| Type | Description |
|------|-------------|
| `ResolveEndpoint` | Resolved entity from an Audius URL (track, user, playlist, album) |

### Tips & Reactions
| Type | Description |
|------|-------------|
| `Tip` | Root tip node |
| `TipDetails` | Full tip metadata including sender, receiver, amount |
| `Reaction` | Root reaction node |
| `ReactionDetails` | Full reaction metadata including type and sender |

### Blockchain / Web3
| Type | Description |
|------|-------------|
| `BlockchainTransaction` | Generic on-chain transaction record |
| `SolanaTransaction` | Solana-specific transaction with instructions and logs |
| `NFTTrack` | Track minted as an NFT with chain, contract, and token ID |
| `Token` | $AUDIO or other protocol token metadata |
| `APIKey` | API key record with owner and rate limit |

### Connections / Pagination
- `PageInfo` — Standard pagination metadata
- `TrackConnection`, `UserConnection`, `PlaylistConnection`, `TipConnection`

### Search
- `SearchResults` — Unified search across tracks, users, playlists, and albums

## Source API

- Documentation: https://docs.audius.org/developers/api
- Base URL: https://api.audius.co
- SDK: https://docs.audius.org/developers/sdk
- Open Source: https://github.com/AudiusProject
