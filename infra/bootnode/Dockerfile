FROM ethereum/client-go:alltools-v1.13.13

# Install required packages
RUN apk add --no-cache curl jq acl

# Create a user with a known UID/GID within range 10000-20000.
# This is required by Choreo to run the container as a non-root user.
RUN addgroup -S choreo && adduser -D -u 10001 -G choreo choreo

# Set the working directory
WORKDIR /log-directory

# Set permissions for /log-directory to allow read/write access for any user
RUN chown -R 10001:choreo /log-directory && \
    setfacl -R -d -m u:10001:rwx,g::rwx,o::rwx /log-directory

# Use the above created unprivileged user
USER 10001

# Expose the required ports
EXPOSE 30310 30311

# Set the entry point to the startup script
ENTRYPOINT ["/bin/sh", "/startup-scripts/bootnode.sh"]
