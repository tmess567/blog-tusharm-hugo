---
title: Google Colaboratory - Easy Big Query access
author: tusharm
type: post
date: '2018-07-23'
image: /wp-content/uploads/wallhaven-131694-2.jpg
---
My sister recently asked me for some help in running a comparison job between some large files spanning GBs worth of text. The most efficient solution I could find was Big Query. 

So I tried some sample jobs by manually getting the data into a Google Compute Engine then to Google Storage and then loaded into a BigQuery dataset. The reason I had to use the Compute Engine was because this large file was available on a remote server with an ssh only access. Instead of asking my sister to install gsutil for uploading to Google Storage, I found it easier to just ask her to scp the file to a GCE. 

The runtimes were quite surprising:\
`Query complete (9.4s elapsed, 6.81 GB processed)`

For the first few iterations, I used the UI and manually sent out the output. Eventually I built an automated [Google Colaboratory notebook](https://colab.research.google.com/drive/1xRhkEajxoD-rx4-TEVyx9OxJjw1A3w2H) where my sister could do this on her own.

## Setting up Google Compute Engine to sync directory to Google Storage

Setup a Shell Script to sync the directory to Google Storage bucket every x seconds.

https://cloud.google.com/storage/docs/gsutil/commands/rsync

```
#!/bin/shwhile true  do    gsutil -m rsync -r -d /home/tusharm567/didi_data_src/ gs://didi_data_src > /tmp/sync.log 2>&1    sleep 5  done
```

Then set it to run every time GCE boots up.

TODO...

https://stackoverflow.com/questions/12973777/how-to-run-a-shell-script-at-startup

We also need to provide access to the user who'll be using the notebook. 

```
gsutil iam ch user:tusharm57123@gmail.com:objectCreator,objectViewer gs://didi_data_src
```

**PS:** User needs to login when we call 

```
auth.authenticate_user()
```

## Creating a table and adding data from Google Storage

https://googlecloudplatform.github.io/google-cloud-python/latest/bigquery/usage.html

Creating a table can be done simply using the BigQuery python client.

```
table_ref = dataset_ref.table(table_name)table = bigquery.Table(table_ref)table = client.create_table(table)
```

To load data from a Google Storage CSV file, I needed to create a job with some configurations.

> The user running this should have the 
>
> **"BigQuery Data Owner" **
>
> role assigned to them. Search for IAM in Google Cloud Console and add user ( by Email ID ) and assign the above role.

https://googlecloudplatform.github.io/google-cloud-python/latest/bigquery/generated/google.cloud.bigquery.job.LoadJobConfig.html#google.cloud.bigquery.job.LoadJobConfig

```
job_config = bigquery.LoadJobConfig()job_config.autodetect = Truejob_config.skip_leading_rows = 1load_job = client.load_table_from_uri(uri, dataset_ref.table(table_name), job_config=job_config)
```

autodetect -> Infer the schema from File

skip_leading_rows -> Leave out first row assuming header.

> The user running this should have the 
>
> **"BigQuery Job User" **
>
> role assigned to them. Search for IAM in Google Cloud Console and add user ( by Email ID ) and assign the above role.
>
> For More Info: https://cloud.google.com/bigquery/docs/access-control#bigquery.dataOwner

## Querying the table

Tried directly using BQ Python Client's SQL query, but it doesn't support duplicate column names and the query I was using was an inner join with conflicting columns.

So I read the query output in a Pandas dataframe instead.

```
df = pd.io.gbq.read_gbq("""select * from {0}.{1};""".format(dataset_name, table_name), project_id=project_id, verbose=False)
```

## User I/O

For file I/O, I used google.colab.files

```
uploaded = files.upload()files.download(output_file_path)
```

Google Collab supports some form feature which are quite simple.

```
table_name = 'sampler' #@param {type:"string"}
```

You can also get a checkbox quite easily

```
skip_header = False #@param {type: "boolean"}
```

Good thing is the updates in the Forms are also reflected in code.

For more info: https://colab.research.google.com/notebooks/forms.ipynb
