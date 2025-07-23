# MCP_Servers

    Reference Documentation:
    https://github.com/grafana/mcp-grafana

# 1. Install Docker Desktop on Windows Machine  

    https://docs.docker.com/desktop/setup/install/windows-install/

# 2. Startup Grafana Container in Docker Desktop  

    docker run -d -p 3000:3000 --name=grafana grafana/grafana

# 3. Startup Prometheus Container in Docker Desktop   

    docker run -d -p 9090:9090 prom/prometheus

# 4. Startup Loki and Promtail Container in Docker Desktop   

    mkdir loki
    cd loki
    
    wget https://raw.githubusercontent.com/grafana/loki/v3.4.1/cmd/loki/loki-local-config.yaml -O loki-config.yaml
    wget https://raw.githubusercontent.com/grafana/loki/v3.4.1/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml

    docker run --name loki -d -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:3.4.1 -config.file=/mnt/config/loki-config.yaml
    docker run --name promtail -d -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:3.4.1 -config.file=/mnt/config/promtail-config.yaml

# 5. Clone the Loki-MCP Repository

    git clone https://github.com/grafana/loki-mcp.git

    # Build the Docker image
    docker build -t loki-mcp-server . 

# 5. Run the MCP-SuperAssitant npx command with config file

    npx @srbhptl39/mcp-superassistant-proxy@latest --config C:\Users\Public\github\MCP_Servers\chatgpt_web_config.json   

# 6. Run Commands from Chatgpt and have fun  

    List users and teams


