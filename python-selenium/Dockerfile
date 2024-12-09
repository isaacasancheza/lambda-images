# base image
ARG BASE_IMAGE

# custom function directory
ARG FUNCTION_DIR

FROM ${BASE_IMAGE}

RUN apt-get update  \
    && export DEBIAN_FRONTEND=noninteractive \
    #
    # install selenium deps
    && apt-get install -y --no-install-recommends xvfb chromium-driver \
    #
    # clean-up
    && apt-get autoremove -y  \
    && apt-get clean -y  \
    && rm -rf /var/lib/apt/lists/* /tmp/library-scripts
