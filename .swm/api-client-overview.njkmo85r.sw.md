---
title: API Client Overview
---
# API Client Overview

The API Client is a key component that facilitates communication between the application and the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken>. It is responsible for sending requests to the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken> and handling the responses. The API Client uses <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="7:4:4" line-data="It translates gRPC into RESTful JSON APIs.">`gRPC`</SwmToken> to communicate with the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken>, ensuring efficient and reliable message exchange.

## Why API Client is used

The API Client is used to facilitate communication between the application and the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken>. It ensures that requests are sent and responses are handled efficiently and reliably, abstracting the complexities of direct service communication.

## How to use the API Client

The API Client uses <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="7:4:4" line-data="It translates gRPC into RESTful JSON APIs.">`gRPC`</SwmToken> to communicate with the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken>. Functions like <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="37:2:2" line-data="func request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_GetRolloutInfo_0`</SwmToken> and <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="75:2:2" line-data="func local_request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_GetRolloutInfo_0`</SwmToken> demonstrate how the API Client constructs requests and processes responses. It handles various operations such as getting rollout information, watching rollout updates, and managing rollout actions like promotion, abortion, and image setting.

<SwmSnippet path="/pkg/apiclient/rollout/rollout.pb.go" line="1899">

---

The <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:2:2" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutServiceClient`</SwmToken> is the client API for the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken>, which uses <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="7:4:4" line-data="It translates gRPC into RESTful JSON APIs.">`gRPC`</SwmToken> for communication.

```go
// RolloutServiceClient is the client API for RolloutService service.
//
// For semantics around ctx use and closing/ending streaming RPCs, please refer to https://godoc.org/google.golang.org/grpc#ClientConn.NewStream.
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/rollout/rollout.pb.go" line="2079">

---

The <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="2079:2:2" line-data="// RolloutServiceServer is the server API for RolloutService service.">`RolloutServiceServer`</SwmToken> is the server API for the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="2079:14:14" line-data="// RolloutServiceServer is the server API for RolloutService service.">`RolloutService`</SwmToken>, complementing the client API.

```go
// RolloutServiceServer is the server API for RolloutService service.
```

---

</SwmSnippet>

## Main functions

There are several main functions in this folder. Some of them are <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="37:2:2" line-data="func request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_GetRolloutInfo_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="75:2:2" line-data="func local_request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_GetRolloutInfo_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="113:2:2" line-data="func request_RolloutService_WatchRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (RolloutService_WatchRolloutInfoClient, runtime.ServerMetadata, error) {">`request_RolloutService_WatchRolloutInfo_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="159:2:2" line-data="func request_RolloutService_ListRolloutInfos_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_ListRolloutInfos_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="186:2:2" line-data="func local_request_RolloutService_ListRolloutInfos_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_ListRolloutInfos_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="213:2:2" line-data="func request_RolloutService_WatchRolloutInfos_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (RolloutService_WatchRolloutInfosClient, runtime.ServerMetadata, error) {">`request_RolloutService_WatchRolloutInfos_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="248:2:2" line-data="func request_RolloutService_GetNamespace_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_GetNamespace_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="257:2:2" line-data="func local_request_RolloutService_GetNamespace_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_GetNamespace_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="266:2:2" line-data="func request_RolloutService_RestartRollout_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_RestartRollout_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="312:2:2" line-data="func local_request_RolloutService_RestartRollout_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_RestartRollout_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="358:2:2" line-data="func request_RolloutService_PromoteRollout_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_PromoteRollout_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="404:2:2" line-data="func local_request_RolloutService_PromoteRollout_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_PromoteRollout_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="450:2:2" line-data="func request_RolloutService_AbortRollout_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_AbortRollout_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="496:2:2" line-data="func local_request_RolloutService_AbortRollout_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_AbortRollout_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="542:2:2" line-data="func request_RolloutService_SetRolloutImage_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_SetRolloutImage_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="621:2:2" line-data="func local_request_RolloutService_SetRolloutImage_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_SetRolloutImage_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="700:2:2" line-data="func request_RolloutService_UndoRollout_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_UndoRollout_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="757:2:2" line-data="func local_request_RolloutService_UndoRollout_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_UndoRollout_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="814:2:2" line-data="func request_RolloutService_RetryRollout_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_RetryRollout_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="860:2:2" line-data="func local_request_RolloutService_RetryRollout_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_RetryRollout_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="906:2:2" line-data="func request_RolloutService_Version_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_Version_0`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="915:2:2" line-data="func local_request_RolloutService_Version_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_Version_0`</SwmToken>. We will dive a little into <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="37:2:2" line-data="func request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_GetRolloutInfo_0`</SwmToken> and <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="75:2:2" line-data="func local_request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_GetRolloutInfo_0`</SwmToken>.

### <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="37:2:2" line-data="func request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_GetRolloutInfo_0`</SwmToken>

The <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="37:2:2" line-data="func request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_GetRolloutInfo_0`</SwmToken> function constructs a request to get rollout information. It extracts parameters from the HTTP request, converts them to the appropriate types, and sends the request to the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken>. The response is then returned to the caller.

<SwmSnippet path="/pkg/apiclient/rollout/rollout.pb.gw.go" line="37">

---

The function <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="37:2:2" line-data="func request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_GetRolloutInfo_0`</SwmToken> constructs a request to get rollout information by extracting parameters from the HTTP request and converting them to the appropriate types.

```go
func request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {
	var protoReq RolloutInfoQuery
	var metadata runtime.ServerMetadata

	var (
		val string
		ok  bool
		err error
		_   = err
	)

	val, ok = pathParams["namespace"]
	if !ok {
		return nil, metadata, status.Errorf(codes.InvalidArgument, "missing parameter %s", "namespace")
	}

	protoReq.Namespace, err = runtime.String(val)

	if err != nil {
		return nil, metadata, status.Errorf(codes.InvalidArgument, "type mismatch, parameter: %s, error: %v", "namespace", err)
	}
```

---

</SwmSnippet>

### <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="75:2:2" line-data="func local_request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_GetRolloutInfo_0`</SwmToken>

The <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="75:2:2" line-data="func local_request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_GetRolloutInfo_0`</SwmToken> function is similar to <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="37:2:2" line-data="func request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_GetRolloutInfo_0`</SwmToken>, but it handles the request locally on the server side. It processes the HTTP request, extracts the necessary parameters, and calls the <SwmToken path="server/server.go" pos="191:9:9" line-data="func (s *ArgoRolloutsServer) GetRolloutInfo(c context.Context, q *rollout.RolloutInfoQuery) (*rollout.RolloutInfo, error) {">`GetRolloutInfo`</SwmToken> method on the server.

<SwmSnippet path="/pkg/apiclient/rollout/rollout.pb.gw.go" line="75">

---

The function <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="75:2:2" line-data="func local_request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`local_request_RolloutService_GetRolloutInfo_0`</SwmToken> handles the request locally on the server side by processing the HTTP request and extracting the necessary parameters.

```go
func local_request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, server RolloutServiceServer, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {
	var protoReq RolloutInfoQuery
	var metadata runtime.ServerMetadata

	var (
		val string
		ok  bool
		err error
		_   = err
	)

	val, ok = pathParams["namespace"]
	if !ok {
		return nil, metadata, status.Errorf(codes.InvalidArgument, "missing parameter %s", "namespace")
	}

	protoReq.Namespace, err = runtime.String(val)

	if err != nil {
		return nil, metadata, status.Errorf(codes.InvalidArgument, "type mismatch, parameter: %s, error: %v", "namespace", err)
	}
```

---

</SwmSnippet>

## Rollout <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="7:12:12" line-data="It translates gRPC into RESTful JSON APIs.">`APIs`</SwmToken>

The Rollout <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="7:12:12" line-data="It translates gRPC into RESTful JSON APIs.">`APIs`</SwmToken> provide various endpoints to interact with the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken>.

### <SwmToken path="server/server.go" pos="191:9:9" line-data="func (s *ArgoRolloutsServer) GetRolloutInfo(c context.Context, q *rollout.RolloutInfoQuery) (*rollout.RolloutInfo, error) {">`GetRolloutInfo`</SwmToken>

The <SwmToken path="server/server.go" pos="191:9:9" line-data="func (s *ArgoRolloutsServer) GetRolloutInfo(c context.Context, q *rollout.RolloutInfoQuery) (*rollout.RolloutInfo, error) {">`GetRolloutInfo`</SwmToken> endpoint retrieves information about a specific rollout. The function <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="37:2:2" line-data="func request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_GetRolloutInfo_0`</SwmToken> constructs the request by extracting the <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="48:11:11" line-data="	val, ok = pathParams[&quot;namespace&quot;]">`namespace`</SwmToken> and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list.go" pos="14:1:1" line-data="	name          string">`name`</SwmToken> from the path parameters and sends it to the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken>. The response contains detailed information about the rollout.

<SwmSnippet path="/pkg/apiclient/rollout/rollout.pb.gw.go" line="37">

---

The function <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="37:2:2" line-data="func request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_GetRolloutInfo_0`</SwmToken> constructs the request by extracting the <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="48:11:11" line-data="	val, ok = pathParams[&quot;namespace&quot;]">`namespace`</SwmToken> and <SwmToken path="pkg/kubectl-argo-rollouts/cmd/list/list.go" pos="14:1:1" line-data="	name          string">`name`</SwmToken> from the path parameters and sends it to the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken>.

```go
func request_RolloutService_GetRolloutInfo_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {
	var protoReq RolloutInfoQuery
	var metadata runtime.ServerMetadata

	var (
		val string
		ok  bool
		err error
		_   = err
	)

	val, ok = pathParams["namespace"]
	if !ok {
		return nil, metadata, status.Errorf(codes.InvalidArgument, "missing parameter %s", "namespace")
	}

	protoReq.Namespace, err = runtime.String(val)

	if err != nil {
		return nil, metadata, status.Errorf(codes.InvalidArgument, "type mismatch, parameter: %s, error: %v", "namespace", err)
	}
```

---

</SwmSnippet>

### <SwmToken path="server/server.go" pos="380:9:9" line-data="func (s *ArgoRolloutsServer) SetRolloutImage(ctx context.Context, q *rollout.SetImageRequest) (*v1alpha1.Rollout, error) {">`SetRolloutImage`</SwmToken>

The <SwmToken path="server/server.go" pos="380:9:9" line-data="func (s *ArgoRolloutsServer) SetRolloutImage(ctx context.Context, q *rollout.SetImageRequest) (*v1alpha1.Rollout, error) {">`SetRolloutImage`</SwmToken> endpoint updates the image of a specific container in a rollout. The function <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="542:2:2" line-data="func request_RolloutService_SetRolloutImage_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_SetRolloutImage_0`</SwmToken> constructs the request by extracting the <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="48:11:11" line-data="	val, ok = pathParams[&quot;namespace&quot;]">`namespace`</SwmToken>, <SwmToken path="test/fixtures/common.go" pos="62:1:1" line-data="	rollout *unstructured.Unstructured">`rollout`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="137:17:17" line-data="	Container            string   `protobuf:&quot;bytes,2,opt,name=container,proto3&quot; json:&quot;container,omitempty&quot;`">`container`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="138:17:17" line-data="	Image                string   `protobuf:&quot;bytes,3,opt,name=image,proto3&quot; json:&quot;image,omitempty&quot;`">`image`</SwmToken>, and <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="139:17:17" line-data="	Tag                  string   `protobuf:&quot;bytes,4,opt,name=tag,proto3&quot; json:&quot;tag,omitempty&quot;`">`tag`</SwmToken> from the path parameters and sends it to the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken>. The response confirms the update of the image.

<SwmSnippet path="/pkg/apiclient/rollout/rollout.pb.gw.go" line="542">

---

The function <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="542:2:2" line-data="func request_RolloutService_SetRolloutImage_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {">`request_RolloutService_SetRolloutImage_0`</SwmToken> constructs the request by extracting the <SwmToken path="pkg/apiclient/rollout/rollout.pb.gw.go" pos="561:11:11" line-data="	val, ok = pathParams[&quot;namespace&quot;]">`namespace`</SwmToken>, <SwmToken path="test/fixtures/common.go" pos="62:1:1" line-data="	rollout *unstructured.Unstructured">`rollout`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="137:17:17" line-data="	Container            string   `protobuf:&quot;bytes,2,opt,name=container,proto3&quot; json:&quot;container,omitempty&quot;`">`container`</SwmToken>, <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="138:17:17" line-data="	Image                string   `protobuf:&quot;bytes,3,opt,name=image,proto3&quot; json:&quot;image,omitempty&quot;`">`image`</SwmToken>, and <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="139:17:17" line-data="	Tag                  string   `protobuf:&quot;bytes,4,opt,name=tag,proto3&quot; json:&quot;tag,omitempty&quot;`">`tag`</SwmToken> from the path parameters and sends it to the <SwmToken path="pkg/apiclient/rollout/rollout.pb.go" pos="1899:14:14" line-data="// RolloutServiceClient is the client API for RolloutService service.">`RolloutService`</SwmToken>.

```go
func request_RolloutService_SetRolloutImage_0(ctx context.Context, marshaler runtime.Marshaler, client RolloutServiceClient, req *http.Request, pathParams map[string]string) (proto.Message, runtime.ServerMetadata, error) {
	var protoReq SetImageRequest
	var metadata runtime.ServerMetadata

	newReader, berr := utilities.IOReaderFactory(req.Body)
	if berr != nil {
		return nil, metadata, status.Errorf(codes.InvalidArgument, "%v", berr)
	}
	if err := marshaler.NewDecoder(newReader()).Decode(&protoReq); err != nil && err != io.EOF {
		return nil, metadata, status.Errorf(codes.InvalidArgument, "%v", err)
	}

	var (
		val string
		ok  bool
		err error
		_   = err
	)

	val, ok = pathParams["namespace"]
	if !ok {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28tcm9sbG91dHMtZGVtbyUzQSUzQVN3aW1tLURlbW8=" repo-name="intuit-argo-rollouts-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
