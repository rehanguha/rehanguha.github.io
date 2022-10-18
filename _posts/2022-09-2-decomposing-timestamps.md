---
layout: post
title: "Decomposing Timestamp"
excerpt: "This post shows us most possible ways to decompose the timestamp and other features."
tags: [Image, Mathematics, Code, CV]
categories: [Computer Vision, Code]
link: https://github.com/rehanguha/brisque
share: true
comments: true
mathjax: false
---

## Decomposing the Timestamp for Regression problems

Example ::  **2038-01-19 03:14:07**

- **timestamp**: The `timestamp` value that was decomposed. Example: 
- **timestamp_unix**: Unix format of `timestamp`.
- **diff**: The difference in seconds from the previous numeric `timestamp` value.

- **year**: The year component of the `timestamp`.
- **quarter**: The quarter of the year from the `timestamp` year.
- **halfyear**: First or second half of the year
- **month**: The month component of the `timestamp` with base 1 or base 0.
- **month.label**: The month label. January and ending with December.

- **hour**: The hour component of the `timestamp`.
- **minute**: The minute component of the `timestamp`.
- **second**: The second component of the `timestamp`.
- **hour12**: The hour component on a 12 hour scale.
- **am_pm**: Morning (AM) = 1, Afternoon (PM) = 2.
- **wday**: The day of the week with base 1 or base 0. Sunday = 1/0 and Saturday = 7/6.
- **wday.label**: The day of the week label. Sunday and ending with Saturday.
- **dayofmonth**: The day of the month it is same as the day from `timestamp`.
- **dayofquater**: The day of the quarter.
- **dayofyear**: The day of the year.
- **weekofmonth**: The week of the month.
- **week**: The week number of the year.
- **week2mod**: The modulus for bi-weekly frequency.
- **week3mod**: The modulus for tri-weekly frequency.
- **week4mod**: The modulus for quad-weekly frequency.

## References

Most of them are common deductions and some were searched online as well. But I felt that all the decomposition components were not available at a single blog or post...