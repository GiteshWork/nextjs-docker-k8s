🐳 Docker Setup
3️⃣ Build and run locally
docker build -t nextjs-blog .
docker run -p 3000:3000 nextjs-blog


Now open http://localhost:3000
.

4️⃣ Using Docker Compose
docker-compose up --build

🔑 Docker Hub Configuration
5️⃣ Create Access Token

Go to Docker Hub Security Settings

Create a new access token

Save it for later (used in GitHub Secrets)

🤖 GitHub Actions CI/CD
6️⃣ Add GitHub Secrets

In your GitHub repo:

DOCKER_HUB_USERNAME → Your Docker Hub username

DOCKER_HUB_ACCESS_TOKEN → The token you created

7️⃣ Workflow file

Located at: .github/workflows/ci.yml

It:

Logs in to Docker Hub

Builds Docker image

Pushes image to Docker Hub

🚀 CI/CD in Action

Every push to the main branch will:

Build Docker image

Tag as latest

Push to Docker Hub:

docker.io/<your-username>/nextjs-blog:latest

📝 Usage

Pull your image anywhere and run:

docker pull <your-username>/nextjs-blog:latest
docker run -p 3000:3000 <your-username>/nextjs-blog:latest

📂 Project Structure
├── .github/workflows/ci.yml     # GitHub Actions workflow
├── Dockerfile                   # Docker build instructions
├── docker-compose.yml            # Local development setup
├── pages/                       # Next.js pages
├── public/                      # Static assets
└── package.json
