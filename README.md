<h1>Production-Ready Dockerized Go API with CI/CD</h1>

<p>
This project demonstrates a production-grade containerized Go REST API built with 
modern DevOps best practices. The application is packaged using a multi-stage Docker build, 
runs on a distroless base image for security, and is automatically built and pushed 
to Docker Hub using GitHub Actions CI/CD.
</p>

<hr/>

<h2>Architecture Overview</h2>

<p>
The system follows a simple but production-aligned container architecture.
</p>

<h3>Logical Flow</h3>

<pre><code>
Developer Push → GitHub → GitHub Actions → Docker Build → Docker Hub Registry → Deployment Environment
</code></pre>

<h3>Runtime Flow</h3>

<pre><code>
Client → Host Port (5004) → Docker Container (8080) → Go Application
</code></pre>

<hr/>

<h2>Architecture Diagram</h2>

<pre><code>
                    ┌────────────────────────────┐
                    │        Developer            │
                    │     (Push to main branch)   │
                    └──────────────┬──────────────┘
                                   │
                                   ▼
                    ┌────────────────────────────┐
                    │        GitHub Repo         │
                    └──────────────┬──────────────┘
                                   │
                                   ▼
                    ┌────────────────────────────┐
                    │     GitHub Actions CI      │
                    │  - Checkout Code           │
                    │  - Login to Docker Hub     │
                    │  - Build Image             │
                    │  - Push Image              │
                    └──────────────┬──────────────┘
                                   │
                                   ▼
                    ┌────────────────────────────┐
                    │        Docker Hub          │
                    │   Image Registry           │
                    └──────────────┬──────────────┘
                                   │
                                   ▼
                    ┌────────────────────────────┐
                    │      Runtime Server        │
                    │   Docker Container         │
                    │   Port 8080 (Internal)     │
                    └──────────────┬──────────────┘
                                   │
                                   ▼
                             Client Request
</code></pre>

<hr/>

<h2>Key Features</h2>

<ul>
  <li>Multi-stage Docker build</li>
  <li>Distroless runtime image</li>
  <li>Non-root container execution</li>
  <li>Automated Docker build and push</li>
  <li>Commit-based image versioning</li>
  <li>Secure credential management using GitHub Secrets</li>
</ul>

<hr/>

<h2>Technology Stack</h2>

<ul>
  <li>Go 1.22</li>
  <li>Docker (Multi-stage Build)</li>
  <li>Distroless Base Image</li>
  <li>GitHub Actions</li>
  <li>Docker Hub</li>
</ul>

<hr/>

<h2>Local Development</h2>

<h3>Build Image</h3>

<pre><code>docker build -t go-api-secure .</code></pre>

<h3>Run Container (Using Port 5004)</h3>

<pre><code>docker run -d -p 5004:8080 --name secure-go-api go-api-secure</code></pre>

<h3>Test Endpoint</h3>

<pre><code>http://localhost:5004</code></pre>

Expected Response:

<pre><code>{
  "message": "Hello from Go Docker API"
}</code></pre>

<hr/>

<h2>Docker Design Strategy</h2>

<h3>Stage 1 – Builder</h3>
<ul>
  <li>Uses official Go Alpine image</li>
  <li>Downloads dependencies</li>
  <li>Builds static binary</li>
</ul>

<h3>Stage 2 – Runtime</h3>
<ul>
  <li>Uses distroless base image</li>
  <li>No shell access</li>
  <li>No package manager</li>
  <li>Runs as non-root user</li>
</ul>

<p>
This significantly reduces image size and attack surface.
</p>

<hr/>

<h2>CI/CD Workflow</h2>

<p>
The GitHub Actions pipeline performs the following:
</p>

<ol>
  <li>Triggers on push to main branch</li>
  <li>Logs in to Docker Hub using repository secrets</li>
  <li>Builds Docker image</li>
  <li>Pushes image with two tags:</li>
</ol>

<pre><code>
raghavender123456/go-api-secure:latest
raghavender123456/go-api-secure:&lt;commit-sha&gt;
</code></pre>

<hr/>

<h2>Security Practices Implemented</h2>

<ul>
  <li>No root user inside container</li>
  <li>Distroless runtime image</li>
  <li>No debugging utilities in production image</li>
  <li>Secure credential storage in GitHub Secrets</li>
</ul>

<hr/>

<h2>Image Tagging Strategy</h2>

<ul>
  <li><strong>latest</strong> → Always points to most recent build</li>
  <li><strong>commit SHA</strong> → Enables traceable and reproducible deployments</li>
</ul>

<hr/>

<h2>Production Readiness</h2>

<p>
This project is designed to be:
</p>

<ul>
  <li>Kubernetes-ready</li>
  <li>Cloud-deployment ready</li>
  <li>Secure by default</li>
  <li>Scalable</li>
</ul>

<hr/>

<h2>Future Enhancements</h2>

<ul>
  <li>Add semantic version tagging (v1.0.0)</li>
  <li>Add automated test stage before build</li>
  <li>Add multi-architecture builds (AMD64 + ARM64)</li>
  <li>Add automated deployment to cloud instance</li>
</ul>

<hr/>

<h2>Author</h2>

<p>
Raghavender
</p>
