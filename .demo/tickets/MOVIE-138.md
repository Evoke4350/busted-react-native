# MOVIE-138: Add "Save to Watchlist" feature on movie detail screen

**Status:** Open
**Priority:** P2 - High
**Type:** Feature
**Reporter:** Jordan Park (Product)
**Assignee:** Unassigned
**Sprint:** Sprint 14
**Labels:** `feature`, `detail-screen`, `save`, `watchlist`
**Epic:** User Engagement

---

## Description

Users should be able to save movies to a personal watchlist from the movie
detail screen. The Save tab currently exists but is a placeholder. We want to
wire it up with real functionality.

## User Story

As a user, I want to save movies to my watchlist from the detail screen so
that I can keep track of movies I want to watch later.

## Requirements

### Detail Screen (`app/movie/[id].tsx`)
- Add a bookmark/save icon button in the top-right area of the poster image
- Icon should toggle between outlined (not saved) and filled (saved) states
- Tapping should save/unsave the movie with haptic feedback
- Show a brief toast or visual confirmation when saved/unsaved

### Save Tab (`app/(tabs)/save.tsx`)
- Replace the placeholder with a grid of saved movies (same layout as home)
- Each movie card should show poster, title, and rating
- Tapping a saved movie navigates to its detail screen
- Empty state: "No saved movies yet. Browse and save movies you want to watch!"
- Pull-to-refresh support

### State Management
- Use React Context to manage the saved movies list
- Persist saved movies to AsyncStorage so they survive app restarts
- Expose `saveMovie`, `unsaveMovie`, and `isSaved` functions via the context

## Design Reference

See attached Figma JSON in `.demo/figma/watchlist-feature.json`

Key design specs:
- Save button: 40x40px, positioned top-right of poster with 16px padding
- Unsaved state: outline bookmark icon, semi-transparent white background
- Saved state: filled bookmark icon, accent purple (#AB8BFF) background
- Toast: bottom-center, 2s duration, dark background with white text
- Grid layout on Save tab: 3 columns, same as home screen movie grid

## Acceptance Criteria

- [ ] Bookmark button appears on movie detail screen
- [ ] Tapping toggles saved state with visual feedback
- [ ] Saved movies appear in the Save tab as a grid
- [ ] Saved movies persist across app restarts (AsyncStorage)
- [ ] Empty state shown when no movies are saved
- [ ] Navigation from Save tab to movie detail works correctly
- [ ] Removing a saved movie updates both the detail screen and Save tab

## Technical Notes

- Use `expo-haptics` (already installed) for tactile feedback on save/unsave
- Consider using `@react-native-async-storage/async-storage` for persistence
- The `MovieCard` component can be reused in the Save tab
- Context provider should wrap the app in `app/_layout.tsx`
