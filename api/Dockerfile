FROM rust:1.87 as builder

RUN apt-get update && apt-get install -y git

WORKDIR /build
RUN git clone --depth=1 https://github.com/ic-ufrj/alumnic.git
WORKDIR /build/alumnic

RUN cargo build --release

FROM debian:bookworm-slim

RUN mkdir -p /root/.config/alumnic

COPY config.yaml /root/.config/alumnic/config.yaml

COPY --from=builder /build/alumnic/target/release/alumnic /usr/local/bin/alumnic

EXPOSE 8164

CMD ["alumnic", "serve", "0.0.0.0:8164"]

