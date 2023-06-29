---
title: "Federal Level Name Matching Project"
draft: false
enableToc: false
creation_date: 2023-06-28
---
# Timeline

1. **Algorithm Stage** | *2022.04-2022.08*
	1. Explored and designed an algorithm to do an initial fuzzy match.
	2. Meeting Memo Explored FY2001 | *2022.05.06*
		1. 4 Types of match cases![[notes/images/Federal Level Name Matching Project_image_1.png|300]]
		2. Algorithm Details ([RapidFuzz](https://pypi.org/project/rapidfuzz/))
			1. **Cleaning**: Clean company-name-variables (both CRSP and USAspending) with [Cleanco](https://pypi.org/project/cleanco/) package
			2. **CRSP**: Merge each firm-FY observation within +1/-1 fiscal year with the historical name file
			3. [ ] **Methodology**: We **enumerate** each observation-year from USAspending data to match a subset of CRSP name file with the same initial letter #todo : verify if we later use this methodology (a subset that shares the same initial letter)
			4. Cutoffs
				1. Score Cutoff = 0
				2. Number Limit = 25 (Top 25 match cases will be returned)
		3. RapidFuzz Score Distribution![[notes/images/Federal Level Name Matching Project_image_2.png|300]]![[notes/images/Federal Level Name Matching Project_image_3.png|400]]
	3. Meeting Memo | *2022.05.30-06.28*
		1. Working Language![[notes/images/Federal Level Name Matching Project_image_4.png]]
		2. Matching Diagram![[notes/images/Federal Level Name Matching Project_image_5.png]]![[notes/images/Federal Level Name Matching Project_image_6.png]]
		3. Matching Pipeline (FY2000 as an illustration)![[notes/images/Federal Level Name Matching Project_image_7.png]]
		4. Disposal Rule![[notes/images/Federal Level Name Matching Project_image_8.png]]
			1. [ ] #todo check the clean file generator code to formulate disposal rule
		5. List Match Algorithm![[notes/images/Federal Level Name Matching Project_image_9.png]]
		6. Have more examples in the file "20220530-0628_FuzzyMatch_Presentation.pptx"
2. **Manual Matching Stage** | *2022.08-2022.12*
	1. Provided a detailed brochure for student helpers to match the company names manually | *2022.08* 
	1. Student helpers manually matched the company names and conducted 2 rounds of crosscheck | *2022.08-2022.12*
	2. Meeting Memo | *2022.08.10*
		1. Grouping logic of manual cleaning files for student helpers: Group by CRSP name and each CRSP maps to multiple USAspending![[notes/images/Federal Level Name Matching Project_image_10.png]]![[notes/images/Federal Level Name Matching Project_image_11.png]]
		2. 
3. **Checking and mapping Stage** | *2022.12-2023.03*
	1. Handled multiple mapping cases and selected useful variables
	2. Generated a [merged file](https://drive.google.com/drive/folders/0B6mr-vLPsBgwfm9JeXNDZ3k2dWJhMjhEcExGNGRkWHhGMThtSWFZMy1wU0cybzdtclJrV2c?resourcekey=0-UHb7-q10NrZihG-6L_v5PQ&usp=drive_link) with selected variables

# File names
**exploratary_rapidfuzz.csv**
> Finished and exported first round output for year 2000 as exploratary_rapidfuzz.csv with rapid fuzz algorithm.
> May 24, 2022, Fuzzy Match Project-Yifeng Week 2 Progress Report



# High-Level Learning 
- [ ] #todo Move them elsewhere
1. Always create functions, and maybe it'd be good to write function and implementation separately.
2. Make good slides so that after some time it's simple to review

