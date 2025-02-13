# class: RequestOptions
* langs: java

The [RequestOptions] allows to create form data to be sent via [APIRequestContext]. Playwright will automatically
determine content type of the request.

```java
context.request().post(
  "https://example.com/submit",
  RequestOptions.create()
    .setQueryParam("page", 1)
    .setData("My data"));
```

**Uploading html form data**

[FormData] class can be used to send a form to the server, by default the request will use `application/x-www-form-urlencoded` encoding:

```java
context.request().post("https://example.com/signup", RequestOptions.create().setForm(
  FormData.create()
    .set("firstName", "John")
    .set("lastName", "Doe")));
```

You can also send files as fields of an html form. The data will be encoded using [`multipart/form-data`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST):

```java
Path path = Paths.get("members.csv");
APIResponse response = context.request().post("https://example.com/upload_members",
  RequestOptions.create().setMultipart(FormData.create().set("membersList", path)));
```

Alternatively, you can build the file payload manually:
```java
FilePayload filePayload = new FilePayload("members.csv", "text/csv",
  "Alice, 33\nJohn, 35\n".getBytes(StandardCharsets.UTF_8));
APIResponse response = context.request().post("https://example.com/upload_members",
  RequestOptions.create().setMultipart(FormData.create().set("membersList", filePayload)));
```

## method: RequestOptions.create
- returns: <[RequestOptions]>

Creates new instance of [RequestOptions].

## method: RequestOptions.setData
- returns: <[RequestOptions]>

Sets the request's post data.

### param: RequestOptions.setData.data
- `data` <[string]|[Buffer]|[Serializable]>

Allows to set post data of the request. If the data parameter is an object, it will be serialized to json string
and `content-type` header will be set to `application/json` if not explicitly set. Otherwise the `content-type` header will be
set to `application/octet-stream` if not explicitly set.

## method: RequestOptions.setFailOnStatusCode
- returns: <[RequestOptions]>

### param: RequestOptions.setFailOnStatusCode.failOnStatusCode
- `failOnStatusCode` <[boolean]>

Whether to throw on response codes other than 2xx and 3xx. By default response object is returned
for all status codes.

## method: RequestOptions.setForm
- returns: <[RequestOptions]>

Provides [FormData] object that will be serialized as html form using `application/x-www-form-urlencoded` encoding and sent as
this request body. If this parameter is specified `content-type` header will be set to `application/x-www-form-urlencoded`
unless explicitly provided.

### param: RequestOptions.setForm.form
- `form` <[FormData]>

Form data to be serialized as html form using `application/x-www-form-urlencoded` encoding and sent as
this request body.

## method: RequestOptions.setHeader
- returns: <[RequestOptions]>

Sets an HTTP header to the request.

### param: RequestOptions.setHeader.name
- `name` <[string]>

Header name.

### param: RequestOptions.setHeader.value
- `value` <[string]>

Header value.

## method: RequestOptions.setIgnoreHTTPSErrors
- returns: <[RequestOptions]>

### param: RequestOptions.setIgnoreHTTPSErrors.ignoreHTTPSErrors
- `ignoreHTTPSErrors` <[boolean]>

Whether to ignore HTTPS errors when sending network requests.

## method: RequestOptions.setMethod
- returns: <[RequestOptions]>

Changes the request method (e.g. [PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT) or
[POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST)).

### param: RequestOptions.setMethod.method
- `method` <[string]>

Request method, e.g. [POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST).

## method: RequestOptions.setMultipart
- returns: <[RequestOptions]>

Provides [FormData] object that will be serialized as html form using `multipart/form-data` encoding and sent as
this request body. If this parameter is specified `content-type` header will be set to `multipart/form-data`
unless explicitly provided.

### param: RequestOptions.setMultipart.form
- `form` <[FormData]>

Form data to be serialized as html form using `multipart/form-data` encoding and sent as
this request body.

## method: RequestOptions.setQueryParam
- returns: <[RequestOptions]>

Adds a query parameter to the request URL.

### param: RequestOptions.setQueryParam.name
- `name` <[string]>

Parameter name.

### param: RequestOptions.setQueryParam.value
- `value` <[string]|[boolean]|[int]>

Parameter value.

## method: RequestOptions.setTimeout
- returns: <[RequestOptions]>

Sets request timeout in milliseconds. Defaults to `30000` (30 seconds). Pass `0` to disable timeout.

### param: RequestOptions.setTimeout.timeout
- `timeout` <[float]>

Request timeout in milliseconds.
