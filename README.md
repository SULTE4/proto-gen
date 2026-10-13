<div align="center">

# proto-gen

**Go code generated from [SULTE4/protos](https://github.com/SULTE4/protos). Don't edit by hand.**

A GitHub Action runs `protoc` over every `.proto` in the protos repo and commits the `.pb.go`<br>
and `_grpc.pb.go` files here, so services can `go get` the contracts.

![Go](https://img.shields.io/badge/Go-generated-00ADD8?logo=go&logoColor=white)
![gRPC](https://img.shields.io/badge/gRPC-protoc--gen--go--grpc-244c5a?logo=grpc&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/CI-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)

</div>

---

## How it works

```
 push to main
     │
     ▼
 .github/workflows/generate.yml
     ├─ git clone SULTE4/protos
     ├─ install protoc, protoc-gen-go, protoc-gen-go-grpc
     ├─ protoc every *.proto  (paths=source_relative)
     └─ commit "Auto-generate .pb.go files from protos" and push
     │
     ▼
 user/user.pb.go, user/user_grpc.pb.go, ...
```

The workflow pushes with the `PAT_TOKEN` repository secret.

> **Status:** no generated code is committed yet. The only workflow run so far (April 2026) failed before `PAT_TOKEN` was added. The next push to `main` will run it again.

## Usage

Once the code is generated and the repo has a `go.mod`:

```go
import userpb "github.com/SULTE4/proto-gen/user"
```

## Changing a contract

Edit the `.proto` in [protos](https://github.com/SULTE4/protos), never the generated files here. Then trigger the workflow by pushing to this repo's `main`.

## Roadmap

- [ ] Trigger generation from a push to `protos` (`repository_dispatch`) instead of a push here
- [ ] `go.mod` for the generated module
