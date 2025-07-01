# API Design Guidelines

**Comprehensive guidelines for creating robust, scalable, and maintainable APIs across all technologies and languages.**

---

## 🎯 Core Design Philosophy

### The Golden Rule
**"Design for the consumer, not the provider"** - APIs should be intuitive, consistent, and valuable to the developers who use them.

---

## 📈 Richardson Maturity Model (RMM) Framework

### **Mandatory: Level 2 (HTTP Verbs)**
All APIs **MUST** implement Level 2 as the minimum standard:

```http
✅ Level 2 Requirements:
GET    /api/users/123        # Retrieve user
POST   /api/users            # Create user
PUT    /api/users/123        # Update user (full)
PATCH  /api/users/123        # Update user (partial)
DELETE /api/users/123        # Delete user

# Proper status codes
200 OK, 201 Created, 204 No Content
400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found
500 Internal Server Error
```

### **Selective: Level 3 (Hypermedia Controls)**
Apply Level 3 strategically for maximum value:

#### **When to Use Level 3:**
- **Public APIs**: External developers benefit from discoverability
- **Complex Workflows**: Multi-step processes with state transitions
- **Frequently Evolving APIs**: Reduce client coupling
- **Integration Platforms**: APIs that orchestrate other services

#### **Level 3 Implementation:**
```json
{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com",
  "_links": {
    "self": { "href": "/api/users/123" },
    "edit": { "href": "/api/users/123", "method": "PUT" },
    "delete": { "href": "/api/users/123", "method": "DELETE" },
    "orders": { "href": "/api/users/123/orders" }
  }
}
```

#### **When to Skip Level 3:**
- **Internal APIs**: Team-controlled consumption
- **Simple CRUD**: Basic data operations
- **Resource Constraints**: Limited development/maintenance time
- **Performance Critical**: Minimal payload requirements

### **Decision Framework:**
```
API Complexity Assessment
│
├─ Simple CRUD Operations → Level 2
├─ Internal Team APIs → Level 2
├─ Public/Partner APIs → Consider Level 3
├─ Complex Workflows → Level 3 Recommended
└─ High-Traffic APIs → Level 2 (performance priority)
```

---

## 🔒 Security Best Practices

### **Authentication & Authorization**
```http
# JWT Bearer Token (Recommended)
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...

# API Key (For simple services)
X-API-Key: your-api-key-here

# OAuth 2.0 (For third-party access)
Authorization: Bearer oauth-access-token
```

### **Input Validation**
```json
// Request validation schema
{
  "email": {
    "type": "string",
    "format": "email",
    "required": true
  },
  "age": {
    "type": "integer",
    "minimum": 0,
    "maximum": 150
  }
}
```

### **Security Headers**
```http
Content-Security-Policy: default-src 'self'
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block
Strict-Transport-Security: max-age=31536000
```

### **Rate Limiting**
```http
# Response headers
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 89
X-RateLimit-Reset: 1640995200
Retry-After: 3600
```

### **Security Checklist**
- [ ] HTTPS enforced in production
- [ ] All inputs validated and sanitized
- [ ] Sensitive data never logged
- [ ] Rate limiting implemented
- [ ] Authentication required for protected resources
- [ ] SQL injection prevention
- [ ] CORS configured properly

---

## ⚡ Performance Optimization

### **Pagination Strategy**
```http
# Cursor-based (Recommended for large datasets)
GET /api/users?cursor=eyJpZCI6MTIzfQ&limit=20

# Offset-based (Simple but less performant)
GET /api/users?page=2&limit=20

# Response format
{
  "data": [...],
  "pagination": {
    "next_cursor": "eyJpZCI6MTQzfQ",
    "has_more": true,
    "total_count": 1500
  }
}
```

### **Caching Strategy**
```http
# HTTP Caching
Cache-Control: public, max-age=3600
ETag: "33a64df551425fcc55e4d42a148795d9f25f89d4"
Last-Modified: Wed, 21 Oct 2015 07:28:00 GMT

# Conditional requests
If-None-Match: "33a64df551425fcc55e4d42a148795d9f25f89d4"
If-Modified-Since: Wed, 21 Oct 2015 07:28:00 GMT
```

### **Query Optimization**
```http
# Field selection (avoid over-fetching)
GET /api/users?fields=id,name,email

# Filtering
GET /api/users?status=active&created_after=2023-01-01

# Sorting
GET /api/users?sort=-created_at,name
```

### **N+1 Query Prevention**
```json
// Include related data in single request
{
  "user": {
    "id": 123,
    "name": "John Doe",
    "orders": [
      {"id": 1, "total": 100},
      {"id": 2, "total": 200}
    ]
  }
}
```

---

## 🚨 Error Handling Excellence

### **Standardized Error Format (RFC 9457)**
```json
{
  "type": "https://example.com/probs/validation-error",
  "title": "Validation Error",
  "status": 400,
  "detail": "The request body contains invalid data",
  "instance": "/api/users",
  "trace_id": "abc123",
  "errors": [
    {
      "field": "email",
      "code": "INVALID_FORMAT",
      "message": "Email format is invalid"
    }
  ]
}
```

### **HTTP Status Code Usage**
```http
# Success
200 OK          # Successful GET, PUT, PATCH
201 Created     # Successful POST
204 No Content  # Successful DELETE

# Client Errors
400 Bad Request         # Invalid request syntax
401 Unauthorized        # Authentication required
403 Forbidden          # Valid request, access denied
404 Not Found          # Resource doesn't exist
409 Conflict           # Resource state conflict
422 Unprocessable Entity # Valid syntax, semantic errors
429 Too Many Requests   # Rate limit exceeded

# Server Errors
500 Internal Server Error # Generic server error
502 Bad Gateway          # Upstream service error
503 Service Unavailable  # Temporary service issue
```

### **Error Response Examples**
```json
// 400 Bad Request
{
  "type": "validation-error",
  "title": "Invalid Request Data",
  "status": 400,
  "errors": [
    {
      "field": "email",
      "message": "Valid email address is required"
    }
  ]
}

// 404 Not Found
{
  "type": "resource-not-found",
  "title": "User Not Found",
  "status": 404,
  "detail": "User with ID 123 does not exist"
}

// 500 Internal Server Error
{
  "type": "internal-error",
  "title": "Internal Server Error",
  "status": 500,
  "detail": "An unexpected error occurred",
  "trace_id": "req_abc123xyz"
}
```

---

## 🔄 Versioning Strategies

### **URL Versioning (Recommended)**
```http
# Version in URL path
GET /api/v1/users
GET /api/v2/users

# Advantages: Clear, cache-friendly, easy to route
# Use for: Public APIs, major breaking changes
```

### **Header Versioning**
```http
# Custom header
API-Version: 2023-01-15

# Accept header
Accept: application/vnd.api+json;version=2

# Advantages: Clean URLs, fine-grained control
# Use for: Internal APIs, minor variations
```

### **Backward Compatibility Strategy**
```json
// Additive changes (non-breaking)
{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "+1-555-0123",  // ✅ New optional field
  "created_at": "2023-01-15T10:30:00Z"
}

// Breaking changes (require new version)
{
  "user_id": 123,           // ❌ Renamed field
  "full_name": "John Doe",  // ❌ Renamed field
  "contact": {              // ❌ Restructured data
    "email": "john@example.com",
    "phone": "+1-555-0123"
  }
}
```

### **Version Lifecycle Management**
```http
# Deprecation notice
Sunset: Wed, 11 Nov 2024 23:59:59 GMT
Warning: 299 - "Deprecated API, use /api/v2/users instead"

# Version support timeline
v1: 2023-01-01 → 2024-12-31 (2 years)
v2: 2023-06-01 → 2025-06-01 (2 years)
v3: 2024-01-01 → 2026-01-01 (2 years)
```

---

## 📝 Documentation & Developer Experience

### **OpenAPI Specification**
```yaml
openapi: 3.0.0
info:
  title: User Management API
  version: 1.0.0
  description: Comprehensive user management system

paths:
  /users:
    get:
      summary: List users
      parameters:
        - name: limit
          in: query
          schema:
            type: integer
            minimum: 1
            maximum: 100
            default: 20
      responses:
        '200':
          description: List of users
          content:
            application/json:
              schema:
                type: object
                properties:
                  data:
                    type: array
                    items:
                      $ref: '#/components/schemas/User'
```

### **Request/Response Examples**
```json
// POST /api/users
{
  "name": "John Doe",
  "email": "john@example.com",
  "role": "user"
}

// Response: 201 Created
{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com",
  "role": "user",
  "created_at": "2023-01-15T10:30:00Z",
  "updated_at": "2023-01-15T10:30:00Z"
}
```

### **SDK & Client Libraries**
```javascript
// Official JavaScript SDK
const api = new UserAPI({ apiKey: 'your-key' });
const user = await api.users.create({
  name: 'John Doe',
  email: 'john@example.com'
});
```

---

## 🏗️ Resource Design Patterns

### **RESTful Resource Mapping**
```http
# Collection operations
GET    /api/users           # List users
POST   /api/users           # Create user

# Individual resource operations
GET    /api/users/123       # Get user
PUT    /api/users/123       # Update user (full)
PATCH  /api/users/123       # Update user (partial)
DELETE /api/users/123       # Delete user

# Nested resources
GET    /api/users/123/orders       # User's orders
POST   /api/users/123/orders       # Create order for user
GET    /api/users/123/orders/456   # Specific order
```

### **Complex Operations**
```http
# Actions on resources
POST /api/users/123/activate
POST /api/users/123/reset-password
POST /api/orders/456/cancel

# Bulk operations
POST /api/users/bulk-import
PUT  /api/users/bulk-update
DELETE /api/users/bulk-delete
```

### **Search & Filtering**
```http
# Search endpoint
GET /api/search/users?q=john&fields=name,email

# Advanced filtering
GET /api/users?filter[status]=active&filter[role]=admin
GET /api/users?created_after=2023-01-01&sort=-created_at
```

---

## 🌐 International & Accessibility

### **Internationalization**
```http
# Language negotiation
Accept-Language: en-US,en;q=0.9,ja;q=0.8

# Response with localized content
{
  "message": "User created successfully",
  "message_i18n": {
    "en": "User created successfully",
    "ja": "ユーザーが正常に作成されました",
    "es": "Usuario creado exitosamente"
  }
}
```

### **Date & Time Handling**
```json
{
  "created_at": "2023-01-15T10:30:00Z",        // ISO 8601 UTC
  "updated_at": "2023-01-15T10:30:00+09:00",   // With timezone
  "local_time": "2023-01-15T19:30:00",         // Local time
  "timezone": "Asia/Tokyo"
}
```

### **Currency & Numbers**
```json
{
  "price": {
    "amount": 1299,        // Amount in cents
    "currency": "USD",
    "formatted": "$12.99"
  },
  "locale_data": {
    "country": "US",
    "language": "en",
    "number_format": "1,234.56"
  }
}
```

---

## 📊 Monitoring & Observability

### **Health Checks**
```http
# Basic health check
GET /health
{
  "status": "healthy",
  "timestamp": "2023-01-15T10:30:00Z",
  "version": "1.2.3"
}

# Detailed health check
GET /health/detailed
{
  "status": "healthy",
  "checks": {
    "database": "healthy",
    "redis": "healthy",
    "external_api": "degraded"
  },
  "metrics": {
    "response_time_ms": 45,
    "cpu_usage": 23.5,
    "memory_usage": 67.2
  }
}
```

### **Request Tracing**
```http
# Request headers
X-Request-ID: req_abc123xyz
X-Correlation-ID: corr_def456uvw

# Response headers
X-Request-ID: req_abc123xyz
X-Response-Time: 234ms
```

### **Structured Logging**
```json
{
  "timestamp": "2023-01-15T10:30:00Z",
  "level": "INFO",
  "message": "User created",
  "request_id": "req_abc123xyz",
  "user_id": 123,
  "duration_ms": 234,
  "method": "POST",
  "path": "/api/users",
  "status_code": 201
}
```

---

## 🎯 Quality Assurance Checklist

### **Pre-Development**
- [ ] Requirements clearly defined
- [ ] Resource modeling completed
- [ ] Security requirements identified
- [ ] Performance targets established
- [ ] Documentation plan created

### **During Development**
- [ ] Richardson Maturity Model Level 2 implemented
- [ ] HTTP status codes used correctly
- [ ] Input validation implemented
- [ ] Error handling standardized
- [ ] Authentication/authorization working
- [ ] Rate limiting configured

### **Pre-Production**
- [ ] OpenAPI specification complete
- [ ] Integration tests passing
- [ ] Performance benchmarks met
- [ ] Security scan completed
- [ ] Documentation reviewed
- [ ] Monitoring configured

### **Post-Production**
- [ ] Real-world usage metrics collected
- [ ] Error rates within acceptable limits
- [ ] Performance SLAs met
- [ ] User feedback incorporated
- [ ] Maintenance procedures documented

---

## 🚫 Common Anti-Patterns to Avoid

### **Design Anti-Patterns**
```http
# ❌ RPC-style APIs
POST /api/getUserById
POST /api/createUser
POST /api/updateUserName

# ✅ RESTful design
GET    /api/users/123
POST   /api/users
PATCH  /api/users/123
```

### **Error Handling Anti-Patterns**
```json
// ❌ Generic error responses
{
  "error": "Something went wrong"
}

// ✅ Detailed, actionable errors
{
  "type": "validation-error",
  "title": "Invalid Request Data",
  "status": 400,
  "errors": [
    {
      "field": "email",
      "code": "INVALID_FORMAT",
      "message": "Please provide a valid email address"
    }
  ]
}
```

### **Security Anti-Patterns**
```http
# ❌ Exposing sensitive data
{
  "id": 123,
  "password": "plaintext_password",
  "api_key": "secret_key_123"
}

# ✅ Secure data handling
{
  "id": 123,
  "password_last_changed": "2023-01-15T10:30:00Z"
}
```

---

## 📚 Success Metrics

### **Technical Metrics**
- **Response Time**: < 200ms for 95th percentile
- **Error Rate**: < 1% for 4xx errors, < 0.1% for 5xx errors
- **Availability**: > 99.9% uptime
- **Throughput**: Handle expected load + 50% headroom

### **Developer Experience Metrics**
- **Time to First Success**: < 15 minutes from API key to working request
- **Documentation Completeness**: All endpoints documented with examples
- **SDK Adoption**: Official client libraries available
- **Community Engagement**: Active developer community

### **Business Metrics**
- **API Adoption Rate**: Monthly active API consumers
- **Feature Utilization**: Most/least used endpoints
- **Integration Success**: Successful third-party integrations
- **Support Ticket Volume**: API-related support requests

---

**Remember**: Great APIs are not just technically sound—they solve real problems elegantly and create value for both providers and consumers.