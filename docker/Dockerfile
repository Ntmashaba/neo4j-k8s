# docker/Dockerfile

FROM neo4j:5.19.0

# Copy custom configuration files into the appropriate directories
COPY neo4j.conf /var/lib/neo4j/conf/neo4j.conf
COPY custom-env.sh /docker-entrypoint-initdb.d/custom-env.sh

# Ensure the script is executable
RUN chmod +x /docker-entrypoint-initdb.d/custom-env.sh

# Environment variables can be set directly in the Dockerfile if needed
# ENV NEO4J_dbms_memory_pagecache_size=2G
# ENV NEO4J_dbms_memory_heap_initial_size=512M
# ENV NEO4J_dbms_memory_heap_max_size=1G