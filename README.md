# Install pyspark on linux 16.04LTS (xenial64)

You have a fresh linux instance.

## #1: Install Java8

```
sudo apt-add-repository ppa:webupd8team/java -y
sudo apt-get update
sudo apt-get install oracle-java8-installer -y  //Installer Asks for accepting the licence.
```

Set environment variables

+ `export JAVA_HOME=/usr/lib/jvm/java-8-oracle`
+ `export PATH=$JAVA_HOME/bin:$PATH`

## #2: Install Python3, pip3

Install python, venv, pip

```
sudo apt-get install python3
sudo apt install python3-venv python3-pip -y
```

<!-- Set alias to make python3 as default. Append `~/.bashrc` and source it.
```
alias python=python3
``` -->

Create a symlink between **python3** and **python** (unless 100% sure, don't do this)

```
sudo ln -s /usr/bin/python3 /usr/bin/python
```

Create a symlink between **pip3** and **pip** (unless 100% sure, don't do this)

```
sudo ln -s /usr/bin/pip3 /usr/bin/pip
```

## #3. Install Spark

Download [Spark](https://spark.apache.org/)

```
wget http://apache.osuosl.org/spark/spark-2.3.1/spark-2.3.1-bin-hadoop2.7.tgz
```

Unzip the tar file

```
tar -xzf spark-2.3.1-bin-hadoop2.7.tgz
```

Move the extracted folder to `/srv`

```
sudo mv spark-2.3.1-bin-hadoop2.7 /srv/spark-2.3.1
```

Create symlink for **spark**

```
sudo ln -s /srv/spark-2.3.1 /srv/spark
```

Set environment variables:

+ `export SPARK_HOME=/srv/spark`
+ `export PATH=$SPARK_HOME/bin:$PATH`

## #4 Testing pyspark

Open pyspark console with `pyspark` in console. Print out the version

```
print(sc.version)   //output -> 2.3.1
```

Good news! pyspark is set up now.

# Set up Jupyter notebook to work with pyspark

Install [jupyter](http://jupyter.org/)

```
sudo -H pip install jupyter
```

Set envorinment variables

+ `export PYSPARK_DRIVER_PYTHON=jupyter`
+ `export PYSPARK_DRIVER_PYTHON_OPTS='notebook'`

Create jupyter config file

```
jupyter notebook --generate-config
```

Edit __~/.jupyter/.jupyter_notebook_config.py__

```
c.NotebookApp.allow_origin = '*'
C.NotebookApp.ip = '0.0.0.0'
```

Test by running `pyspark` in console.
