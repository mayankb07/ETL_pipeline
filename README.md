# ETL_pipeline

  # Description
  The Deutsche Börse Public releases real-time trade data in their AWS public s3 bucket, s3://deutsche-boerse-xetra-pds(Xetra data) and s3://deutsche-boerse-eurex-pds (for Eurex data) to the public for free in the EU Central (Frankfurt) region, which is aggregated to on minute by minute basis from the Eurex and Xetra trading systems.
  
  The date from source S3 bucket looks like this
  ![image](https://user-images.githubusercontent.com/85644097/145701443-963cb4f6-839b-4489-806e-fa9c299244cf.png)

  
  # Location
  The data is uploaded in two Amazon S3 buckets in the EU Central (Frankfurt) region
  
  * s3://deutsche-boerse-xetra-pds (for Xetra data)
  * s3://deutsche-boerse-eurex-pds (for Eurex data)
    
    We'll be extracting the data from s3://deutsche-boerse-xetra-pds (for Xetra data)
    
  # Naming convention
  Each bucket contains contains a directory for each available date, named in the ISO 8601 format YYYY-MM-DD.
  
  For dates other than the current trading day in Frankfurt time, where the exchanges live, a file exists for each hour of the trading day. Thes files are       named YYYY-MM-DD_BINS_mrkthh.csv, where mkrt is either XEUR or XETR (ISO 10383 Market Identification Codes) and hh is the two digit hour indicating which       hour of trading the file contains, in 24 hour format. Time is in UTC (both for file names as well as for the content).
  
  For example:
  
  ![image](https://user-images.githubusercontent.com/85644097/145701284-50a630ce-a365-41bb-bc54-1c02dc689b99.png)
  
  
  # The key tasks of the project include:
  * Extracted the date from public S3 bucket, performed transformation and loaded the data in another S3 bucket in parquet format.
  * Created the IAM user in AWS, attached the AmazonS3FullAccess permission policy, and configured it through AWS CLI
  * Used boto3 for interacting with the S3 bucket through python
  * Created features like opening price, closing price, growth percentage, maximum and minimum price for each day
  * Created meta file for job control, if in case there is any failure, we can analyze it
  * Used Docker Hub for storing docker image and docker image was pulled by orchestration tool which created a docker container on execution platform kubernetes
  
