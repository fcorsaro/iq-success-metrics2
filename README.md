

**Download the source code:**

`git clone https://github.com/sotudeko/smproto.git`


*Go into the downloaded director*

`cd ./smproto`


**Using the app**

*1. Create a CSV file containing success metrics data*

This is done by using the Success Metrics API to query IQ 

Example:

`curl -u admin:admin123 -X POST -H "Accept: text/csv" -H "Content-Type: application/json" -o /var/tmp/successmetrics.csv -d@./sm-run/weekly.json http://localhost:8070/api/v2/reports/metrics`

This command reads the file weekly.json in the sm-run current directory. It contains a payload describing data set to retrieve from IQ

More info: https://help.sonatype.com/iqserver/automating/rest-apis/success-metrics-data-rest-api---v2

There are examples of the payload content in the sm-run directory: weekly.json and monthly.json

The output is saved to /var/tmp/successmetrics.csv


*2. Start the app*

This app is a simple web app running by default on port 4040

By default, the app looks for the data in the file /var/tmp/successmetrics.csv 

This file is loaded on start-up of the app. Larger files may take a few mins.

In the smproto directory

`mvn clean spring-boot:run`

You may also use the ./sm-build/build-jar.sh file to build a jar file which you can then run with 'java -jar <jarfile>'

When the file is loaded, you should see output similar to below after which app is ready for access

```
*020-05-11 19:07:30.554  INFO 88726 --- [           main] org.demo.smproto.ReadCSVFileRunner       : Number of entries: 52
2020-05-11 19:07:30.554  INFO 88726 --- [           main] org.demo.smproto.ReadCSVFileRunner       : Ready for browsing*
```

**3. Access the app**

In a browser, go to http://localhost:4040

Follow the links to see data and reports (If you want to access tha database user=user password=install)



Quick start
To run

```
cd sm-run
./create-csv-file.sh [weekly|monthly]
cd ..
mvn clean spring-boot:run
```
or if you want to build and run a jar file

```
cd ./sm-build
./build-jar.sh
cd ../sm-run
./create-csv-file.sh [weekly|monthly]
./run-app.sh <version>
```
