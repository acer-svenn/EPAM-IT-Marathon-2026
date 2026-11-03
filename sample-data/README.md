# Sample Data for Green & Tasty

This folder contains sample data for the Green & Tasty restaurant application.

After deploying the project to AWS, the DynamoDB tables were empty. To display restaurants, dishes and available tables on the website, I added some test data using JSON files.

There are three files:

- `locations.json` — contains 3 restaurant locations.
- `dishes.json` — contains 8 dishes with prices and descriptions.
- `tables.json` — contains 10 tables assigned to the restaurant locations.

## How to Import the Data

The data can be imported using AWS CLI after the DynamoDB tables have been created.

Open PowerShell in the `sample-data` folder and run the following commands:

**Import locations:**

`aws dynamodb batch-write-item --request-items file://locations.json --region us-west-2`

**Import dishes:**

`aws dynamodb batch-write-item --request-items file://dishes.json --region us-west-2`

**Import tables:**

`aws dynamodb batch-write-item --request-items file://tables.json --region us-west-2`

Before importing, make sure the correct AWS account is configured and the tables are empty. Importing records with existing keys may overwrite data.

If the import is successful, AWS CLI returns `"UnprocessedItems": {}`.

## Checking the Data

To check that the records were added, run:

`aws dynamodb scan --table-name Locations --select COUNT --region us-west-2 --query Count --output text`

`aws dynamodb scan --table-name Dishes --select COUNT --region us-west-2 --query Count --output text`

`aws dynamodb scan --table-name Tables --select COUNT --region us-west-2 --query Count --output text`

After importing into empty tables, the expected results are 3 locations, 8 dishes and 10 tables.

Once the data is added, the website can display restaurant locations, menu items and available tables.

These are only sample records for testing. Some dishes use default images because their individual image URLs are not specified. Waiter accounts are not included in these files and must be configured separately for reservations to work.