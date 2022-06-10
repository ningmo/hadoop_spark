FROM centos:7.9.2009

RUN yum install -y which net-tools openssh-server openssh-clients wget

RUN ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa
RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
RUN ssh-keygen -t ecdsa -P ''   -f ~/.ssh/id_ecdsa
RUN ssh-keygen -t ed25519 -P '' -f ~/.ssh/id_ed25519

RUN cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
RUN sed -i  's/HostKey/\#HostKey/g' /etc/ssh/sshd_config
RUN echo -e "\nHostKey /root/.ssh/id_rsa\nHostKey /root/.ssh/id_ecdsa\nHostKey /root/.ssh/id_ed25519\nHostKey /root/.ssh/id_dsa" >> /etc/ssh/sshd_config

ADD jdk /usr/local/jdk
ENV JAVA_HOME /usr/local/jdk
ENV PATH $JAVA_HOME/bin:$PATH

ADD hadoop /usr/local/hadoop
ENV HADOOP_HOME /usr/local/hadoop
ENV PATH $HADOOP_HOME/bin:$PATH

COPY config/* /root/config/
ENV HADOOP_COMMON_HOME=$HADOOP_HOME

RUN echo -e "\nexport HDFS_NAMENODE_USER=root\nexport HDFS_DATANODE_USER=root\nexport HDFS_SECONDARYNAMENODE_USER=root\nexport YARN_RESOURCEMANAGER_USER=root\nexport YARN_NODEMANAGER_USER=root" >> $HADOOP_HOME/etc/hadoop/hadoop-env.sh
RUN echo -e "\nexport JAVA_HOME=/usr/local/jdk\n" >> $HADOOP_HOME/etc/hadoop/hadoop-env.sh
# RUN echo  -e "\n127.0.0.1     master" >> /etc/hosts
workdir /usr/local/hadoop
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
RUN cp -fr /root/config/core-site.xml /root/config/hdfs-site.xml /usr/local/hadoop/etc/hadoop/
# RUN hdfs namenode  -format
# RUN /usr/local/hadoop/sbin/start-all.sh


# -p 8088:8088 -p  8042:8042 -p 8040:8040 -p 8040:8040

# export EV=/Users/yangshaofeng/data/docker/hadoopSpark/env
# export JAVA_HOME=$EV/jdk
# export HADOOP_HOME=$EV/hadoop
# export PATH=$HADOOP_HOME/bin:$JAVA_HOME/bin:$PATH


##### !!!!!!!!!请注意host绑定！！！！！！！
##### !!!!!!!!!请注意host绑定！！！！！！！
##### !!!!!!!!!请注意host绑定！！！！！！！