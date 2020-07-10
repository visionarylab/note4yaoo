---
tags: [react, table]
title: note-react-table-faq
created: '2020-07-07T13:48:55.448Z'
modified: '2020-07-07T15:33:11.907Z'
---

note-react-table-faq

## faq

- How can I manually control the table state?
  - Occasionally, you may need to override some of the table state from a parent component or from somewhere above the usage of useTable. 
  - In this case, you can turn to `useTable` 's `useControlledState` option. 
  - This hook function is run on every render and allows you an opportunity to override or change the final table state in a safe way.
- How can I use the table state to fetch new data?
  - When managing your data externally or asynchronously (eg. server-side pagination/sorting/grouping/etc), you will need to fetch new data as the internal table state changes. 
  - With React Hooks, this is fantastically easier than it was before now that we have the `useEffect` hook. 
  - We can use this hook to "watch" the table state for specific changes and use those effects to trigger fetches for new data (or synchronize any other state you may be managing externally from your table component):
- How can I debounce rapid table state changes?
  - React Table has a few built-in side-effects of it's own (most of which are meant for resetting parts of the state when data changes). 
  - By default, these state side-effects are on and when their conditions are met, they immediately fire off actions that will manipulate the table state. 
  - Sometimes, this may result in multiple rapid rerenders (usually just 2, or one more than normal), and could cause any side-effects you have watching the table state to also fire multiple times in-a-row. 
  - To alleviate this edge-case, React Table exports a `useAsyncDebounce` function that will allow you to debounce rapid side-effects and only use the latest one.
  - A good example of this when doing server-side pagination and sorting, 
    - a user changes the `sortBy` for a table and the `pageIndex` is automatically reset to 0 via an internal side effect. 
    - This would normally cause our effect below to fire 2 times, but with `useAsyncDebounce` we can make sure our data fetch function only gets called once
- How do I stop my table state from automatically resetting when my data changes?
  - Most plugins use state that should normally reset when the data sources changes, 
  - but sometimes you need to suppress that from happening if you are filtering your data externally, or immutably editing your data while looking at it, or simply doing anything external with your data that you don't want to trigger a piece of table state to reset automatically.
  - For those situations, each plugin provides a way to disable the state from automatically resetting internally when data or other dependencies for a piece of state change. 
  - By setting any of them to false, you can stop the automatic resets from being triggered.
