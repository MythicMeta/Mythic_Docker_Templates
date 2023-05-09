FROM itsafeaturemythic/mythic_python_base:latest

COPY --from=golang:1.20-alpine /usr/local/go/ /usr/local/go/

ENV PATH="/usr/local/go/bin:${PATH}"
ENV GOPATH /usr/local/go
ENV PATH $GOPATH/bin:$PATH