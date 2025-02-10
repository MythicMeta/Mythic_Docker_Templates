FROM itsafeaturemythic/mythic_python_base:latest

COPY --from=golang:1.23-bullseye /usr/local/go/ /usr/local/go/

ENV PATH="/usr/local/go/bin:${PATH}"