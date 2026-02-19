# MOVIE-143: Users report all movie ratings show 0 or 1 out of 10

**Status:** Open
**Priority:** P1 - Critical
**Type:** Bug
**Reporter:** Alex Rivera (QA)
**Assignee:** Unassigned
**Sprint:** Sprint 14
**Labels:** `ui`, `detail-screen`, `data-display`

---

## Description

Multiple users have reported that movie ratings on the detail screen always
display as "0/10" or "1/10" regardless of the actual movie rating. For example,
"The Dark Knight" shows "1/10" when it should show "8/10".

## Steps to Reproduce

1. Open the app
2. Tap on any popular movie (e.g., one with a known high rating)
3. Observe the star rating badge on the detail screen

## Expected Behavior

The rating should reflect the TMDB `vote_average` value, rounded to the nearest
whole number. E.g., a movie with `vote_average: 8.2` should display "8/10".

## Actual Behavior

All movies display "0/10" or "1/10". The rating appears to be incorrectly
transformed before display.

## Screenshots

```
[Before]  ★ 0/10 (1,247 votes)    <- wrong
[Expected] ★ 8/10 (1,247 votes)    <- correct
```

Note: The vote COUNT displays correctly. Only the average is wrong.

## Technical Notes

The rating display is in `app/movie/[id].tsx`. The TMDB API returns
`vote_average` on a 0-10 scale. Check if there's an unnecessary
mathematical transformation being applied.

## Acceptance Criteria

- [ ] Movie ratings accurately reflect the TMDB `vote_average` value
- [ ] Ratings are rounded to the nearest whole number
- [ ] No regression on the movie card ratings (home screen)
