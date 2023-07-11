# Start your image with a node base image
FROM python:3.11

# The /app directory should act as the main application directory
WORKDIR /code

#
RUN pip install -U pip && \
    pip install poetry

# Copy the app package and package-lock.json file
COPY poetry.lock pyproject.toml ./

# Copy local directories to the current local directory of our docker image (/app)
COPY src/ ./src/

# Install poetry globally - with the current version of
# poetry, there is a known issue where poetry config will
# not create config.toml: https://github.com/sdispater/poetry/issues/1179
# As such, we create it ourselves.
RUN mkdir -p ${HOME}/.config/pypoetry/ && \
    touch ${HOME}/.config/pypoetry/config.toml && \
    poetry config settings.virtualenvs.create false && \

    # Set PRODUCTION to anything to invoke installation with --no-dev
    ARG PRODUCTION
RUN poetry install ${PRODUCTION:+--no-dev}

EXPOSE 3000