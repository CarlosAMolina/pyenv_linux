# Operating system.
FROM debian:buster-slim

# Desired python version.
ARG PYTHON_VERSION=3.7.2

# Create group nonroot.
RUN groupadd -r nonroot

# Create user called nonroot.
# Create directory /home/nonroot.
RUN useradd \
-r -g nonroot \
-d /home/nonroot \
-s /bin/bash \
-c "Nonroot User" nonroot

# Create directories.
RUN mkdir /home/nonroot

# Change directories permissions.
RUN chown -R nonroot:nonroot /home/nonroot/

# Update repositories.
RUN apt-get update

# Installations.
RUN apt-get -y install \
git \
vim

# Set the working directory.
WORKDIR /home/nonroot

# Clone repository.
RUN git clone https://github.com/carlosamolina/pyenv_linux

# Change working directory to the downloaded git repository.
WORKDIR /home/nonroot/pyenv_linux

# Create .bashrc file required for pyenv.
RUN > /home/nonroot/.bashrc

# Install repository dependencies (root user).
RUN /bin/bash pyenv_linux -id

# Change directories permissions.
# Important to change permissions of the created file .bashrc.
RUN chown -R nonroot:nonroot /home/nonroot/

# Change user.
USER nonroot

# Install pyenv.
RUN /bin/bash pyenv_linux -ip /home/nonroot

# Apply required configurations to work with pyenv.
RUN /bin/bash pyenv_linux -c

# With Dockerfile, the previous command does not modify the path.
# Add .pyenv folder to the path.
ENV PATH="/home/nonroot/.pyenv/bin:$PATH"

# Show pyenv python available versions.
RUN pyenv versions

# Install and set python version.
RUN /bin/bash -c "source pyenv_linux -s $PYTHON_VERSION"

# With Dockerfile, the previous command does not set the python version.
RUN pyenv global $PYTHON_VERSION

# Show pyenv python available versions.
RUN pyenv versions

# Change the working directory to the main one.
WORKDIR /home/nonroot

# Entrypoint.
# Open bash terminal.
CMD ["/bin/bash"]
