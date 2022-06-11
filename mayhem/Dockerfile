# Build Stage
FROM ghcr.io/evanrichter/cargo-fuzz:latest as builder

## Add source code to the build stage.
ADD . /src
WORKDIR /src
RUN cd netlink-packet-route/fuzz/ && cargo fuzz build
RUN cd netlink-packet-audit/fuzz/ && cargo fuzz build

# Package Stage
FROM rustlang/rust:nightly

COPY --from=builder /src/target/x86_64-unknown-linux-gnu/release/netlink-route /
COPY --from=builder /src/target/x86_64-unknown-linux-gnu/release/netlink-audit /
