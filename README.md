

**PRE-Requisite** in case we **don't** have internet connectivity at the location. 

1) Do the  initial setup of the  HDP sandbox. The initial root password is hadoop, but you are required to change it.

https://github.com/HortonworksUniversity/Essentials/blob/master/demos/SandboxSetup.md


    ssh root@127.0.0.1 -p 2222
    root@127.0.0.1's password: 
    You are required to change your password immediately (root enforced)
    Last login: Tue Mar  1 21:05:47 2016 from 10.0.2.2
    Changing password for root.
    (current) UNIX password: 
    New password: 
    Retype new password: 
    [root@sandbox ~]# ambari-admin-password-reset
    Please set the password for admin: 
    Please retype the password for admin: 
    
    The admin password has been set.
    Restarting ambari-server to make the password change effective...
    
    Using python  /usr/bin/python2
    Restarting ambari-server
    Using python  /usr/bin/python2
    Stopping ambari-server
    Ambari Server stopped
    Using python  /usr/bin/python2
    Starting ambari-server
    Ambari Server running with administrator privileges.
    Organizing resource files at /var/lib/ambari-server/resources...
    Server PID at: /var/run/ambari-server/ambari-server.pid
    Server out at: /var/log/ambari-server/ambari-server.out
    Server log at: /var/log/ambari-server/ambari-server.log
    Waiting for server start....................
    Ambari Server 'start' completed successfully.
    It is suggested that you set the admin Ambari user's password to admin for consistency with the other web UIs.

2) for the MEETUP lab, you will need to download datasets: Switch from root to zeppelin user. 

    sudo su - zeppelin
    
    #################################################
    #FOR PHILLY CRIME DATA Analysis
    #################################################
    
    wget https://raw.githubusercontent.com/zeltovhorton/sparkworkshop/master/data/philadelphia-crime-data-2015-ytd.csv
    ls
    pwd
    hadoop fs -mkdir /user/zeppelin/crime
    hadoop fs -put philadelphia-crime-data-2015-ytd.csv /user/zeppelin/crime/
    hadoop fs -ls /user/zeppelin
    hadoop fs -ls /user/zeppelin/crime
    #################################################
    
    #FOR RECOMMENDATION ENGINE example
    
    dataset="http://files.grouplens.org/datasets/movielens/ml-1m.zip"
    
    #dataset="http://files.grouplens.org/datasets/movielens/ml-10m.zip"
    #dataset="http://files.grouplens.org/datasets/movielens/ml-20m.zip"
    
    
    #################################################
    # The rest of this note should not be modified. #
    #################################################
    
    #Get the dataset
    
    echo ""
    rm -rf movielens
    hadoop fs -rm -r -f /user/zeppelin/movielens/
    
    
    mkdir movielens
    cd movielens
    wget $dataset -o /dev/null -O ml.zip
    unzip ml.zip
    rm ml.zip
    mv ml* ml
    gzip ml/ratings.dat
    
    # Move the required files to HDFS
    
    hadoop fs -mkdir /user/zeppelin/movielens
    hadoop fs -put ml/movies.dat /user/zeppelin/movielens/movies.dat
    hadoop fs -put ml/ratings.dat.gz /user/zeppelin/movielens/ratings.dat.gz
    
    echo "Files in HDFS:/user/zeppelin/movielens"
    hadoop fs -ls /user/zeppelin/movielens
    
    #################################################
    # FOR SENSOR DEMO
    #################################################
    
    wget http://s3.amazonaws.com/hw-sandbox/tutorial14/SensorFiles.zip
    unzip SensorFiles.zip
    hadoop fs -mkdir -p /user/zeppelin/SensorDemo
    hadoop fs -copyFromLocal -f SensorFiles/HVAC.csv /user/zeppelin/SensorDemo/
    hadoop fs -tail /user/zeppelin/SensorDemo/HVAC.csv





> Written with [StackEdit](https://stackedit.io/).
