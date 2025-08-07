# Terraform Docker Nginx

This project uses Terraform to provision an Nginx container on Docker locally via the Docker provider.

## 🔧 Requirements

- [Terraform](https://developer.hashicorp.com/terraform/downloads)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Git (for pushing to GitHub)

> Tested on macOS with Docker Desktop v28.3.2 and Terraform 1.x.

---

## 🚀 Setup Instructions

### 1. Clone the repo  ```bash
git clone https://github.com/<your-username>/terraform-docker-nginx.git
cd terraform-docker-nginx
2. Enable Docker Unix Socket on macOS
Docker Desktop doesn’t expose the socket by default on macOS.
Steps:

Open Docker Desktop → Settings → Docker Engine
Update config to include:
{
  "features": {
    "buildkit": true
  },
  "experimental": false,
  "debug": true
}
Click Apply & Restart
3. Run Terraform
terraform init
terraform apply -auto-approve
This will:
Pull the nginx:latest image
Run a container named nginx_container
Map port 80 inside the container to port 8080 on your host
🌐 Access the Nginx Page
Visit:
http://localhost:8080
You should see the Nginx welcome screen.
🧹 Cleanup
To destroy the resources:
terraform destroy -auto-approve
🗂 Project Structure
terraform-docker-nginx/
├── main.tf
└── README.md
📦 Terraform Code Example (main.tf)
provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  name  = "nginx_container"
  image = docker_image.nginx.image_id

  ports {
    internal = 80
    external = 8080
  }
}
👨‍💻 Author
Harsha Vardhan



##
