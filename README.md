# Gist
+ Analyzed Yelp data to understand businesses and user activity in Arizona.
+ Converted JSON files to Parquet for faster analysis.
+ Used Spark SQL to filter businesses by category and identify patterns in reviews, ratings, and user behavior.

# Setup
  1. Java Development Kit (JDK):
  + Required for running Hadoop and Spark.
  2. Hadoop:
  + For distributed storage and processing.
  3. Apache Spark:
  + For distributed data processing, can be integrated with Hadoop.
4. PySpark:
+ Python API for Spark, allowing you to write Spark applications in Python.
5. Jupyter Notebook (Optional):
+ For an interactive development environment, particularly useful when working with PySpark.
+ I just used VS Code.
6. Ubuntu
+ I used a virtual machine with the above tools and softwares installed (for detailed installation of the virtual machine, kindly follow the next section).

# Instructions to install the virtual machine
Steps for Intel-based processors:
1. Install VirtualBox (Intel processors), which is a cross-platform compatible Virtual Machine.
2. Download VirtualBox suitable for your system from [here](https://www.virtualbox.org/wiki/Downloads).
3. Download the VM file from the Dropbox link [here](https://www.dropbox.com/scl/fi/qczuksogkl4ndl8fv2ffi/Ubuntu-22.04-intel-cse511.ova?rlkey=94dppyi20k1d9z7aqcn8a80t0&e=1&st=ek32ogcs&dl=0).
4. You will reach this page:
![](https://res.craft.do/user/full/0f709ccb-026e-16d6-7cd0-33d21e5a77a4/doc/F02F6524-2C75-4BEA-ADBA-A61517B1CF32/9830D7F0-7DDA-4771-BCB2-38AA54183274_2/z0CWAUcZjVb6VFQxSyDw5zNRjwGfiUH8yqNQy2mKfNwz/Image.png)
+ Click on "Log In" and use your Dropbox credentials (create a Dropbox account if you don't have one) to log into Dropbox.
+ You will now be logged in, then click on "Download" button to start the download.
+ Next, open VirtualBox and import the VM file (ending in .ova extension) using instructions found [here](https://docs.oracle.com/cd/E26217_01/E26796/html/qs-import-vm.html).
5. Change the RAM/processor-cores to meet your PC specifications:
  + Adjust the RAM or/and the number of processors to make the VM compatible with your system. VirtualBox may not allow you to start the VM otherwise. Make sure to allocate just enough RAM for the VM to start and spare enough RAM for your computer. You can also change these settings later (after importing the VM) in the settings of theVirtualBox (system settings).
  + Finally, click on import .
6. Start the VM (password is **dps**).

Steps for Apple Silicon processors
1. Install UTM (Apple Silicon processors), which is a Virtual Machine simulator for Apple Silicon processors (M1/M1 Pro/M1 Max/M2/M3).
2. Install UTM from [here](https://mac.getutm.app/).
3. Download the VM file from the Dropbox link [here](https://www.dropbox.com/scl/fo/5mebfr2cpadlsfjc3agwc/ACe6Tx5174af9oD67AAQ9iM?rlkey=y3id2hsxrq02qvvduugoyrzyp&st=ss6syy36&dl=0).
+ You will reach this page:
![](https://res.craft.do/user/full/0f709ccb-026e-16d6-7cd0-33d21e5a77a4/doc/F02F6524-2C75-4BEA-ADBA-A61517B1CF32/7F96AF46-8D67-4464-9D74-364A514B3010_2/fOM1Z2UhgI8V7Yvo9x8e3xgmnwZklIIEu6Izx3KwPfsz/Image.png)
+ You will need to login into Dropbox with your credentials.
+ Then once you are logged in, click on the checkbox on the left side of the "Name" as shown below to select all the 3 files: Data , config.plist , screenshot.png.
+ Then click on "Download" button as shown in the above picture; File ending in .utm.zip will start downloading.
+ After download unzip the file and you should get the file with .utm extension. This is the virtual machine file that you would use in the Virtual Machine Software.
4. To load the pre-configured VM:
+ Click + “ Create a New Virtual Machine ”.
+ Click “ Open ” under the existing tab.
+ Select the downloaded .utm file.
5. Change the RAM/Processor-cores to meet your MAC specifications:
+ Adjust the RAM or/and the number of processors to make the VM compatible with your system. UTM may not allow you to start the VM otherwise.
+ Make sure to allocate just enough RAM for the VM to start and spare enough RAM for your
computer.
+ To adjust the configurations, right click on the VM and click on “ Edit ”.
6. Start the VM by clicking on the play button
+ Ignore "Display Output is not Active" message and wait for some time for VM to start
+ Password is **dps** whenever required for login or installing software.

# Some common commands
1. Format the Hadoop filesystem (only required when running Hadoop for the first time):
```
hdfs namenode -format
```
2. Start the Hadoop daemons:
```
start-dfs.sh
start-yarn.sh
```

3. Verify Hadoop Installation:
+ To check that Hadoop is running correctly, open the following URLs in your web browser:
  + HDFS NameNode Web UI: http://localhost:9870
  + YARN ResourceManager Web UI: http://localhost:8088
+ You should see the Hadoop interfaces, indicating that Hadoop is running successfully.

4. Apache Spark:
+ To verify Spark Installation:
```
spark-shell
```

5. PySpark
+ To verify PySpark Installation:
```
pyspark
```

6. Coding Environment: Jupyter Notebook + VS Code (Optional)
+ Jupyter Notebook provides an interactive environment where you can run PySpark code. Start a Jupyter Notebook with PySpark integration by running:
```
pyspark
```

+ By following these steps, you’ll set up a powerful local environment for big data processing with Hadoop, Spark, and PySpark, all within a Jupyter Notebook if desired.

# Dataset
+ I have used the Yelp dataset, which is a dataset of local businesses, reviews and user data.
+ There is a subset `yelp_dataset` which is a collection of 5 json files.
+ business_id and user_id are the common identifiers across the datasets.
+ Details are as follows:

| Files | Description | Fields |
| ------------- | ------------- | ------------- |
| yelp_academic_dataset_user.json | Reviewer information | 'user_id', 'compliment_writer', 'cool', 'useful', 'compliment_list', 'fans', 'compliment_more', 'average_stars', 'name', 'friends', 'elite', 'compliment_funny', 'compliment_cute', 'compliment_cool', 'compliment_hot', 'review_count', 'compliment_plain', 'compliment_profile', 'compliment_photos', 'compliment_note', 'funny', 'yelping_since' |
| yelp_academic_dataset_tip.json | Information about tip | business_id', 'user_id', 'compliment_count', 'date', 'text' |
| yelp_academic_dataset_review.json | Reviews given by the user | 'business_id', 'user_id', 'review_id', 'date', 'stars', 'useful', 'funny', 'cool', 'text' |
| yelp_academic_dataset_checkin.json | Check-in information | 'business_id', 'date' |
| yelp_academic_dataset_business.json | Restaurant business information with location and city | 'business_id', 'name', 'stars', 'is_open', 'address', 'latitude', 'categories', 'state', 'hours', , 'city', 'review_count', 'attributes', 'longitude', 'postal_code' |

+ To gain deeper understanding of the dataset structure, please visit [here](https://www.yelp.com/dataset/documentation/main).
+ Dataset Download (not required if you are using the Virtual Machine I provided):
1. To download the Yelp Open Dataset, go [here](https://www.yelp.com/dataset).
2. Click the Download Dataset at the end of the page. Fill the required information (name, email, sign and agreeing to terms and conditions). Then click the Download button at the end of the page.
3. You will reach this page:
   ![](https://res.craft.do/user/full/0f709ccb-026e-16d6-7cd0-33d21e5a77a4/doc/F02F6524-2C75-4BEA-ADBA-A61517B1CF32/4F4C6857-2D95-42E1-87EA-FA3EC0D74A23_2/gUHeErsoGaQBtvXIog8U5my9jlV61MXIXdiTyXYMkK0z/Image.png)
   Click on the left Download JSON to download the dataset (Photos is not required). Since the download is large, please be patient and use a stable internet connection while downloading the dataset.

# Project
+ Milestone 1: Business Level Analysis:
  + Objective: Analyze businesses based on their attributes, reviews, ratings, locations,
and other relevant data.
+ Milestone 2: User Level Analysis
  + Objective: Analyze user behavior, contributions (reviews, tips), and influence within the
Yelp community.

# Report
+ For a detailed explanation of my analysis, kindly go through the 2 reports uploaded.
