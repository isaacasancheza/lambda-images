# base image
ARG BASE_IMAGE

# custom function directory
ARG FUNCTION_DIR

FROM ${BASE_IMAGE} AS build-image

# include global arg in this stage of the build
ARG FUNCTION_DIR

# install aws-lambda-cpp build dependencies
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y g++ make cmake unzip libcurl4-openssl-dev

# install the runtime interface client
RUN pip install --disable-pip-version-check --root-user-action ignore --target ${FUNCTION_DIR} awslambdaric

FROM ${BASE_IMAGE}

# include global arg in this stage of the build
ARG FUNCTION_DIR

# copy in the built runtime interface client
COPY --from=build-image ${FUNCTION_DIR} ${FUNCTION_DIR}

# set runtime interface client as default command for the container runtime
ENTRYPOINT [ "/usr/local/bin/python", "-m", "awslambdaric" ]

# pass the name of the function handler as an argument to the runtime
CMD [ "lambda_.handler" ]
