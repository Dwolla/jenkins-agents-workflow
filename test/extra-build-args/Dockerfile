ARG TEMURIN_TAG

FROM eclipse-temurin:$TEMURIN_TAG
ARG EXTRA_ARG

# Fails the build unless the action passed EXTRA_BUILD_ARGS through alongside TAG_NAME=BASE_TAG.
RUN test "$EXTRA_ARG" = expected-value
