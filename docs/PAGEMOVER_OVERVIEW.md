# PageMover: a visual SQL Server index and heap inspection tool

**Steven Wittek | Netherwood Data Partners**  
**Status:** Private-source developer preview. This page is a public technical showcase, not a download or a production recommendation.

## The idea

Traditional index-maintenance reports can tell an operator how fragmented an index appears, but it can be harder to picture where that information comes from or what the next operation will actually do. PageMover uses the look of a classic Windows disk defragmenter to make SQL Server index and heap diagnostics more tangible.

Its local interface supports catalog inventory, optional physical statistics and page-map inspection, index/heap and partition selection, a preview of generated SQL, explicit enablement for maintenance, and verification after attempted changes.

## What the screenshot shows

![Offline PageMover demonstration showing synthetic index pages and maintenance choices](../assets/pagemover-demo.png)

The image above is the application's **offline synthetic demo**, not a live database scan. The blue rectangles stand for fabricated 8 KiB page data, and the statistics are demonstration values. The application is shown by itself, with no browser tab strip, unrelated applications, or private connection information.

## Technical design

| Concern | Approach |
| --- | --- |
| SQL Server connection | Local ASP.NET Core service using Microsoft.Data.SqlClient |
| SQL analysis | Metadata, index/heap statistics, optional page-level inspection |
| User interface | HTML, CSS and JavaScript Canvas, with retro desktop styling |
| Action safety | Read-only analysis first; intentional maintenance mode; review SQL before execution |
| Auditability | Generated statements can be inspected and results verified |
| Local scope | No hosted service or public data collection is required for normal local operation |

## Operational limitations

- Index maintenance is capable of meaningful I/O, blocking and transaction log activity. It should first be evaluated in disposable development environments.
- Rebuild operations are offline in the current developer preview; no online or resumable rebuild support is claimed.
- Physical-page inspection uses an unsupported SQL Server mechanism and can be expensive.
- Cancellation may initiate SQL Server rollback, which can continue after the client stops.
- The demonstration screenshot does **not** prove performance improvements or that a production SQL Server instance was safely modified.

## Where this stands

The private implementation includes source code, a Windows packaging workflow, and existing documented automated tests. A separate public-release checklist covers the full source and commit history, security and licensing review, Windows verification, and approved screenshots. The code is not public yet.

[Read the product overview](https://netherwooddatapartners.com/products/sql-server-index-maintenance-visualizer/) · [Return to the portfolio](../README.md)
