---
title: "USAspending"
draft: false
enableToc: true
creation_date: 2023-06-27
---

# Terminology

## Obligations v.s. Outlays
1. Obligation: When Fed promised to pay
2. Outlay: When Fed's money is *actually* paid out
> Usually it's more common to **measure** spending by **obligation** over outlays.

## Data structure-related variables
> [!tip]- Transaction
> 
> A transaction can be the initial contract, grant, loan, or insurance award or any amendment or modification to that award.

> [!tip]- Award ID
> 
> A unique identification number for each individual award. An award may be a contract, grant, loan, insurance, and direct payment.
> 
> ![[Excalidraw/USAspending 2023-06-29 20.33.23.excalidraw.light.svg]]

> [!tip]- Procurement Instrument Identifier (PIID)
> 
> **Procurement**: A unique identifier assigned to a federal contract, purchase order, basic ordering agreement, basic agreement, and blanket purchase agreement. It is used to track the contract and any modifications or transactions related to it.

>[!tip]- Federal Award Identification Number (FAIN)
>
>An identification code assigned to a specific **financial assistance** award by an agency for tracking purposes. The FAIN is tied to that award (and **all future modifications to that award**) throughout the award's life. **Within an agency, FAINs are unique**; a new award must be issued a new FAIN. FAIN stands for Federal Award Identification Number, though the digits may be both letters and numbers.

> [!tip]- Unique Record Identifier (URI)
> 
> In USAspending.gov site context.


# Federal Data Structure

## Spending Categories
![[Excalidraw/USAspending 2023-06-29 16.19.52.excalidraw.light.svg]]
<!--%%[[Excalidraw/USAspending 2023-06-29 16.19.52.excalidraw.md|🖋 Edit in Excalidraw]], and the [[Excalidraw/USAspending 2023-06-29 16.19.52.excalidraw.dark.svg|dark exported image]]%%-->



## Spending Flow
![[Excalidraw/USAspending 2023-06-29 16.34.53.excalidraw.light.svg]]
<!--%%[[Excalidraw/USAspending 2023-06-29 16.34.53.excalidraw.md|🖋 Edit in Excalidraw]], and the [[Excalidraw/USAspending 2023-06-29 16.34.53.excalidraw.dark.svg|dark exported image]]%%-->


## Data Sources
![[Excalidraw/USAspending 2023-06-29 16.49.28.excalidraw.light.svg]]
<!--%%[[Excalidraw/USAspending 2023-06-29 16.49.28.excalidraw.md|🖋 Edit in Excalidraw]], and the [[Excalidraw/USAspending 2023-06-29 16.49.28.excalidraw.dark.svg|dark exported image]]%%-->
> [!info]- Agency Budget Execution (ABE)
> 
> Agency Budget Execution (ABE) information is compiled in SF 133 reports. It shows how federal agencies spent their funding, as required by **Office of Management and Buget's Circular A-11**.
> *Note*: smaller agencies not required to submit their account data submit their Budget Execution data to a different system.

>[!info]- Governmentwide Treasury Account Symbol Adjusted Balance System (GTAS)
>
>Governmentwide Treasury Account Symbol Adjusted Balance System (GTAS) is extracted by USAspending, used to generate **Treasury Account** balances. This is the system where agencies submit their ABE data.

> [!info]- Agency Financial Systems (AFS)
> 
> Agency Financial Systems (AFS) is where Federal Agencies tracked their **own finances** such as
> 1. Operational costs
> 2. employee salaries
> 3. spending for federal awards

> [!info]- File A: Account Balances
> 
> It's a part of the package of data required by **Data Act** to **submit** to USAspending.gov. It can be generated from GTAS. It contains
> 1. Budgetary resources
> 2. obligation
> 3. outlay data
> 
> It includes both award and non-award spending, and crosswalks with the SF 133 report.

>[!info]- File B: Account Breakdown by Program Activity & Object Class
>
>It's a part of the package submitted to USAspending.gov. It contains **obligation** and **outlay** data for all the relevant **Treasury Accounts**. It breakdowns by
>1. Program Activity
>2. Object Class
>3. Disaster Emergency Fund Code
>
> It includes both award and non-award spending data.

> [!info]- File C: Account Breakdown by Award
>
> It covers contract and financial assistance awards over the **lifetime** of those awards. Noted that File C only covers financial information details. Other non-financial details are in the **Files D1 and D2** where award **transactions** information including recipient names are stored. There are some **unlinked** award between C and D1 & D2. Refers to [Agency Submission Statistics Page](https://www.usaspending.gov/submission-statistics?tab=submissions&fy=2023&period=7) for unlinked statistics.

>[!info]- Governmentwide Award Systems (GAS)
>
>Governmentwide Award Systems (GAS) stores the detailed records of federal awards. It tracks **obligations** for award transactions and related data such as recipients, locations, and purposes. **Any individual award is composed of one or more transactions with a common Award ID**.
>
>![[Excalidraw/USAspending 2023-06-29 20.33.23.excalidraw.light.svg]]
<!--%%[[Excalidraw/USAspending 2023-06-29 20.33.23.excalidraw.md|🖋 Edit in Excalidraw]], and the [[Excalidraw/USAspending 2023-06-29 20.33.23.excalidraw.dark.svg|dark exported image]]%%-->

>[!info]- File D1: Federal Procurement Data System (FPDS)
>
>

# References
- [USAspending - Data Sources](https://www.usaspending.gov/data-sources)
- [USAspending - Data Use Guide](https://www.usaspending.gov/federal-spending-guide)
- [USAspending - Training Videos Get and Post API Request](https://www.usaspending.gov/training-videos)
- [Data Act - Award Type introduction](https://fedspendingtransparency.github.io/whitepapers/types/)

# Data Descriptions
- [Data Dictionary](https://www.usaspending.gov/data-dictionary)
- [Dataset Metadata](https://www.usaspending.gov/download_center/dataset_metadata)