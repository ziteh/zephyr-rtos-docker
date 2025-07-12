ARG BASE_IMAGE="zephyr:arm-0.17.2SDK"

FROM ${BASE_IMAGE}

# Target Zephyr repository and revision

ARG ZEPHYR_REVISION=4.1.0
ARG ZEPHYR_URL=https://github.com/zephyrproject-rtos/zephyr

WORKDIR /workspace

RUN west init -m ${ZEPHYR_URL} --mr v${ZEPHYR_REVISION} ./ && \
    west update --narrow -o=--depth=1 && \
    west zephyr-export && \
    pip install -r zephyr/scripts/requirements-base.txt

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# WORKDIR /workspace
