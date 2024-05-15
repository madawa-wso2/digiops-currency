FROM ethereum/client-go:alltools-v1.13.13

# Install required packages
RUN apk add --no-cache curl jq

# Create a user with a known UID/GID within range 10000-20000.
# This is required by Choreo to run the container as a non-root user.
RUN adduser \
    --disabled-password \
    --gecos "" \
    --uid 10014 \
    --gid 10014 \
    "app"

# Set the working directory
WORKDIR /log-directory

# Set permissions for /log-directory to allow read/write access for any user
RUN chown app:app /log-directory

# Set permissions for /app to allow read/write access for any user
RUN chmod -R 776 /log-directory

# Use the above created unprivileged user
USER app

# Expose the required ports
EXPOSE 30310 30311

# Set the entry point to the startup script
ENTRYPOINT ["/bin/sh", "/startup-scripts/bootnode.sh"]
