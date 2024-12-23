# Docker Neo4j

To install Docker Compose for Neo4j, follow these steps:

### 1. **Install Docker**
If you don't already have Docker installed, follow the instructions for your operating system:

- **Linux:**
  ```bash
  sudo apt-get update
  sudo apt-get install -y docker.io
  ```
  Add your user to the Docker group to avoid using `sudo`:
  ```bash
  sudo usermod -aG docker $USER
  ```

- **macOS/Windows:**
  Install Docker Desktop from [Docker's official website](https://www.docker.com/products/docker-desktop).

---

### 2. **Install Docker Compose**
Most recent versions of Docker Desktop include Docker Compose. To verify:
```bash
docker compose version
```

If not installed, use the following instructions:

- **Linux:**
  ```bash
  sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose
  ```

- **Verify Installation:**
  ```bash
  docker-compose --version
  ```

---

### 3. **Set Up Docker Compose for Neo4j**

1. **Create a `docker-compose.yml` File:**

   Create a file named `docker-compose.yml` with the following content:
   ```yaml
   version: '3.8'

   services:
     neo4j:
       image: neo4j:latest
       container_name: neo4j
       ports:
         - "7474:7474"  # Neo4j Browser
         - "7687:7687"  # Bolt Protocol
       environment:
         NEO4J_AUTH: "neo4j/your_password"  # Replace with your desired password
       volumes:
         - neo4j_data:/data
         - neo4j_logs:/logs
         - neo4j_import:/import
         - neo4j_plugins:/plugins

   volumes:
     neo4j_data:
     neo4j_logs:
     neo4j_import:
     neo4j_plugins:
   ```

   Replace `your_password` with a strong password for your Neo4j database.

2. **Start Neo4j Container:**
   ```bash
   docker-compose up -d
   ```

   This command will pull the Neo4j image, create a container, and start it in detached mode.

---

### 4. **Access Neo4j**
- **Neo4j Browser:** Open your browser and navigate to `http://localhost:7474`.
- **Default Credentials:** 
  - Username: `neo4j`
  - Password: Use the one you specified in `NEO4J_AUTH`.

---

### 5. **Stop Neo4j**
To stop the container, run:
```bash
docker-compose down
```

You now have a fully functional Neo4j database running with Docker Compose! Let me know if you encounter any issues.