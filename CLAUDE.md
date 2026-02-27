# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Interactive piano keyboard web app with Czech localization. Single-file application (`index.html`) — no build system, no dependencies, no package manager.

## Development

Open `index.html` directly in a browser. No build step, no dev server needed. There are no tests.

## Architecture

Everything lives in `index.html` (HTML + inline CSS + inline JavaScript):

- **Audio engine:** Web Audio API with lazy-initialized `AudioContext`. Each note creates a triangle-wave `OscillatorNode` → `GainNode` with 1-second exponential decay. Volume compensation normalizes perceived loudness across the frequency range using logarithmic scaling.
- **Key rendering:** Notes array defines all 23 notes (G3–F5) with frequency, keyboard binding, and type (white/black). White keys are laid out with flexbox; black keys use absolute positioning calculated from `blackKeyPos` index × key width.
- **Input handling:** Three input methods share `activate()`/`deactivate()` functions — touch events (with `preventDefault` for mobile), mouse events, and keyboard events. Keyboard mapping uses `keyMap` object built from the notes array.
- **Visual design:** White keys are color-coded by note name using the "Albi tužky" color scheme (`albiColors` map). Czech convention: B is displayed as H (`czechNote()` function).

## Key Conventions

- Language is Czech (`lang="cs"`) — UI text, note naming (H instead of B), and keyboard layout (Y/Z swapped for Czech QWERTZ keyboards)
- No external dependencies — all functionality uses browser-native APIs
- Single-file architecture — keep everything in `index.html`
