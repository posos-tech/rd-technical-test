FROM python:3.10-slim-buster

# Define uid and gid arguments (passed during docker build command)
ARG user=appuser
ARG group=appuser
ARG uid
ARG gid

# Add in the container the group and the user you filled in
# https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
RUN groupadd -g ${gid} ${group}
RUN useradd -u ${uid} -g ${group} ${user} -m

# Give the created home the proper rights
RUN chown -R ${user}:${group} /home/${user}

# Add the user bin path in global PATH
ENV PATH="/home/${user}/.local/bin/:${PATH}"

# Change user
USER ${user}

# Install jupyterlab in container
RUN pip3 install --user jupyterlab sklearn pandas

# When the container launches, launches a jupyterlab instance
CMD ["jupyter", "lab", "--no-browser", "--notebook-dir='/app/examples'", "--ip=0.0.0.0", "--log-level='INFO'"]
