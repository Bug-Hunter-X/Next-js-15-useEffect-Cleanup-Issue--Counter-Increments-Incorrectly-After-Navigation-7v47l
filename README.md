# Next.js 15 useEffect Cleanup Issue

This repository demonstrates a bug in a Next.js 15 application where a counter on the About page continues to increment even after navigating away from the page and returning.  This is likely due to an improper cleanup in the useEffect hook.

## Bug Description

The `useEffect` hook in `pages/about.js` uses `setInterval` to update a counter. However, the cleanup function (`return () => clearInterval(interval);`) doesn't reliably stop the interval when the component unmounts, resulting in multiple intervals running concurrently, causing an inaccurate count.

## Reproduction Steps

1. Clone this repository.
2. Install dependencies: `npm install`
3. Run the development server: `npm run dev`
4. Navigate to `/about`.
5. Observe the counter incrementing.
6. Navigate away from `/about` (e.g., to `/`).
7. Navigate back to `/about`.
8. Notice the counter continues incrementing from the previous value, instead of resetting to 0.  The count is faster than it should be due to multiple intervals running simultaneously.

## Solution

The solution involves ensuring the `setInterval` is correctly cleared in the cleanup function.  See `aboutSolution.js` for the corrected code.