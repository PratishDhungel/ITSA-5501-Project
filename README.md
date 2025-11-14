## Repo structure
ITSA-5501-Project/
├── docker/   # Contains Dockerfiles or container build configurations
├── k8s/      # Stores Kubernetes manifests (Deployments, Services, etc.)
├── iac/      # Infrastructure as Code (e.g., Terraform, Ansible, CloudFormation)
└── README.md # Project documentation and workflow guide


## Tools Used
- Git
- GitHub
- Docker
- Kubernetes
- Infrastructure as Code (Terraform/Ansible)

## Collaboration Notes
- The main branch is used for stable code only.
- Each contributor must create a new branch for their work.
- All changes must go through a Pull Request and review process.
- Always update your local main branch before starting new work.


## Example Workflow
- Always pull the latest changes from main before editing.

## Example Workflow
1. Build Docker image from files in `docker/`
2. Deploy containers using manifests in `k8s/`
3. Manage infrastructure with scripts in `iac/`
4. Commit and push changes with clear messages
5. Create a Pull Request for review and merge

## Git Commands

# Initialize repo
git init

# Add and commit
git add .
git commit -m "Initial commit"

# Create and switch branches
git checkout -b experiment

# Merge branches
git checkout main
git merge experiment

# Push and pull
git push -u origin main
git pull origin main

# Tag versions
git tag -a v1.0 -m "Milestone 1 complete"
git push origin v1.0


## 🐳 Docker Compose Setup (Milestone 2)

### Services
| Service | Image | Description | Port |
|----------|--------|-------------|------|
| frontend | nginx:alpine | Serves static HTML from `frontend/` | 9090 |
| user-db | mongo | Stores user data (persistent volume `user_data`) | internal |
| product-db | postgres | Product data storage with env vars | internal |
| cache | redis | Caching service | internal |
| prometheus | prom/prometheus | Monitoring endpoint | 9091 |

### Volumes
- `user_data` → persists MongoDB data  
- `product_data` → persists PostgreSQL data  

### Network
- `app-network` → internal bridge for inter-container communication  

### Operations
```bash
cd docker
docker-compose up -d          # start all containers
docker ps                     # list running containers
docker-compose up -d --scale frontend=3  # scale frontend service
docker-compose down           # stop and remove containers
