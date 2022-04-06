FROM rust:1.24.0

WORKDIR /usr/src/app
COPY ./rust_app .

RUN cargo install

CMD ["rust_app"]

#https://github.com/yzemmouri/rust_hello.git