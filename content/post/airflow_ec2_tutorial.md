---
title: "How to Setup Apache Airflow on EC2 (Free Tier)"
date: 2022-05-07T11:58:04+01:00
draft: false
slug: ""
tags: ["tutorial"]
image: "/img/airflow_dark.png"
summary: "How to setup an AWS EC2 instance and install Apache Airflow with pip to schedule and monitor your data pipelines"
---

<center>{{< figure src="/img/airflow_words.png" width=200 caption="source: https://cwiki.apache.org/confluence/display/AIRFLOW/Airflow+logos"  >}}</center>

## Table of Contents
---

1. [Setting up EC2 on AWS](#setting-up-ec2)
2. [Python and Pip](#python-and-pip3)
3. [Creating a virtual environment](#creating-a-virtual-environment)
3. [Installing Airflow](#installing-airflow)
4. [Initialising Airflow](#initialising-airflow)

Apache Airflow is a widely used open source tool in organisations with large amounts of data processing. Created by AirBnb in 2015, Airflow is highly extensible, supporting many use cases in data engineering. It is desgined to orchestrate your data pipelines which are defined by [directed acyclic graphs](https://airflow.apache.org/docs/apache-airflow/stable/concepts/dags.html) (DAGs). Each DAG contains tasks with dependencies and relationships on how they should run. The rich UI webserver allows you to monitor your pipelines and get workflow-related insights.

[comment]: <> (Check out my guide on Airflow to learn more about how it works)

To begin you'll need to setup an [AWS account](https://aws.amazon.com) if you don't have one already. We'll be using the compute service EC2 which has a free tier option, but I recommend you read more about what the free tier includes to ensure you don't incur any unwanted costs.

## Setting up EC2

On the AWS navigation menu go to Compute, EC2 and select the option to launch a new EC2 instance. Give your instance a name and optionally add tags. On the Quick Start menu select the Ubuntu Amazon Machine Image (AMI) and from the dropdown menu choose the 'Ubuntu Server 22.04 LTS (HVM), SS Volume Type' AMI which will have the 'Free tier eligible' marker. 

Keep the instance type at t2.micro and create a new key pair using the .pem private key file if you use an IDE like Visual Studio Code. If you are on Windows, select the .ppk private key file for use with Putty. Leave the network settings at default and choose how much storage you would like to allocate (up to 30gb for the free tier as of writing this).

In order to access the webserver you will need to open up port 8080 to public as that is the port through which we will connect to Airflow on our EC2. To do this, navigate to the EC2's Security section and add an inbound rule to connect to port 8080. You may need to create a new security group if you don't have one and associate it with the EC2.

<center>{{< figure src="/img/security_group.png" width=800 caption=" Your security group inbound rules should include port 22 for SSH and 8080 for the Airflow webserver"  >}}</center>

Once launched it will take a moment to be initialised and you can then test connecting to it via SSH having saved your private key file saved somewhere on your system.

<details>
<summary>Best practice for Ubuntu servers 🙈 </summary>
<br>
On first creation of an Ubuntu server, there are some configuration steps you can run to increase the security and usability of your server and make it easier to run certain commands. I recommend looking at the following tutorial by DigitalOcean:
<br>
<br>
<a href="https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04">Inital Server Setup </a>

</details>


## Python and Pip3

Ubuntu 22.04 ships with Python 3 pre-installed, but we will first update our local package index and then upgrade the packages:

```terminal
sudo apt update
sudo apt -y upgrade
```

You should be able to check your Python version now by running:

```terminal
python3 -V
```

To install Airflow using pip, we will first need to install pip3:

```terminal
sudo apt install -y python3-pip
```

Lastly, to ensure we have all the pre-requisites for some Python packages, run:

```terminal
sudo apt install -y build-essential libssl-dev libffi-dev python3-dev
```

## Creating a Virtual Environment

To isolate your Airflow installation, it is best practice to install it within a virtual environment. Airflow has specific dependencies so this will prevent conflicts with any other projects you start. My preferred way is to use [Poetry](http://eliasbenaddouidrissi.com/setting-up-python-projects-with-pyenv-poetry/). However, since Airflow doesn't fully support it yet, we will use venv instead:

```terminal
sudo apt install -y python3-venv
```

Now navigate to where you would like to store your virtual environment and create a new directory and virtual environment with your own naming conventions:

```terminal
mkdir <new_environment>
```

Once within this new directory, run:

```terminal
python3 -m venv <my_new_environment>
```

To use this environment, you will need to activate it:

```terminal
source <my_new_environment>/bin/activate
```

You will see the new environment activated as your command prompt will now show a prefix with the name of your new environment in brackets. 

## Installing Airflow 

Before installing Airflow you might want to define where Airflow gets installed. By default it is installed in '~/airflow', but to change it run the following with your own new destination:

```terminal
export AIRFLOW_HOME=<new_destination>
```

We will install the latest Airflow (2.3.0 as of writing) using the constraint files specific to your Python version. Running the following commands will do this all for you:

```terminal
AIRFLOW_VERSION=2.3.0
PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
```
```terminal
CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
```
```terminal
pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
```

You've now got Airflow installed but you won't see any new folders yet. The next section will outline a basic setup using the simplest executor and database. 

<details>
<summary>What are the setup options for Aiflow? 🤔 </summary>
<br>
<br>
Airflow has many configuration settings and options for deployment depending on your use case. This tutorial is designed for quick start deployments where individuals can test their own pipelines and is not a standard production deployment. In the most simple form, Airflow can run using the SequentialExecutor which only allows for task instances to run sequentially and doesn't support parallelism. The metadata database used to store information about your DAG's and runs will be a SQLite database. Airflow can also be deployed using Docker which allows for greater customisations and is a more involved setup.
<br>
<br>
For a more robust production deployment, you will want to upgrade the database to a PostgreSQL database and use at least the LocalExecutor, although the most production ready deployments will most likely utilise queueing databases and multiple worker nodes and so would run on the CeleryExecutor or KubernetesExecutor. To find out more about deployment options, visit Airflow's website:
<br>
<br>
<a href="https://airflow.apache.org/docs/apache-airflow/stable/installation/index.html">Airflow Installation </a>
<br>
<br>
</details>

## Initialising Airflow

Airflow provides a 'standalone' command to initialise Airflow which includes creating a user, configuring your database and launching your webserver and scheduler. Let's run each component individually instead to understand how it works. First we'll need to kick start Airflow to create the required directory where we earlier defined as the home directory:

```terminal
airflow db init
```

This will create the SQLite database and the directories. Next, add an admin user that will be used to login on the UI:

```terminal
airflow users create \
    --username admin \
    --password admin \
    --firstname <your_name> \
    --lastname <your_last_name> \
    --role Admin \
    --email <your_email>
```

To start your Airflow webserver and scheduler, you will need to run them in separate shells or use '-D' to run it in the background in a single session:

```terminal
airflow webserver -p 8080 -D
```
```terminal
airflow scheduler -D
```

Lastly, you will need to create the 'dags' folder within the root directory of your Airflow home directory where you will store your own DAGs. I'll be going into more detail about how to write your first DAG in another tutorial.

<center>{{< figure src="/img/airflow_webserver.png"  caption="Airflow homepage showing example DAGs"  >}}</center>

That's it - you now have Airflow running using the SequentialExecutor and a SQLite database. Visit your EC2's public IPv4 DNS which should look something like 'ec2-12-345-678-901.eu-west-2.compute.amazonaws.com' and ensure to add a colon folowed by the port 8080 at the end of the address. You should see a list of all the example loaded DAGs and you're now ready to add your own. To hide these, you'll need to set the 'load_example_dags' variable to 'False' in the configuration file 'airflow.cfg'. This also holds your database connections and many other settings. Read more about what you can change on Airflow's official documentation [here](https://airflow.apache.org/docs/apache-airflow/stable/howto/set-config.html).



