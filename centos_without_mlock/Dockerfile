FROM centos:7

USER root

RUN yum -y group install "Development Tools"

RUN yum install -y numactl-devel kernel kernel-devel kernel-headers wget sudo libhugetlbfs-utils pciutils vim python3

ENV DPDK_URL http://fast.dpdk.org/rel/dpdk-19.11.tar.xz
ENV DPDK_TAR dpdk-19.11.tar.xz 
ENV RTE_SDK "/dpdk-19.11"
ENV RTE_TARGET "x86_64-native-linux-gcc"


WORKDIR /
RUN wget $DPDK_URL
RUN tar xvf $DPDK_TAR

WORKDIR $RTE_SDK
RUN make -j 99 install T=x86_64-native-linux-gcc

WORKDIR $RTE_SDK/app/test-pmd
RUN rm testpmd.c
RUN wget https://raw.githubusercontent.com/bg-chun/mlock_disabled_dpdk/master/dpdk-19.11/app/test-pmd/testpmd.c


WORKDIR $RTE_SDK/app
RUN make -j 99 T=$RTE_TARGET


WORKDIR $RTE_SDK/$RTE_TARGET/app


CMD ["sleep", "infinity"]
