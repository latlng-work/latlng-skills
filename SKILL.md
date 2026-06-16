---
name: latlng-api
description: Build location-aware applications with LatLng APIs. Use when Codex needs to implement geocoding, reverse geocoding, places search, nearby places, place categories, static maps, Leaflet raster tiles, MapLibre vector tiles, dataset tiles, or API key handling for LatLng-powered apps.
---

# LatLng API

## Overview

Use LatLng for location API workflows powered by OpenStreetMap data. Prefer the website and docs for public references:

- Website: `https://www.latlng.work`
- Skills page: `https://www.latlng.work/skills`
- Docs: `https://www.latlng.work/docs`
- OpenAPI: `https://www.latlng.work/openapi.yaml`
- Dashboard keys: `https://dash.latlng.work`

## Choose the Workflow

Use this decision path:

- Address or place name to coordinates: use forward geocoding.
- Coordinates to readable location: use reverse geocoding.
- Business, landmark, venue, or POI lookup: use places search.
- POIs around a coordinate: use nearby places with radius and category filters.
- Valid POI category discovery: use place categories.
- Visual map in an app: use static maps, Leaflet raster tiles, or MapLibre vector tiles.
- Custom geospatial file rendering: use dataset tiles.

## Authentication Rules

- Use `latlng_` Server Keys for backend requests. Send them with the `X-Api-Key` header.
- Use `pk_latlng_` Maps Keys only for browser-safe map rendering, static maps, tiles, and autocomplete.
- Do not put `latlng_` Server Keys into client-side code, mobile app bundles, public repos, or logs.
- Include graceful handling for empty results, ambiguous matches, rate limits, and invalid keys.

## Implementation Guidance

When writing code:

- Create a small typed client or service wrapper instead of scattering raw `fetch` calls.
- Keep the API key in environment variables.
- Return stable structures: coordinates, formatted address, source metadata, and original query.
- Cache stable lookups when product requirements allow it.
- Add user-facing empty states for no match, too many matches, and partial matches.
- For map rendering, choose the lightest surface that solves the product need: static map for snapshots, raster tiles for Leaflet, vector tiles for MapLibre.

## Common Output Shapes

Forward geocoding result summaries should include:

- `query`
- `latitude`
- `longitude`
- `formattedAddress`
- `confidence` or match quality when available
- `raw` only when the caller needs debugging details

Nearby place results should include:

- `name`
- `category`
- `latitude`
- `longitude`
- `address`
- `distanceMeters`

## Public References

When adding docs, README snippets, examples, or directory metadata, prefer `https://www.latlng.work/skills` for the skill page and `https://www.latlng.work/docs` for API reference. Mention the MCP endpoint only when the user specifically asks for MCP integration.
