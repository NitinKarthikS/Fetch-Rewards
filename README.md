# First: New Structured Relational Data Model

After analyzing the three Json files[ receipts, brands, users] provided, the receipts table is linked to users with userId column, indeed the recepits table has the rewardsReceiptitemList with delimitor[|] in which the rewardsProductPartnerId is present which links to the brands[cpg_id] column.

Inorder to link the recepits and brands, I would like to create the product table which has the receipt_id from the receipt table, product_id which is nothing but the rewardsProductPartnerId, quantity, brand_id which is the id from the brands table.




![image](https://user-images.githubusercontent.com/22611282/178987292-3d6cab64-e25c-418b-9d6b-9308265dcbc9.png)


# Second: Query

In order to getting started, I had imported the json files into table using table import wizard in Mysql Workbech

![img-1](https://user-images.githubusercontent.com/22611282/178990611-c890d987-2e45-4b48-b292-cf67768f2646.jpg)


![image](https://user-images.githubusercontent.com/22611282/178990926-8223689a-aff7-4a37-a689-343cc37f2e5b.png)

![image](https://user-images.githubusercontent.com/22611282/178991096-4bfab257-ac5d-4f80-9b3a-3b27414f4255.png)

![image](https://user-images.githubusercontent.com/22611282/178991241-b827dc75-2988-4a8d-8a84-329152b6966e.png)

![image](https://user-images.githubusercontent.com/22611282/178991306-208b1d5b-d095-4b8b-90f5-7d414f93dd1d.png)


all the tables would be imported and the data can be seen with the select query

## What are the top 5 brands by receipts scanned for most recent month?

select brand, count(*) from product p join brands b on p.brand_id = b.id join receipts r on r.id = p.receipts_id where date_trunc('month', r.purchaseDate) = max(date_trunc('month', r.purchaseDate)) order by count(*) desc limit 5;

## When considering average spend from receipts with 'rewardsReceiptStatus’ of ‘Accepted’ or ‘Rejected’, which is greater?

SELECT r.rewardsReceiptStatus, sum(r.purchasedItemCount)
FROM receipts r
GROUP BY r.rewardsReceiptStatus;

Average spend from receipts with 'rewardsReceiptStatus' of accepted is not in the table but, considering finished as accepted ;; accepted is greater than receipts with 'rewardsReceiptStatus' of rejected


![image](https://user-images.githubusercontent.com/22611282/178994516-8337d9dd-edce-4179-a288-14d77ace4ee1.png)




## When considering total number of items purchased from receipts with 'rewardsReceiptStatus’ of ‘Accepted’ or ‘Rejected’, which is greater?

SELECT createdDate__$date from users
ORDER BY createdDate__$date desc
LIMIT 10;

Considering finished as accepted;; The receipts with accepted status had more purchases than of rejected.

![image](https://user-images.githubusercontent.com/22611282/178995848-dea7d1ff-8095-4e98-8556-7eefc2697815.png)


# Third: Evaluate the Data Quality Issues

## Select * from brands

1.there are some many missing data in all the tables

![image](https://user-images.githubusercontent.com/22611282/178997316-6a5c3308-3ed8-46f9-a61b-f0474a208035.png)

2. The description field has the item not found text

![image](https://user-images.githubusercontent.com/22611282/178998469-d5f4ad68-cf25-4755-aaf7-23d9b55a1bbf.png)

3. The roles of users are Consumer and the fetch_staff, the staff is in general description provided for the user role which not suggestable

![image](https://user-images.githubusercontent.com/22611282/178999354-197b866b-0292-4fd5-9123-62ce4e48665d.png)

4. The brand names are not valid

![image](https://user-images.githubusercontent.com/22611282/179000086-c520c18c-919c-4a5d-859d-55686f47dce9.png)

# Fourth: Communication with Stakeholders

Hello Team,

I hope you are doing good! While I was analyzing the fetch rewards data, I had encountered few descripencies, I write this email in hope to get clarification on it. Below are few queries:

1. The json files include many nested fileds, is it possible to get the rewardsReceiptItemList column, found in the Receipts file, and the CPG column, located in the Brands file, expanded seperately in any other excel/text file.
2. For the Users table, there are so many users who had 'FETCH-STAFF' as the role. Is it possible to get specified roles of the users
3. There ae some many missing values in the receipts and brand files
4. The userId is not unique

I do have few questions on the data
1. How do I fill the missing values?
2. Which fields can be removed in the tables?
3. Is it possible to share with me the original data from which the json files are extracted?

I would be glad to discuss on the above points . I am flexible for this week and next week. Please let me know your avaibility so that we can have a elaborate discussion on these observations. Looking forward for your reply

Thank you for your time.

Regards,
Nitin.
