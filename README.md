<h1>Dockerized Go API with CI/CD (Production Ready)</h1>

<p>
This project demonstrates a production-ready Go REST API containerized using Docker 
with a multi-stage build, a distroless runtime image, and an automated CI/CD pipeline 
using GitHub Actions.
</p>

<hr/>

<h2>Project Overview</h2>

<p>
The application is a simple Go HTTP API that returns a JSON response. 
The main objective of this repository is not just the API itself, 
but demonstrating modern DevOps practices including:
</p>

<ul>
  <li>Multi-stage Docker builds</li>
  <li>Distroless production images</li>
  <li>Non-root container security</li>
  <li>Automated Docker image build and push</li>
  <li>Commit-based image tagging</li>
</ul>

<hr/>

<h2>Technology Stack</h2>

<ul>
  <li>Go 1.22</li>
  <li>Docker (Multi-stage build)</li>
  <li>Distroless base image</li>
  <li>GitHub Actions (CI/CD)</li>
  <li>Docker Hub (Container Registry)</li>
</ul>

<hr/>

<h2>Application Endpoint</h2>

<p>
Once running, the API exposes:
</p>

<pre><code>GET /</code></pre>

<p>Response:</p>

<pre><code>{
  "message": "Hello from Go Docker API"
}</code></pre>

<hr/>

<h2>Build the Docker Image Locally</h2>

<pre><code>docker build -t go-api-secure .</code></pre>

<hr/>

<h2>Run the Container</h2>

<p>
If port 8080 is already in use on your system, you can map another host port such as 5004.
</p>

<pre><code>docker run -d -p 5004:8080 --name secure-go-api go-api-secure</code></pre>

<p>Access the API:</p>

<pre><code>http://localhost:5004</code></pre>

<hr/>

<h2>Docker Architecture</h2>

<h3>Multi-Stage Build</h3>

<p>
The Dockerfile uses two stages:
</p>

<ol>
  <li>
    <strong>Builder Stage</strong> – Compiles the Go binary using the official Go Alpine image.
  </li>
  <li>
    <strong>Runtime Stage</strong> – Uses a minimal distroless image to run the compiled binary.
  </li>
</ol>

<p>
This results in:
</p>

<ul>
  <li>Smaller image size</li>
  <li>Reduced attack surface</li>
  <li>No unnecessary build tools in production</li>
</ul>

<hr/>

<h2>Security Best Practices Implemented</h2>

<ul>
  <li>Non-root user execution</li>
  <li>Distroless base image</li>
  <li>No shell or package manager in runtime image</li>
  <li>Static binary compilation (CGO disabled)</li>
</ul>

<hr/>

<h2>CI/CD Pipeline</h2>

<p>
This repository includes a GitHub Actions workflow that:
</p>

<ol>
  <li>Triggers on push to the <code>main</code> branch</li>
  <li>Logs in to Docker Hub using repository secrets</li>
  <li>Builds the Docker image</li>
  <li>Pushes the image to Docker Hub</li>
  <li>Tags the image with both <code>latest</code> and commit SHA</li>
</ol>

<hr/>

<h2>Image Tagging Strategy</h2>

<p>
Each push generates:
</p>

<pre><code>raghavender123456/go-api-secure:latest
raghavender123456/go-api-secure:&lt;commit-sha&gt;</code></pre>

<p>
This ensures traceability and reproducible deployments.
</p>

<hr/>

<h2>Environment Configuration</h2>

<p>
The CI pipeline uses:
</p>

<ul>
  <li><code>Repository Variable:</code> DOCKER_USERNAME</li>
  <li><code>Repository Secret:</code> DOCKER_PASSWORD</li>
</ul>

<p>
This avoids hardcoding credentials in the workflow file.
</p>

<hr/>

<h2>Production Considerations</h2>

<p>
This setup is designed to be:
</p>

<ul>
  <li>Kubernetes-ready</li>
  <li>Cloud deployment ready</li>
  <li>Secure by default</li>
  <li>Scalable</li>
</ul>

<hr/>

<h2>Future Improvements</h2>

<ul>
  <li>Add semantic version tagging</li>
  <li>Add automated tests before build stage</li>
  <li>Add multi-architecture image build (AMD64 + ARM64)</li>
  <li>Add automatic deployment to cloud environment</li>
</ul>

<hr/>

<h2>Author</h2>

<p>
Maintained by Raghavender.
</p>
