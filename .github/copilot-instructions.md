# AR Compass App - AI Coding Instructions

## Project Overview
This is a location-based augmented reality (AR) web application built with A-Frame, focusing on directional object placement. The app displays 3D models (e.g., Fuji Mountain and Osaka Castle) at specific bearings from the user's location, visible only when the device is oriented towards them.

## Architecture
- **Single HTML Entry**: `index.html` contains the entire app, including A-Frame scene, custom components, and scripts.
- **Core Components**:
  - `a-camera[gps-camera]`: Handles GPS positioning and camera controls.
  - Custom entities with `show-on-bearing`: Display objects based on device orientation relative to target coordinates.
  - Debug UI: Real-time GPS coordinates display at bottom-left.

## Key Workflows
- **Development**: Edit `index.html` directly; no build process required.
- **Testing**: Serve over HTTPS (required for GPS/AR permissions). Test on mobile devices with compass access.
- **Debugging**: Use browser console for logs (e.g., bearing calculations). Enable compass permissions via UI button on iOS.

## Project-Specific Patterns
- **Custom Component Registration**: Use `AFRAME.registerComponent` for behaviors like `show-on-bearing` (see lines 25-120 in `index.html`).
- **Bearing Calculations**: Implement `calculateBearing` and `calculateDestination` functions for geospatial math (examples in `show-on-bearing` and `direction-target` components).
- **Event-Driven Placement**: Listen to `gps-camera-update-position` events to dynamically set `gps-entity-place` attributes.
- **Orientation Handling**: Combine `deviceorientation` and `deviceorientationabsolute` events for cross-platform compass data.
- **Visibility Logic**: Objects are placed 30m ahead in the target direction and shown only within a 20-degree tolerance of the bearing.

## Dependencies & Integrations
- **A-Frame Ecosystem**: Core framework with AR.js for webcam AR, GPS components for location-based features.
- **External Scripts**: Loaded from CDNs (A-Frame, AR.js, GPS plugins). No local package management.
- **Cross-Component Communication**: Components share state via global event listeners and DOM attributes.

## Examples
- To add a new directional object: Copy the `a-entity` structure (lines 200-210), update latitude/longitude, and assign a unique GLTF model from `./assets/`.
- For custom bearing logic: Extend `calculateBearing` in a new component, ensuring 360-degree normalization.