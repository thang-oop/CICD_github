# CI/CD GitHub Project

Spring Boot microservice với CI/CD pipeline hoàn chỉnh sử dụng GitHub Actions.

## 📋 Tính năng

- ✅ Spring Boot 3.2.5 với Java 17
- ✅ RESTful API
- ✅ Health check endpoints (Spring Boot Actuator)
- ✅ Docker containerization
- ✅ Docker Compose cho local development
- ✅ CI/CD pipeline với GitHub Actions
- ✅ Automated testing
- ✅ Docker image build và push tự động lên GitHub Container Registry

## 🚀 Quick Start

### Chạy local với Maven

```bash
mvn spring-boot:run
```

Truy cập: http://localhost:8080

### Chạy với Docker Compose

```bash
docker-compose up -d
```

### Build Docker image manually

```bash
docker build -t cicd-github-app .
docker run -p 8080:8080 cicd-github-app
```

## 📡 API Endpoints

- `GET /` - Hello message
- `GET /actuator/health` - Health check endpoint
- `GET /actuator/info` - Application info
- `GET /actuator/metrics` - Application metrics

## 🔄 CI/CD Pipeline

Pipeline tự động chạy khi:
- Push code lên branch `main` hoặc `develop`
- Tạo Pull Request vào `main` hoặc `develop`
- Trigger thủ công qua GitHub Actions UI

### Pipeline Stages

1. **Build and Test**
   - Checkout code
   - Setup JDK 17
   - Build với Maven
   - Run unit tests
   - Upload JAR artifact

2. **Docker Build and Push** (chỉ chạy khi push vào `main`)
   - Build Docker image
   - Push lên GitHub Container Registry
   - Support multi-platform (amd64, arm64)
   - Automatic tagging (latest, branch name, SHA)

3. **Deploy** (chỉ chạy khi push vào `main`)
   - Placeholder cho deployment configuration
   - Có thể cấu hình deploy lên Kubernetes, Cloud providers, etc.

## 🐳 Docker Images

Images được publish lên GitHub Container Registry:

```bash
docker pull ghcr.io/thang-oop/cicd_github:latest
```

## 📦 Build & Test

```bash
# Build
mvn clean package

# Run tests
mvn test

# Skip tests
mvn clean package -DskipTests
```

## 🔧 Configuration

### Application Properties

File: `src/main/resources/application.properties`

```properties
server.port=8080
spring.application.name=CiCD_github
management.endpoints.web.exposure.include=health,info,metrics
```

### Docker Compose

File: `docker-compose.yml`

Cấu hình:
- Port mapping: 8080:8080
- Health checks
- Auto restart
- Log volume mounting

## 📝 Project Structure

```
.
├── .github/
│   └── workflows/
│       └── ci-cd.yml          # GitHub Actions workflow
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── org/example/
│   │   │       └── ApplicationMain.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
├── Dockerfile                  # Multi-stage Docker build
├── docker-compose.yml          # Local development setup
├── .dockerignore
├── pom.xml                     # Maven configuration
└── README.md
```

## 🛠️ Development

### Prerequisites

- Java 17+
- Maven 3.6+
- Docker & Docker Compose (optional)

### Local Development

1. Clone repository
```bash
git clone https://github.com/thang-oop/CICD_github.git
cd CICD_github
```

2. Run application
```bash
mvn spring-boot:run
```

3. Test the API
```bash
curl http://localhost:8080
curl http://localhost:8080/actuator/health
```

## 🚢 Deployment Options

### Kubernetes

```bash
kubectl create deployment cicd-app --image=ghcr.io/thang-oop/cicd_github:latest
kubectl expose deployment cicd-app --port=8080 --type=LoadBalancer
```

### Docker Swarm

```bash
docker service create --name cicd-app -p 8080:8080 ghcr.io/thang-oop/cicd_github:latest
```

### Cloud Providers

- **AWS ECS**: Sử dụng task definition với image từ GHCR
- **Azure Container Apps**: Deploy trực tiếp từ container registry
- **Google Cloud Run**: Deploy serverless container

## 📊 Monitoring

Health check endpoint:
```bash
curl http://localhost:8080/actuator/health
```

Metrics endpoint:
```bash
curl http://localhost:8080/actuator/metrics
```

## 🤝 Contributing

1. Fork repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 📄 License

MIT License

## 👤 Author

**Thang OOP**
- GitHub: [@thang-oop](https://github.com/thang-oop)

---

**Built with ❤️ using Spring Boot and GitHub Actions**
