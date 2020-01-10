FROM centos:7
RUN yum install -q -y \
	go \
	git \
	glusterfs \
	glusterfs-fuse \
	attr \
	gcc 
RUN curl -LO https://dl.google.com/go/go1.13.6.linux-amd64.tar.gz && \
	tar -C /usr/local -xvzf go1.13.6.linux-amd64.tar.gz 
RUN export PATH=$PATH:/usr/local/go/bin && \
	mkdir -p /root/go/src/github.com/docker && \
	cd /root/go/src/github.com/docker && \
	git clone https://github.com/docker/go-connections.git && \
	cd go-connections && \
	git checkout 908dcf0115b8215cde21154dd910fb80862dbf86 && \
	cd / && \
	go get github.com/trajano/docker-volume-plugins/glusterfs-volume-plugin && \
	mv $HOME/go/bin/glusterfs-volume-plugin / && \
	rm -rf /usr/local/go && \
	yum remove -q -y go git gcc && \
	yum autoremove -q -y && \
	yum clean all && \
	rm -rf \
		/var/cache/yum \
		/var/log/anaconda \
		/var/cache/yum \
		/etc/mtab \
	&& \
	rm -fv \
		/var/log/lastlog \
		/var/log/tallylog