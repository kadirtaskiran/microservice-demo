FROM busybox AS tini

ENV TINI_VERSION=v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN ["chmod", "+x" ,"/tini"]

#java 21.0.6 nonroot
FROM gcr.io/distroless/java21@sha256:7c872fc8a1187874a0235c9d93a434fff06d573f887467ccf2f80e120e6d59e9
LABEL maintainer=kadir.taskiran

COPY --from=tini /tini /tini

COPY build/libs/product-service.jar lib/product-service.jar

ENTRYPOINT ["/tini", "--"]

EXPOSE 8081

CMD ["java", "-jar", "-Djava.security.egd=file:/dev/./urandom", "-Duser.timezone=Europe/Istanbul", "-Dfile.encoding=UTF-8", "lib/product-service.jar"]