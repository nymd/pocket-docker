FROM ubuntu:xenial

# metadata
ARG VCS_REF
ARG BUILD_DATE

LABEL openethereum.image.authors="devops-team@parity.io" \
	openethereum.image.vendor="OpenEthereum project" \
	openethereum.image.title="openethereum/openethereum" \
	openethereum.image.description="Fast and feature-rich multi-network Ethereum client." \
	openethereum.image.source="https://github.com/openethereum/openethereum/blob/${VCS_REF}/\
	scripts/docker/hub/Dockerfile" \
	openethereum.image.documentation="https://wiki.parity.io/Parity-Ethereum" \
	openethereum.image.revision="${VCS_REF}" \
	openethereum.image.created="${BUILD_DATE}"

# show backtraces
ENV RUST_BACKTRACE 1

# install tools and dependencies
RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
	file curl jq ca-certificates; \
	# apt cleanup
	apt-get autoremove -y; \
	apt-get clean; \
	update-ca-certificates; \
	rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/*; \
	# add user
	groupadd -g 1000 openethereum; \
	useradd -m -u 1000 -g openethereum -s /bin/sh openethereum

WORKDIR /home/openethereum

# add openethereum binary to docker image
COPY openethereum/openethereum /bin/openethereum
COPY openethereum/check_sync.sh /check_sync.sh
RUN chmod +x /bin/openethereum
RUN chmod +x /check_sync.sh

RUN mkdir -p /data/oe
RUN chown -R openethereum:openethereum /data/oe

# switch to user openethereum here
USER openethereum

# check if executable works in this container
RUN openethereum --version

ENTRYPOINT ["/bin/openethereum"]
