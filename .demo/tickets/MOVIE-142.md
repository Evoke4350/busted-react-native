# MOVIE-142: Search trending data not updating

**Status:** Open
**Priority:** P2 - High
**Type:** Bug
**Reporter:** Sarah Chen (Backend)
**Assignee:** Unassigned
**Sprint:** Sprint 14
**Labels:** `data-integrity`, `search`, `analytics`

---

## Description

The trending movies section on the home screen is not reflecting actual user
search behavior. The Appwrite `search_counts` collection shows stale data -
search terms are either not being recorded or are being recorded with the wrong
movie association.

## Steps to Reproduce

1. Open the app and go to the Search tab
2. Search for "Inception"
3. Note the results appear correctly on screen
4. Check the Appwrite dashboard - the search count for "Inception" was NOT
   incremented, or it was incremented with data from a previous search

## Expected Behavior

When a user searches for a movie and results are displayed, the
`updateSearchCount` function should record the search term along with the
first result's data in Appwrite.

## Actual Behavior

The `updateSearchCount` call appears to fire, but it uses movie data from the
*previous* search rather than the current one. On the very first search after
app launch, it doesn't fire at all because there are no previous results.

## Technical Notes

The search flow is in `app/(tabs)/search.tsx`. The debounced effect calls
`loadMovies()` and then checks `movies` state to call `updateSearchCount`.
Something seems off with the timing - the analytics call might be racing
against the data fetch.

## Acceptance Criteria

- [ ] Search count is correctly incremented for each search term
- [ ] The movie associated with the search term matches the first result
- [ ] First search after app launch correctly records data
- [ ] Existing debounce behavior (500ms) is preserved
