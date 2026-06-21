# ZenXBattle Common Proto

Shared Protocol Buffer definitions for all ZenXBattle gRPC services. Single source of truth for service contracts.

## Services Defined

| Proto | Service | Description |
|-------|---------|-------------|
| `AuthUserAdminService/authuseradmin.proto` | AuthUserAdmin | User auth, admin operations |
| `ChallengeService/challenge.proto` | Challenge | Real-time battle orchestration |
| `ProblemsService/problemsservice.proto` | ProblemService | Coding problem CRUD |

## Usage

```go
// Import in any service
import (
    auth "github.com/zenxbattle/CommonProto/AuthUserAdminService"
    challenge "github.com/zenxbattle/CommonProto/ChallengeService"
    problems "github.com/zenxbattle/CommonProto/ProblemsService"
)

// Generate stubs
make proto  # regenerates all .pb.go files
```

## Regenerate Protos

```bash
# Install protoc + Go plugins
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest

# Generate
protoc --go_out=. --go_opt=paths=source_relative \
       --go-grpc_out=. --go-grpc_opt=paths=source_relative \
       */*.proto
```

## Conventions

- Service packages named after the service (e.g., `AuthUserAdminService/`)
- All gRPC methods follow `Service/Method` naming
- Request/Response messages suffixed with `Request`/`Response`
- Field numbers never reused — always add new fields at the end

## Related Services

- [ApiGateway](https://github.com/zenxbattle/ApiGateway) — consumes these protos for gRPC clients
- [AuthUserAdminService](https://github.com/zenxbattle/AuthUserAdminService) — implements auth proto
- [ChallengeService](https://github.com/zenxbattle/ChallengeService) — implements challenge proto
- [ProblemService](https://github.com/zenxbattle/ProblemService) — implements problem proto
