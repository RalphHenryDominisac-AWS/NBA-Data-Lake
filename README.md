
# NBA Data Lake Setup

This repository contains the `setup_nba_data_lake.py` script, which automates the creation of a data lake for NBA analytics using AWS services. The script integrates Amazon S3, AWS Glue, and Amazon Athena to set up the infrastructure needed to store and query NBA-related data.

## Features

The `setup_nba_data_lake.py` script performs the following actions:

1. **Amazon S3**: Creates a bucket to store raw and processed data, and uploads sample NBA data in JSON format.
2. **AWS Glue**: Creates a database and an external table for querying the data.
3. **Amazon Athena**: Configures Athena for querying data stored in the S3 bucket.

Additionally, the repository includes the following scripts:

- `delete_aws_resources.py`: Deletes the S3 bucket, Glue database, and Athena configurations created during setup.
- `IAM_Role.txt`: Defines the IAM role policies required for the scripts to function.

## Prerequisites

Before using this repository, ensure you have the following:

- An AWS account with appropriate permissions (refer to `IAM_Role.txt`).
- Python 3.x installed on your machine.
- The `boto3` and `python-dotenv` libraries installed (`pip install boto3 python-dotenv`).
- A valid Sportsdata.io API key.


## Architecture

The system implements a serverless data lake architecture using AWS services, designed for efficient data processing and querying. Here's how the components interact:

![Image Alt](https://github.com/RalphHenryDominisac-AWS/NBA-Data-Lake/blob/686e2ba03aa577423b9958efb03e3f48c2a361bf/architecture%20NBA%20data%20lake.jpg)

## Components Flow

1. Data Storage (S3 Buckets)

- Serves as the primary storage for raw data
- Stores JSON documents in a structured format
- Acts as the source for all downstream processing


2. Data Processing (Crawler)

- Utilizes Apache Spark ETL jobs for data transformation
- Automatically discovers and catalogs data schema
- Processes data for downstream analytics


3. Metadata Management (AWS Glue Data Catalog)

- Maintains metadata information about all datasets
- Stores DDL (Data Definition Language) Hive metadata
- Serves as a central metadata repository


4. Query Engine (Amazon Athena)

- Provides serverless SQL query capabilities
- Uses Presto distributed engine for processing
- Enables direct querying of data stored in S3

## Setup Instructions

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/nba-data-lake-setup.git
   cd nba-data-lake-setup
   ```

2. Configure your environment variables:
   - Create a `.env` file in the project root with the following content:
     ```
     SPORTS_DATA_API_KEY=your_api_key
     NBA_ENDPOINT=https://api.sportsdata.io/v4/nba/stats/json/Players
     ```

3. Run the `setup_nba_data_lake.py` script to set up the data lake:
   ```bash
   python setup_nba_data_lake.py
   ```

4. To clean up resources after use, run the `delete_aws_resources.py` script:
   ```bash
   python delete_aws_resources.py
   ```

## AWS Services Used

- **Amazon S3**: Stores raw and processed NBA data.
- **AWS Glue**: Creates a schema for the data and manages metadata.
- **Amazon Athena**: Enables SQL-based querying of the data.

## IAM Role Permissions

The `IAM_Role.txt` file defines the permissions required for the scripts. These include access to:

- S3 operations (create, delete, upload, list).
- Glue operations (create, delete, query databases and tables).
- Athena operations (execute and fetch queries).

## Example Usage

Once the data lake is set up, you can query NBA data using Amazon Athena. For example:
```sql
SELECT * FROM nba_players WHERE Points > 20;
```

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

---

