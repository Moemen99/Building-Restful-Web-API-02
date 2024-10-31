# HTTP Methods and Status Codes

## HTTP Methods (Verbs)

```mermaid
graph LR
    CRUD[CRUD Operations] --> C[Create]
    CRUD --> R[Read]
    CRUD --> U[Update]
    CRUD --> D[Delete]
    
    C --> POST[POST]
    R --> GET[GET]
    U --> PUT[PUT]
    D --> DELETE[DELETE]
```

### Main HTTP Methods

| Method | CRUD Operation | Description |
|--------|---------------|-------------|
| POST | Create | Creates new resource on server |
| GET | Read | Retrieves data from server |
| PUT | Update | Updates entire resource |
| DELETE | Delete | Removes resource from server |

## Status Code Groups

```mermaid
graph TD
    A[HTTP Status Codes] --> B[1xx: Informational]
    A --> C[2xx: Success]
    A --> D[3xx: Redirection]
    A --> E[4xx: Client Error]
    A --> F[5xx: Server Error]
```

### Detailed Status Code Breakdown

#### 2xx Success Codes
| Code | Name | Description |
|------|------|-------------|
| 200 | OK | Request successful, resource returned |
| 201 | Created | Resource created successfully |
| 202 | Accepted | Request accepted but processing not completed |
| 204 | No Content | Request successful, no content to return |

```mermaid
sequenceDiagram
    participant Client
    participant Server
    
    Client->>Server: POST /api/resources
    Server->>Client: 201 Created
    Note over Server,Client: Response includes resource location
    
    Client->>Server: GET /api/resources/123
    Server->>Client: 200 OK
    Note over Server,Client: Response includes resource
    
    Client->>Server: DELETE /api/resources/123
    Server->>Client: 204 No Content
```

#### 4xx Client Error Codes
| Code | Name | Description |
|------|------|-------------|
| 400 | Bad Request | Invalid request data or format |
| 401 | Unauthorized | Authentication required |
| 404 | Not Found | Resource doesn't exist |
| 405 | Method Not Allowed | HTTP method not supported |

#### 5xx Server Error Codes
| Code | Name | Description |
|------|------|-------------|
| 500 | Internal Server Error | Server encountered an error |

## Common Use Cases

### POST (Create)
```mermaid
sequenceDiagram
    participant Client
    participant Server
    Client->>Server: POST /api/users
    Note right of Client: User data in request body
    Server->>Client: 201 Created
    Note left of Server: Returns created resource
```

### GET (Read)
```mermaid
sequenceDiagram
    participant Client
    participant Server
    Client->>Server: GET /api/users/123
    Server->>Client: 200 OK
    Note left of Server: Returns requested resource
```

### PUT (Update)
```mermaid
sequenceDiagram
    participant Client
    participant Server
    Client->>Server: PUT /api/users/123
    Note right of Client: Complete resource in body
    Server->>Client: 204 No Content
```

### DELETE (Remove)
```mermaid
sequenceDiagram
    participant Client
    participant Server
    Client->>Server: DELETE /api/users/123
    Server->>Client: 204 No Content
```

## Status Code Response Examples

### Successful Operations
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "id": 123,
    "name": "John Doe"
}
```

### Resource Creation
```http
HTTP/1.1 201 Created
Location: /api/resources/123
Content-Type: application/json

{
    "id": 123,
    "status": "created"
}
```

### Client Errors
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
    "error": "Invalid data format",
    "details": "Name field is required"
}
```

## Best Practices
1. Use appropriate HTTP methods for CRUD operations
2. Return correct status codes
3. Include meaningful error messages
4. Follow RESTful conventions
5. Maintain consistency in API responses

---
*Note: Understanding HTTP methods and status codes is crucial for building robust and reliable web applications and APIs.*




# URI (Uniform Resource Identifier) Structure

## Basic Structure

```mermaid
graph LR
    URI --> Mandatory[Mandatory Components]
    URI --> Optional[Optional Components]
    
    Mandatory --> A[Scheme]
    Mandatory --> B[Authority]
    
    Optional --> C[Path]
    Optional --> D[Query]
    Optional --> E[Fragment]
```

## Components Breakdown

### Mandatory Components

#### 1. Scheme
- Defines protocol for server communication
- Common schemes:
  - `http://` (standard)
  - `https://` (secure)
- Always ends with `://`
- Automatically added by browsers
- Visible when URI is copied

#### 2. Authority
- Format: `hostname[:port]`
- Examples:
  - Development: `localhost:3000`
  - Production: `www.example.com`
- Separated from scheme by `://`

```mermaid
graph TD
    A[URI Example] --> B[https://www.example.com/path]
    B --> C[Scheme: https://]
    B --> D[Authority: www.example.com]
```

### Optional Components

#### 1. Path
- Follows authority
- Can have multiple segments
- Example: `/users/profile/settings`
- Used to identify specific resources

#### 2. Query String
- Starts with `?`
- Format: `key=value`
- Multiple parameters joined by `&`
- Example: `?year=2024&month=1`

#### 3. Fragment
- Starts with `#`
- Used for page navigation
- Points to specific HTML section
- Example: `#section-1`

## Example URIs

### Basic URI
```
https://www.devcreed.com/courses/add
└─┬──┘ └─────┬─────┘ └───┬───┘
  │          │          │
Scheme   Authority     Path
```

### Complex URI with All Components
```
https://www.devcreed.com/courses?year=2024&month=1#api-course
└─┬──┘ └─────┬─────┘ └─┬─┘ └─────┬─────┘ └───┬──┘
  │          │         │         │           │
Scheme   Authority   Path      Query     Fragment
```

## Common Use Cases

### Development Environment
```
http://localhost:3000/api/users
```

### Production Environment
```
https://www.example.com/api/users
```

### With Query Parameters
```
https://api.example.com/products?category=electronics&sort=price
```

### With Fragment
```
https://docs.example.com/guide#installation-steps
```

## Best Practices

1. **Security**
   - Use HTTPS when possible
   - Be careful with sensitive data in URLs

2. **Query Parameters**
   - Use meaningful parameter names
   - Encode special characters
   - Keep URLs reasonably short

3. **Path Structure**
   - Use logical hierarchy
   - Follow RESTful conventions
   - Use lowercase letters
   - Use hyphens for spaces

4. **Fragment Usage**
   - Use for page navigation
   - Keep identifiers meaningful
   - Consider SEO implications

---
*Note: Understanding URI structure is crucial for web development and API design.*
