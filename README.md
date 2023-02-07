Here, data is moved from an OLTP system into an OLAP system. Data enrichment is done during the data movement.
Please refer the Architecture Diagram first so as to get an idea of what we are trying to build.
I have included the important notes on each and every service used in the pipeline and also all the code snippets.
The notes are numbered in the order in which the services were built in the pipeline.

This pipeline is built for "ongoing / current" data migration. 
Refer "https://github.com/vinods03/AWS-DatabaseMigration-HistoricalData" for historical data migration details.
The spark code that we developed for EMR in the historical data migration has been made Glue-compatible here.

The concept of synchronous lambda invocations (where we await the response of a command) is shown here.
Idempotence is also ensured - if a record is present in Redshift staging table that is already processed into the final layer, we delete the record from the final table and then insert from staging layer. This way, we ensure only record is present for one order_id and that is the latest version.
