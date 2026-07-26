# Java URL Shortener

A lightweight, high-performance URL shortener backend built with **Spring Boot 3**, **JPA**, and **Base62 encoding**. Generate short links, track clicks, set custom aliases, and handle expiration — all through a clean REST API.

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.3.0-brightgreen)](https://spring.io/projects/spring-boot)
[![Java](https://img.shields.io/badge/Java-21-orange)](https://openjdk.org/projects/jdk/21/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

##  Features

| Feature | Description |
|---------|-------------|
|  **Shorten URLs** | Convert long URLs into compact Base62 short codes |
|  **Custom Aliases** | Define your own short codes (e.g., `my-project`) |
|  **Expiration** | Set optional expiry dates per link |
|  **Click Tracking** | Automatically counts every redirect |
|  **Redirect** | 302 redirects from short code to original URL |
|  **Validation** | URL format validation with meaningful error messages |
|  **Docker Ready** | Dockerfile included for containerized deployment |
|  **H2 Console** | In-memory DB with web console for development |

---

##  Quick Start

### Prerequisites
- Java 21+
- Maven 3.9+
- (Optional) Docker

### 1. Clone & Run

```bash
git clone https://github.com/ashleythabang47-cloud/url-shortener.git
cd url-shortener
mvn spring-boot:run
```

The API will be available at `http://localhost:8080`.

### 2. Create a Short URL

```bash
curl -X POST http://localhost:8080/api/shorten   -H "Content-Type: application/json"   -d '{
    "url": "https://www.google.com/search?q=spring+boot",
    "customAlias": "spring-search",
    "expiresInDays": 7
  }'
```

**Response:**
```json
{
  "shortUrl": "http://localhost:8080/spring-search",
  "originalUrl": "https://www.google.com/search?q=spring+boot",
  "shortCode": "spring-search",
  "createdAt": "2026-07-26T15:30:00",
  "expiresAt": "2026-08-02T15:30:00"
}
```

### 3. Visit the Short URL

Open `http://localhost:8080/spring-search` in your browser — you'll be redirected instantly.

---

##  Docker

```bash
# Build the image
docker build -t url-shortener .

# Run the container
docker run -p 8080:8080 url-shortener
```

---

##  API Reference

### Shorten a URL
```http
POST /api/shorten
Content-Type: application/json
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `url` | string | Yes | The original long URL |
| `customAlias` | string | No | Custom short code (max 10 chars) |
| `expiresInDays` | integer | No | Days until the link expires |

### Redirect
```http
GET /{shortCode}
```
Returns `302 Found` with `Location` header pointing to the original URL.

### H2 Console (Dev Only)
```
http://localhost:8080/h2-console
JDBC URL: jdbc:h2:mem:urlshortener
```

---

##  Project Structure

```
url-shortener/
├── src/main/java/com/example/urlshortener/
│   ├── controller/          # REST endpoints
│   ├── service/             # Business logic & Base62 encoding
│   ├── repository/          # JPA data access
│   ├── model/               # Entity definitions
│   ├── dto/                 # Request/Response objects
│   ├── exception/           # Global error handling
│   └── UrlShortenerApplication.java
├── src/main/resources/
│   └── application.yml      # App configuration
├── pom.xml
└── Dockerfile
```

---

##  Configuration

Edit `src/main/resources/application.yml`:

```yaml
app:
  base-url: https://yourdomain.com   # Production domain

spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/shortener  # Switch to PostgreSQL
```

---

##  Roadmap

- [ ] Redis caching for hot links
- [ ] Rate limiting per IP
- [ ] Analytics dashboard (clicks over time, referrers)
- [ ] QR code generation for short URLs
- [ ] OAuth2 / API key authentication

---

##  Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you'd like to change.

1. Fork the repo
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

##  License

This project is Built for Educational Purpose.

---

<p align="center">Built with Coffe and Spring Boot</p>
