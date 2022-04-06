# gh-metrics

A [`gh`](https://cli.github.com/) extension that provides summary pull request metrics.

- [Usage](#usage)
- [Metric definitions](#metric-definitions)
- [Influences](#influences)

## Usage

To install the extension use:

```console
$ gh extension install hectcastro/gh-metrics
```

Once installed, you can summarize all pull requests for the `cli/cli` repository over the last 10 days:

```console
$ gh metrics --owner cli --repo cli
┌──────┬─────────┬───────────┬───────────┬───────────────┬──────────────────────┬──────────┬──────────────┬───────────────────┬─────────────────────────┐
│   PR │ COMMITS │ ADDITIONS │ DELETIONS │ CHANGED FILES │ TIME TO FIRST REVIEW │ COMMENTS │ PARTICIPANTS │ FEATURE LEAD TIME │ FIRST APPROVAL TO MERGE │
├──────┼─────────┼───────────┼───────────┼───────────────┼──────────────────────┼──────────┼──────────────┼───────────────────┼─────────────────────────┤
│ 5408 │       1 │         3 │         5 │             1 │ 13h15m               │        0 │            2 │ 18h15m            │ 4h52m                   │
│ 5406 │       1 │         1 │         0 │             1 │ 18h5m                │        1 │            3 │ 18h19m            │ 14m                     │
│ 5405 │       1 │         2 │         8 │             1 │ 2h9m                 │        0 │            5 │ 19h0m             │ 16h38m                  │
│ 5390 │       7 │       183 │         0 │             3 │ 65h41m               │        1 │            4 │ 329h11m           │ 4h29m                   │
│ 5384 │       1 │        14 │         2 │             1 │ 6m                   │        4 │            6 │ 1h30m             │ 59m                     │
│ 5374 │       1 │        19 │         3 │             2 │ 11h20m               │        1 │            3 │ 11h33m            │ --                      │
│ 5370 │       1 │       105 │        20 │             7 │ 2h14m                │        0 │            2 │ 12h6m             │ 9h47m                   │
│ 5369 │      11 │      1518 │        20 │            11 │ 13m                  │        1 │            4 │ 23h39m            │ 23h26m                  │
│ 5367 │       1 │         3 │         2 │             2 │ 23h48m               │        0 │            1 │ 23h48m            │ --                      │
│ 5366 │       6 │       101 │       376 │            12 │ 2h8m                 │        1 │            2 │ 234h38m           │ 27m                     │
│ 5357 │       1 │         1 │         1 │             1 │ 6m                   │        0 │            5 │ 95h5m             │ 8m                      │
│ 5356 │       2 │        19 │         0 │             2 │ 96h14m               │        0 │            2 │ 112h8m            │ 3m                      │
│ 5345 │       1 │         1 │         1 │             1 │ 12h26m               │        2 │            5 │ 135h15m           │ 122h47m                 │
│ 5334 │       1 │      1493 │        55 │            16 │ 28h24m               │        1 │            2 │ 23m               │ 56h26m                  │
│ 5326 │       1 │        19 │         8 │             1 │ 312h53m              │        1 │            4 │ 313h8m            │ 14m                     │
│ 5316 │      11 │       820 │         1 │            10 │ 219h52m              │        1 │            3 │ 343h6m            │ 31m                     │
│ 5306 │       4 │        85 │        20 │             7 │ 396h39m              │        0 │            3 │ 397h11m           │ --                      │
│ 5272 │      15 │       466 │        61 │             9 │ 598h41m              │        3 │            3 │ 663h20m           │ 1m                      │
│ 5225 │       1 │       130 │         7 │             2 │ 742h4m               │        0 │            2 │ 930h48m           │ 188h34m                 │
│ 4921 │       2 │         6 │         3 │             3 │ 18h29m               │        2 │            3 │ 2492h13m          │ 7m                      │
└──────┴─────────┴───────────┴───────────┴───────────────┴──────────────────────┴──────────┴──────────────┴───────────────────┴─────────────────────────┘
```

Or, within a more precise window of time:

```console
$ gh metrics --owner cli --repo cli --start 2022-03-21 --end 2022-03-22
┌──────┬─────────┬───────────┬───────────┬───────────────┬──────────────────────┬──────────┬──────────────┬───────────────────┬─────────────────────────┐
│   PR │ COMMITS │ ADDITIONS │ DELETIONS │ CHANGED FILES │ TIME TO FIRST REVIEW │ COMMENTS │ PARTICIPANTS │ FEATURE LEAD TIME │ FIRST APPROVAL TO MERGE │
├──────┼─────────┼───────────┼───────────┼───────────────┼──────────────────────┼──────────┼──────────────┼───────────────────┼─────────────────────────┤
│ 5339 │       4 │         6 │         3 │             1 │ 2m                   │        0 │            3 │ 1h12m             │ 1h9m                    │
│ 5336 │       1 │         2 │         2 │             2 │ 7m                   │        0 │            1 │ 2h30m             │ 2h24m                   │
│ 5327 │       1 │         1 │         1 │             1 │ 41h57m               │        1 │            4 │ 65h44m            │ 23h36m                  │
└──────┴─────────┴───────────┴───────────┴───────────────┴──────────────────────┴──────────┴──────────────┴───────────────────┴─────────────────────────┘
```

Alternatively, instead of the default table output, output can be generated in CSV format:

```console
$ gh metrics --owner cli --repo cli --start 2022-03-21 --end 2022-03-22 --csv
PR,Commits,Additions,Deletions,Changed Files,Time to First Review,Comments,Participants,Feature Lead Time,First Approval to Merge
5339,4,6,3,1,2m,0,3,1h12m,1h9m
5336,1,2,2,2,7m,0,1,2h30m,2h24m
5327,1,1,1,1,41h57m,1,4,65h44m,23h36m
```

## Metric definitions

- **Time to first review**: The duration from when the pull request was created or marked *Ready for review* to when the first review against it was completed.
- **Feature lead time**: The duration from when the first commit contained in the pull request was created to when the pull request was merged.
- **First approval to merge**: The duration from when the first approval review is given to when the pull request is merged.

## Influences

Development of this extension was heavily inspired by [jmartin82/mkpis](https://github.com/jmartin82/mkpis).
