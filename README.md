# Distributed Hadoop Cluster Setup
This repository contains configuration scripts, documentation, and setup instructions for deploying a distributed Hadoop cluster on multiple Debian-based machines. The cluster supports running MapReduce jobs and basic HDFS operations, making it ideal for data analytics and educational purposes.

![Apache Hadoop](https://img.shields.io/badge/Apache%20Hadoop-66CCFF?style=plastic&logo=apachehadoop&logoColor=black)
![Debian](https://www.debian.org/logos/openlogo-75.png)


## Features

- Multi-node Hadoop cluster with NameNode and DataNodes
- Configured for HDFS and YARN
- Passwordless SSH between nodes
- Custom configuration of core-site.xml, hdfs-site.xml, yarn-site.xml, and mapred-site.xml
- Sample MapReduce job included for testing

## Repository Structure
``` markdown
├── config/         # XML configuration files
├── SETUP-GUIDE.md  # Step-by-step installation & setup instructions
├── sample-jobs/    # Sample WordCount job and input/output
└── README.md       # Project overview and usage
```


## Technologies Used

- Hadoop 3.4.1
- Java 8 or 11 (I used Java 8 but 11 works just as fine)
- Bash Scripting (minimal)

### System Version (The one which I used)
``` bash
PRETTY_NAME="Debian GNU/Linux 12 (bookworm)"
NAME="Debian GNU/Linux"
VERSION_ID="12"
VERSION="12 (bookworm)"
VERSION_CODENAME=bookworm
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
```

## Setup Instructions

For a complete setup guide, refer to [`SETUP-GUIDE.md`](./SETUP-GUIDE.md).

## Author

Ayush Chanekar  
GitHub: [@chanekarayush](https://github.com/chanekarayush)
