---
title: "20220701 USAspending Meeting"
draft: false
enableToc: false
creation_date: 2023-07-01
---

# Presentation

## Federal Level
> Last Meeting Q&A

3. Action
	1. [x] Improve Federal Variable List
	2. [x] Add “Award Type” variable to Fed-level data
	3. After understanding “types” of data reported in Fed level data, give a definition of amount and how we can use them
	4. Give a breakdown (distribution) on amount (contract value) by 9 groups of award data types (to understand the relevancy/representation/importance of each type)

**About Salaries**
>[!faq]- Employee salaries in non-award data
>
>The employees refer to **government employees**, according to "For example, account spending includes money used to **pay federal government employees’ salaries**. This spending is not included in award spending" from [Federal Spending Guide](https://www.usaspending.gov/federal-spending-guide)

---

**Definition of Direct Payment**
>[!info]- Direct Payment (A type of Financial Assistance)
>
>A cash payment made by the federal government to an individual, **a private firm**, or another private institution.

> [!info]- Direct Payment for Specified Use
> 
> **Financial assistance** provided by the federal government directly to individuals, **private firms**, and other private institutions for a particular activity. 
> 
> To receive this assistance, the recipient must perform certain agreed-upon activities and meet certain milestones. **Direct payments don’t include solicited contracts for the procurement of goods and services for the government**.

>[!info]- Direct Payment with Unrestricted Use
>
>**Financial assistance** provided by the federal government directly to beneficiaries who meet certain federal **eligibility requirements**. This type of assistance doesn’t place any restrictions on how the recipient spends the money. Some examples of direct payments include **retirement, pension, and compensatory programs**.

---

**How to locate IDV/Award** type?
> [!tip] "award_or_idv_flag" used to partition procurement

---

**About dummy for Procurement and Financial Assistance Data**

We're using a table called "transaction_fpds" (merged with "transaction_normalized", which contains variables "transaction_fabs" as well. The dummy is "is_fpds" from the database. The main reason is action date)(**2021 technical issue not merged with normalized**, can merge ourselves to make the action date more tractable). Thus only procurement data is included. The data level is **transaction-level**. (**fabs not joined, need to verify**).

>[!info]- File D1: Federal Procurement Data System (FPDS)
>
>This is where federal contracting officials submit **transaction-level** data for **procurement**. It contains
>1. obligation
>2. transaction description
>3. action date
>4. awarding agency
>5. recipient code (UEI)
>6. recipient location
>7. place of performance
>8. Industry (NAICS)
>9. product or service
>10. type of set aside

> [!info]- Transaction
> 
> A transaction can be the initial contract, grant, loan, or insurance award or any amendment or modification to that award.

---

**About Amount**

>[!faq]- Obligations v.s. Outlays
>
> 1. Obligation: When Fed promised to pay
> 2. Outlay: When Fed's money is *actually* paid out
> 
>Usually it's more common to **measure** spending by **obligation** over outlays.

> Note: Outlays are not available in our current table. Outlay data are available in sources File A and File B (See below).

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

---

**About data potential**

Our current link file looks like
![[notes/images/20220701 USAspending Meeting_image_1.png]]
Where 
>[!tip]- "usa_id" from match pair list
>
>It's concatenated by "awardee_or_recipient_uniqu"+"fiscal year"
>The first variable is **the id we used for name matching** between CRSP and USA Spending. A 9-digit number assigned by Dun and Bradstreet (D&B) referred to as the DUNS® number that uniquely identifies an awardee or recipient. **From 2022, SAM switched from DUNS to UEI**.

>[!tip]- Unique Entity Identifier (UEI) From SAM.gov
>
>The Unique Entity Identifier (UEI) for an awardee or recipient is an alphanumeric code created in the System for Award Management (SAM.gov) that is used to uniquely identify specific **commercial, nonprofit, or business entities** registered to do business with the federal government.
>
>**From 2022, SAM switched from DUNS to UEI**.

> [!tip]- "awardee_or_recipient_uniqu" in our data set: DUNS
> 
> DUNS stands for Data Universal Numbering System. It is a unique 9-digit identification number assigned to a company or organization by Dun & Bradstreet, Inc. A DUNS is required to register in the System for Award Management (SAM). An organization must be registered in SAM (and obtain a DUNS) to do business with the federal government. There is a separate DUNS number for each business location in the Dun & Bradstreet database. The DUNS number is random, and specific digits have no significance.
> 
> ![[notes/images/20220701 USAspending Meeting_image_2.png]]
> **From 2022, SAM switched from DUNS to UEI** ([link](https://sam.gov/content/duns-uei)).

Other table that could be linked by **awardee_or_recipient_uniqu**
1. broker_subaward
2. duns and historical_parent_duns: can use to get "uei" and "ultimate_parent_uei"
3. source_assistance_transaction
4. source_procurement_transaction
5. **transaction_fabs**

> [!info]- File D2: Financial Assistance Broker Submission (FABS)
>
>The Financial Assistance Broker Submission (FABS) is how federal agencies submit [transaction-level](https://www.usaspending.gov/data-sources?glossary=transaction&) data for [financial assistance](https://www.usaspending.gov/data-sources?glossary=financial-assistance&) awards to USAspending.gov. It contains information about 
>1. award transaction obligation
>2. [award transaction description](https://www.usaspending.gov/data-sources?glossary=transaction-description&)
>3. [action date](https://www.usaspending.gov/data-sources?glossary=action-date&)
>4. [awarding agency](https://www.usaspending.gov/data-sources?glossary=awarding-agency&)
>5. [recipient code](https://www.usaspending.gov/data-sources?glossary=unique-entity-identifier-uei&)
>6. [recipient location](https://www.usaspending.gov/data-sources?glossary=recipient-location&)
>7. [place of performance](https://www.usaspending.gov/data-sources?glossary=primary-place-of-performance&)
>8. [assistance listing](https://www.usaspending.gov/data-sources?glossary=assistance-listings-cfda-program&)

---

**About Amount and id**

for "transaction_fpds" table
1. **(KEY)** id: "transaction_id"
2. awardee id: "awardee_or_recipient_uniqu"
3. amount: "federal_action_obligation"

>[!tip]- Main amount: "federal_action_obligation"
>
>Amount of Federal government’s obligation, de-obligation, or liability, in dollars, for an award transaction.


---
**About procurement distribution and definition of subtypes**
![[notes/images/20220701 USAspending Meeting_image_3.png]]
![[notes/images/20220701 USAspending Meeting_image_4.png]]
![[notes/images/20220701 USAspending Meeting_image_5.png]]![[notes/images/20220701 USAspending Meeting_image_6.png]]![[notes/images/20220701 USAspending Meeting_image_7.png]]
> [!tip] "award_or_idv_flag" used to partition procurement

> [!info]- Procurement: IDV Type
> 
> - A: GWAC – Government-Wide Agency Contract approved by OMB
> - B: IDC – Indefinite delivery contract
> - C: FSS – GSA or VA Federal Supply Schedule
> - D: BOA – Basic Ordering Agreement
> - E: BPA – Blanket Purchase Agreement

>[!tip]- IDV-A: GWAC – Government-Wide Agency Contract approved by OMB
>
>Government-Wide Acquisition Contract (GWAC) is a **multi-agency** contract. It offers Information Technology (IT) services to agencies across the government. It is an Indefinite Delivery Vehicle (IDV) for certain types of IT work:
>- Systems design
>- Software engineering
>- Information assurance
>- Enterprise architecture
>
>Vendors compete for the initial contracts. Once selected, they are eligible to compete further for agency-specific tasks.
>
>[Official Definition](https://www.gsa.gov/portal/content/104874)

>[!tip]- IDV-B: IDC – Indefinite delivery contract
>
>Indefinite Delivery Contract (IDC) facilitates the delivery of supply and service orders during a set timeframe. This type of contract is awarded to one or more vendors.
> 
> Types of IDC's Include:
> 
> - Indefinite Delivery / Definite Quantity Contract
> - Indefinite Delivery / Requirements Contract
> - Indefinite Delivery / Indefinite Quantity (IDIQ) Contract
>   
>   [Official Definition](https://www.fpds.gov/help/Indefinite_Delivery_Contract.htm)

>[!tip]- IDV-C: FSS – GSA or VA Federal Supply Schedule
>
>The Federal Supply Schedule (FSS) is a listing of contractors that have been awarded a contract by GSA that can be used by all federal agencies. This is also known as a Multiple Award Schedule (MAS).
>
>404 Official Definition

>[!tip]- IDV-D: BOA – Basic Ordering Agreement
>
>A Basic Ordering Agreement (BOA) is a type of Indefinite Delivery Vehicle (IDV). **It is not a contract**; it is a written understanding between government and contractor. It details the supplies or services offered. It also details pricing and delivery for future orders.
> 
> BOA's can speed up contracting when requirements are uncertain. For instance, when specifications, quantities, and prices are not yet known.
> 
> These agreements can also help the government achieve economies of scale for part orders. For the contractor, they can lessen lead-time, enable a larger inventory investment, and lessen old inventory.
> 
> [Official Definition](https://www.fpds.gov/help/Create_a_BOA.htm)

>[!tip]- IDV-E: BPA – Blanket Purchase Agreement
> 
> A Blanket Purchase Agreement (BPA) is a method federal agencies use to **make repeat purchases of supplies or services**. A type of Indefinite Delivery Vehicle (IDV), a BPA operates by setting up a "charge account" with trusted vendors. Both agencies and vendors often prefer BPAs because they help speed up the process of repeated purchases. Once a BPA is set up, repeat purchases are easy for both sides.
> 
> A BPA is an agreement with an individual agency, meaning only a handful of offices can place orders on a BPA. A BPA can be awarded to a set of vendors, who will then be able to bid on upcoming orders. A BPA can be set up with or without General Services Administration (GSA) schedules. Without GSA schedules, orders are capped at the Simplified Acquisition Threshold (SAT) of $100,000.
> 
> Examples of BPAs:
> 
> - Agency A establishes a BPA with a computer manufacturer for repeat laptop purchases
> - Agency B establishes a BPA with a graphic design agency for design of brochures and event signage

>[!info]- Procurement: Award Type
>
> - A: BPA Call – call against a blanket purchase agreement
> - B: Purchase order
> - C: Delivery Order – delivery order or task order under an Indefinite Delivery Vehicle
> - D: Definitive contract

>[!tip]- A: BPA Call – call against a blanket purchase agreement

> [!tip]- B: Purchase order
> 
> A Purchase Order is an offer by the government established to buy supplies or services, including construction and research and development, upon specified terms and conditions, using simplified acquisition procedures.

>[!tip]- C: Delivery Order – delivery order or task order under an Indefinite Delivery Vehicle

>[!tip]- D: Definitive contract
>
>A Definitive Contract is a mutually binding legal relationship obligating the seller to provide the supplies or services (including construction) and the buyer to pay for them. It includes all types of commitments that obligate the Government to an expenditure of appropriated funds and that, except as otherwise authorized, are in writing. In addition to bilateral instruments, contracts include (but are not limited to) 
>1. awards and notices of awards; 
>2. job orders, or task letters, issued under **basic ordering agreements**; 
>3. letter contracts; 
>4. orders, such as **purchase orders**, under which the contract becomes effective by written acceptance or performance; 
>5. and bilateral contract modifications.


---
**About award and transaction** and **an example of an award**

> [!tip]- Award ID
> 
> A unique identification number for each individual award. An award may be a contract, grant, loan, insurance, and direct payment.
> 
> ![[Excalidraw/USAspending 2023-06-29 20.33.23.excalidraw.light.svg]]


---

## State Level
> Last Meeting Q&A
2. Verify the State level data
	1. If payment data cover both contract payment and direct payment 

**About cleaning**
1. I finished my part.
2. Have meeting tonight with Zhengliu to check his part.

# Discussion
**Fed-level checklist**
- [ ] Duplications in current (transaction id is **id**)
- [ ] Necessity to link to other tables?
- [ ] 2021 Data incomplete? (Can explore by "Action Date")
- [ ] across year case study for certain contracts?

**About state-level name matching**
![[Excalidraw/Federal Level Pipeline 2023-06-30 12.25.57.excalidraw.light.svg]]
1. How to automate the selection process?
2. Can prepare a case study for a state

# Todo
