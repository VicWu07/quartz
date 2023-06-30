---
title: "20220318_MergeFile.ipynb"
draft: false
enableToc: false
creation_date: 2023-03-18
---


Use a selected variable list ("0319_var.csv") to merge between "0202_Full_PairList_with_Size.csv" and USAspending_table "transaction_fpds" (Procurement data)

1. Create a "Match_List" by merging on "awardee_or_recipient_uniqu" and fiscal year, resulting a file with![[notes/images/20220318_MergeFile.ipynb_image_1.png]]
	1. "transaction_id"
	2. "awardee_or_recipient_uniqu"
	3. A list of "permno" with maximum length of 5
2. Use "Match_List" and the selected variable list to merge on "transaction_id"
