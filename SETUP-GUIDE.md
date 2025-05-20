# Hadoop Cluster Setup Guide (Multi-Node)

This guide walks you through setting up a distributed Hadoop cluster using Debian-based machines. It assumes basic familiarity with Linux and SSH.

---

## 🖥️ Hardware Requirements

- 1 Master Node (NameNode + ResourceManager)
- 1 or more Slave Nodes (DataNode + NodeManager)
- Minimum 2 GB RAM per node recommended

---

## 1: Install Java (on all nodes)
I'm using `java 8` here but `java 11` is also supported.
```bash
sudo apt update
sudo apt install openjdk-8-jdk -y
java -version
````

Add Java to `.bashrc`:

```bash
echo 'export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64' >> ~/.bashrc
echo 'export PATH=$PATH:$JAVA_HOME/bin' >> ~/.bashrc
source ~/.bashrc
```

---

## 2: Install Hadoop (on all nodes)

Download Hadoop:

```bash
wget https://archive.apache.org/dist/hadoop/common/hadoop-3.4.1/hadoop-3.4.1.tar.gz
tar -xvzf hadoop-3.4.1.tar.gz
sudo mv hadoop-3.4.1 /usr/local/hadoop
```

### Set Hadoop environment variables (`~/.bashrc`):

```bash
export HADOOP_HOME=/usr/local/hadoop
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
```

### Reload `.bashrc`:

```bash
source ~/.bashrc
```

---

## 3: Setup Passwordless SSH (master only)

### On the master node:

```bash
ssh-keygen -t rsa
ssh-copy-id user@master_ip
ssh-copy-id user@slave1_ip
ssh-copy-id user@slave2_ip
```

### Test SSH:

```bash
ssh slave1
```

---

## 4: Configure Hadoop

### Edit the following config files inside `$HADOOP_HOME/etc/hadoop/`:

1. **core-site.xml**
2. **hdfs-site.xml**
3. **mapred-site.xml**
4. **yarn-site.xml**
5. **hadoop-env.sh** (set `JAVA_HOME`)

### Sample files are available in the `/config/` folder of this repo.

---

## 5: Define Masters & Slaves

### Inside `$HADOOP_HOME/etc/hadoop/`:

* `masters`:

  ```
  master-hostname
  ```

* `workers` (or `slaves` in older versions):

  ```
  slave1-hostname
  slave2-hostname
  ```

---

## 6: Format HDFS (only once)

```bash
hdfs namenode -format
```

---

## 7: Start Hadoop Services

### On master:

```bash
start-dfs.sh
start-yarn.sh
```

### Check with:

```bash
jps
```

*jps must show all the running services if yarn(Resource Manager), datanode, secondary datanode are not working then you messed up. Please try again from the last and try to troubleshoot also refer to the [troubleshooting section](./SETUP-GUIDE.md#troubleshooting)*

---

## 8: Test MapReduce Job

```bash
hdfs dfs -mkdir /input
hdfs dfs -put sample.txt /input
hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-*.jar wordcount /input /output
hdfs dfs -cat /output/*
```

---

### Stop Services

```bash
stop-yarn.sh
stop-dfs.sh
```

---

## Troubleshooting

* Ensure hostnames and `/etc/hosts` are properly configured on all nodes.
* Java version mismatch can cause issues — use Java 8 or 11 but compile using only one.
* Use `jps` to confirm Hadoop daemons are running.

---

## 🧑‍💻 Maintainer

Ayush Chanekar
GitHub: [@chanekarayush](https://github.com/chanekarayush)
