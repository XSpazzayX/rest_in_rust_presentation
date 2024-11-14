---
marp: true
theme: uncover
paginate: true
---


# Rest in Rust

Writing REST API wrapper libraries and CLIs in Rust
<!-- Describe what will be discused in this presentation:
The goal of the presentation will be to show how to write CLIs and rest API wrappers in application with an emphasis on exploring rust features and ecosystem
-->
![width:460px height:307px](./images/rustacean-flat-happy.png)


---

# Case study
<!--- Note: Indicate that we are first discussing the library and than the CLI wrapper -->
<div style="width: 100%; overflow: hidden;">
     <div style="width: 600px; float: left;"> 
        <div> <b> rl_ticloud_sdk </b></div>
        <img src="images/cargo.png"/>
     </div>
     <div style="margin-left: 620px">
        <div> <b> rl_ticloud_cli </b></div>
        <img src="images/cli.jpeg"/>
     </div>
</div>


---

<!-- Scoped style -->
<style scoped>
li {
   font-size: 34px
}
</style>

<div style="position: relative; top: -120px; width: 100%; overflow: hidden;">
      <h2 style="margin-top: 100px; float: top"> rl_ticloud_sdk</h2>
     <div style="width: 600px; float: left; margin-top: 0px; margin-left: 40px">
         <ul>
            <li> Easy to use </li>
            <li> Hard to misuse </li>
            <li> Async/Sync support </li>
            <li> Client agnostic </li>
            <li> Documented </li>
            <li> Tested </li>
          </ul>
     </div>
      <div style="margin-left: 620px">
        <img style="width: 400px; height: 400px" src="images/cargo.png"/>
     </div>
</div>

---
<div style="background-image: linear-gradient(rgba(255,255,255,0.5), rgba(255,255,255,0.5)), url('./images/surreal-landscape-with-split-road-signpost-arrows-showing-two-different-courses-left-right-direction-choose-road-splits-distinct-direction-ways-difficult-decision-choice-concept_35691-34920.avif'); width: 100%, height: 100%;
position: absolute;
left: 0px;
right: 0px;
top: 0px;
height: 100%;
background-repeat: no-repeat;
background-size: cover;
">
<h2> Which way to go?</h2>
<div style="width: 100%; overflow: hidden;">
     <div style="width: 600px; float: left;"> 
        <div> <b> GENERATING CODE </b></div>
        <img style="width:380px; height:400px; mix-blend-mode: multiply" src="images/sloth.jpg">
        </img>
     </div>
     <div style="margin-left: 620px">
        <div> <b> WRITING CODE </b></div>
        <img style="width:400px; height:400px; mix-blend-mode: multiply" src="images/monkey-typing-on-computer-funny-600nw-573117796.webp">
        </img>
      </div>
</div>
</div>

<!-- Create fun path graphic, put text in two doors or something like that, or two paths -->

---
<style scoped>
li {
  font-size: 36px;
}

</style>

<!--- 
PROS, CONS, tooling
-->
<div style="
position: absolute;
left: 0px;
right: 0px;
top: 0px;
height: 100%;
">
   <h2> Generating code </h2>
   <div style="width: 100%; overflow: hidden;">
     <div style="width: 600px; float: left;"> 
        <div> <h3> PROS </h3></div>
        <ul style="margin-top: 30px; list-style-type: square; margin-left: 120px">
         <li> Minimizes/removes developer error</li>
         <li> Faster development</li>
         <li> Easier development</li>
        </ul>
     </div>
     <div style="margin-left: 620px">
        <div> <h3> CONS </h3></div>
        <ul style="margin-top: 30px; list-style-type: square; margin-left: 120px">
         <li> Not completely customizable/flexible <!-- we can only do what the API generation  tool provides or make manual edits to the generated code which is not optimal
         -->
         </li>
         <li> Requires correct and extensive API definitions  to exist</li>
         <li> Requires tooling<!--  (what i mean here is that everyone who writes manual library APIs will do something different, its better for something to be standardized and familiar for users) --> </li>
        </ul>
      </div>
</div>



</div>

---
<style scoped>
th,td {
  font-size: 32px;
  border-left: 1px solid black
}
table {
   border: none;
   border: 1px solid black
}
</style>

<div style="
position: absolute;
left: 0px;
right: 0px;
top: 0px;
height: 100%;
">
<h2> API client generators </h2>
<div style="margin-top: 100px; padding-left: 20px; padding-right: 20px">
   <table>
   <tr>
      <th>Generator name</th>
      <th>Repository link</th>
      <th>Stable</th>
   </tr>
   <tr>
      <td>Libninja</td>
      <td>https://github.com/kurtbuilds/libninja</td>
      <td>No</td>
   </tr>
   <tr>
      <td>Paperclip</td>
      <td>https://github.com/paperclip-rs/paperclip</td>
      <td>No</td>
   </tr>
   <tr>
      <td>Smithy</td>
      <td>https://github.com/smithy-lang/smithy-rs</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Progenitor</td>
      <td>https://github.com/oxidecomputer/progenitor</td>
      <td>No</td>
   </tr>
   <tr>
      <td>swagger-codegen</td>
      <td>https://github.com/swagger-api/swagger-codegen</td>
      <td>Yes</td>
   </tr>
   </table>
   </div>
</div>

---
### Smithy
- Smithy is an interface definition language and set of tools that allows developers to build clients and servers in multiple languages.
- Developed by AWS
- Official AWS SDK is generated by smithy https://awslabs.github.io/aws-sdk-rust/

---
<style scoped>
li {
  font-size: 36px;
}
</style>

<div style="
position: absolute;
left: 0px;
right: 0px;
top: 0px;
height: 100%;
">
   <h2> Writing code </h2>
   <div style="width: 100%; overflow: hidden;">
     <div style="width: 600px; float: left;"> 
        <div> <h3> PROS </h3></div>
        <ul style="margin-top: 30px; list-style-type: square; margin-left: 120px">
         <li> Customizable/optimizable implemention for each distinct API </li>
         <li> Easy to modify/extend </li>
         <li> Requires no previous correct/extensive API documentation</li>
        </ul>
     </div>
     <div style="margin-left: 620px">
        <div> <h3> CONS </h3></div>
        <ul style="margin-top: 30px; list-style-type: square; margin-left: 120px">
         <li> Takes much more development time to write </li>
         <li> Repeating ourselves, we mostly write the same code for each API </li>
         <li> Increased potential for developer errors <!--  (what i mean here is that everyone who writes manual library APIs will do something different, its better for something to be stanadides and familiar for users) --> </li>
        </ul>
      </div>
</div>

</div>

---

## The result?
<!-- Show example of usage -->
```rust
let client = ClientBuilder::new()
   .username("username")
   .password("password")
   .base_url("https://data.reversinglabs.com")
   .with_default_blocking_http_client()?;

let response = client
   .ip_threat_intelligence()
   .report_query("127.0.0.1".parse())
   .extended(true)
   .send_blocking()?;
```

---
<!-- Scoped style -->
<!--- Note: Indicate that we are first discussing the library and than the CLI wrapper -->
## Building blocks
<div style="width: 100%; overflow: hidden;">
     <div style="width: 700px; float: left; margin-left: 40px"> 
        <ul>
            <li>Client
            <ul>
                <li>SyncHttpClient</li>
                <li>AsyncHttpClient</li>
            </ul>
            </li>
            <li>API</li>
            <li>Request
            <ul>
                <li>SendableRequest</li>
            </ul>
            </li>
            <li>Response</li>
            <li>Error</li>
        </ul>
     </div>
     <div style="margin-left: 620px">
        <img src="images/builder_crab-removebg-preview.png" style="width: 340px; height: 340px"/>
     </div>
</div>

---

## Client
```rust
/// Client for calling ReversingLabs TitaniumCloud APIs
#[derive(Clone, Debug)]
pub struct Client<C>(C);

impl<C: Clone> Client<C> {
    /// Returns an instance of MalwarePresenceApi (TCA-0101)
    ///
    /// This service provides information
    /// about the malware status of requested samples.
    /// The status can be malicious, known, or unknown.
    pub fn malware_presence(&self) -> MalwarePresenceApi<C> {
        MalwarePresenceApi::new(self.0.clone())
    }
    // ...
    // ...

}
```

---
## Client builder
```
/// Builder for [crate::client::Client]
#[derive(Debug, Default)]
pub struct ClientBuilder {
    username: Option<String>,
    password: Option<Secret<String>>,
    base_url: Option<String>,
    proxy: Option<String>,
    allow_http: bool,
    timeout: Option<u32>,
}
```

---
### Building a client

```
    /// Returns a [rl_ticloud_sdk::client::Client] instance
    pub fn client(&self) -> Result<Client<impl SyncHttpClient>, BuildError> {
        let mut client_builder = ClientBuilder::new()
            .username(self.username.clone())
            .password(self.password.clone())
            .base_url(self.api_url.clone());

        if let Some(proxy) = self.proxy.clone() {
            client_builder = client_builder.proxy(proxy);
        }

        if let Some(timeout) = self.timeout {
            client_builder = client_builder.timeout(timeout);
        }

        let client = client_builder.with_default_blocking_http_client()?;

        Ok(client)
    }
```
---
## AsyncHttpClient
```
#[async_trait]
pub trait AsyncHttpClient: Clone + Send + Sync {
    // TODO: Add generic http_request method supports both streams and fixed size bodies
    // I have not yet decided how to implement this

    fn with_config(
        config: Config,
    ) -> Result<Self, Box<dyn std::error::Error + Send + Sync + 'static>>
    where
        Self: Sized;

    async fn get_json<T: DeserializeOwned>(
        &self,
        resource_path: &str,
        query_params: Option<&[(&str, &str)]>,
    ) -> Result<T, HttpClientError>;

    async fn post_json<T: DeserializeOwned, B: Serialize + ?Sized + Sync>(
        &self,
        resource_path: &str,
        query_params: Option<&[(&str, &str)]>,
        body: &B,
    ) -> Result<T, HttpClientError>;

    // TODO: Its currently a string, use serde_xml instead
    async fn post_xml(
        &self,
        resource_path: &str,
        query_params: Option<&[(&str, &str)]>,
        body: String,
    ) -> Result<(), HttpClientError>;

    async fn get_byte_stream(
        &self,
        resource_path: &str,
        query: Option<&[(&str, &str)]>,
    ) -> Result<BoxStream<Result<Bytes, HttpClientError>>, HttpClientError>;

    async fn post_byte_stream<S>(
        &self,
        resource_path: &str,
        query: Option<&[(&str, &str)]>,
        stream: S,
    ) -> Result<(), HttpClientError>
    where
        S: TryStream + Send + Sync + 'static,
        S::Error: Into<Box<dyn std::error::Error + Send + Sync>>,
        Bytes: From<S::Ok>;
}
```
---
## SyncHttpClient
```
pub trait SyncHttpClient: Clone {
    fn with_config(
        config: Config,
    ) -> Result<Self, Box<dyn std::error::Error + Send + Sync + 'static>>
    where
        Self: Sized;

    fn blocking_get_json<T: DeserializeOwned>(
        &self,
        resource_path: &str,
        query_params: Option<&[(&str, &str)]>,
    ) -> Result<T, HttpClientError>;

    fn blocking_post_json<T: DeserializeOwned, B: Serialize + ?Sized>(
        &self,
        resource_path: &str,
        query_params: Option<&[(&str, &str)]>,
        body: &B,
    ) -> Result<T, HttpClientError>;

    fn get_bytes(
        &self,
        resource_path: &str,
        query_params: Option<&[(&str, &str)]>,
    ) -> Result<impl Read, HttpClientError>;

    fn post_bytes<R>(
        &self,
        resource_path: &str,
        query: Option<&[(&str, &str)]>,
        reader: R,
    ) -> Result<(), HttpClientError>
    where
        R: Read + Send + 'static;

    fn blocking_post_xml(
        &self,
        resource_path: &str,
        query_params: Option<&[(&str, &str)]>,
        body: String,
    ) -> Result<(), HttpClientError>;
}
```
---
## Reqwest
https://github.com/seanmonstar/reqwest

```
~/Projects/Private/rust_rl_ticloud_client/rl_ticloud_sdk/src/client/impls$ tree
.
├── asynchronous
│   ├── mod.rs
│   └── reqwest.rs
├── mod.rs
└── synchronous
    ├── mod.rs
    └── reqwest.rs
```

---
## API
```
#[derive(Clone)]
pub struct XrefApi<C> {
    client: C,
}

impl<C: Clone> XrefApi<C> {
    pub fn single_query(&self, hash: Hash) -> SendableRequest<C, XrefRequest> {
        SendableRequest::new(self.client.clone(), XrefRequest::new(hash))
    }

    pub fn bulk_query(&self, hashes: Vec<Hash>) -> SendableRequest<C, XrefBulkRequest> {
        SendableRequest::new(self.client.clone(), XrefBulkRequest::new(hashes))
    }

    pub fn new(client: C) -> Self {
        XrefApi { client }
    }
}
```
  
---
<!-- What to write here, talk about required arguments -->
## Request
```
/// Represents an instance of a request to the XREF (TCA-0103) API bulk query endpoint
#[derive(Serialize, Deserialize, Debug, PartialEq, Clone, Validate)]
#[non_exhaustive]
pub struct XrefBulkRequest {
    /// Queried hash
    #[validate(length(min = 0, max = 100))]
    #[validate(custom(function = "crate::validators::validate_hashes"))]
    pub hashes: Vec<Hash>,
    /// If true the response will contain historic XREF/multi-AV scan records
    pub history: bool,
}
```
---
### non_exhaustive?
The non_exhaustive attribute indicates that a type or variant may have more fields or variants added in the future.
It prevents us from instantiating a struct with struct expressions.

```rust
/// This is not allowed with non_exhaustive
let xref_bulk_request = XrefBulkRequest {
    hashes: vec![],
    history: false
};
```

---
### Constructors

```rust
impl XrefBulkRequest {
    /// Returns an xref bulk request for the provided hashes
    pub fn new(hashes: Vec<Hash>) -> Self {
        Self {
            hashes,
            history: false,
        }
    }
    // ... 
    // ...
}
```
---
### Consuming setters to enable a fluent API

```rust
// PRESENTATION_NOTE: I will explain why I'm using this macro later
generate_sendable_request_impl! {
    impl XrefBulkRequest {
        /// history defines whether the response should contain
        /// multi-AV records from history (when true) or latest
        /// one only
        pub fn with_history(mut self, history: bool) -> Self {
            self.history = history;
            self
        }
    }
}
```
---
### Breaking the fluent API chain
In adddition to constructing the request in a single method chain, due to the setters consuming/moving self we can stop and continue the chain at any point
```rust
let mut request = RhaFunctionalSimilarityRequest::new(sha1, rha1_type)
    .with_extended_response(extended);

if let Some(limit) = calculate_limit() {
    request = request.with_limit(limit);
}

let response = request.send(&client);

```
---
## Request trait
```
/// Represents an request which can be sent via
/// [crate::client::SyncHttpClient] or [crate::client::AsyncHttpClient]
#[async_trait]
pub trait Request {
    /// Response type of request
    type Response;
    /// Error response type of request
    type Error;

    /// Sends the request synchronously
    fn send_blocking<C: SyncHttpClient>(&self, client: &C) -> Result<Self::Response, Self::Error>;

    /// Sends the request asynchronously
    async fn send<C: AsyncHttpClient>(&self, client: &C) -> Result<Self::Response, Self::Error>;
}
```

---
### Implementing the Request trait

```
#[async_trait]
impl Request for XrefBulkRequest {
    type Response = XrefBulkResponse;
    type Error = XrefApiError;

    async fn send<C: AsyncHttpClient>(
        &self,
        client: &C,
    ) -> Result<Self::Response, Self::Error> {
        self.validate()?;

        let response = client
            .post_json::<RlWrapper<XrefBulkResponse>, _>(
                self.resource_path(),
                Some(&[("format", "json"), ("history", &self.history.to_string())]),
                &self.body(),
            )
            .await?
            .rl;

        Ok(response)
    }

    fn send_blocking<C: SyncHttpClient>(
        &self,
        client: &C,
    ) -> Result<Self::Response, Self::Error> {
        self.validate()?;

        let response = client
            .blocking_post_json::<RlWrapper<XrefBulkResponse>, _>(
                self.resource_path(),
                Some(&[("format", "json"), ("history", &self.history.to_string())]),
                &self.body(),
            )?
            .rl;

        Ok(response)
    }
}
```

---

## SendableRequest

```rust
/// Transparent wrapper type around an request
/// that allows it to be used in a fluent API
#[derive(Clone)]
pub struct SendableRequest<C, R> {
    /// Client used for sending the request
    client: C,
    /// Inner request
    request: R,
}

```

---

```rust
impl<C: AsyncHttpClient, R: Request> SendableRequest<C, R> {
    /// Sends the inner request asynchronously
    pub async fn send(&self) -> Result<R::Response, R::Error> {
        self.request.send(&self.client).await
    }
}

impl<C: SyncHttpClient, R: Request> SendableRequest<C, R> {
    /// Sends the inner request synchronously
    pub fn send_blocking(&self) -> Result<R::Response, R::Error> {
        self.request.send_blocking(&self.client)
    }
}
```
---
### Declarative macros

```
/// Generate an implementation for the specified request and for [crate::request::SendableRequest]
macro_rules! generate_sendable_request_impl {
    (
        impl $name:ident $(<$generic:ident>)? {
            $(
                $( #[$meta:meta] )*
                pub fn $method:ident (mut $self:ident $(, $arg:ident : $arg_ty:ty)*) -> $ret_ty:ty {
                    $($body:tt)*
                }
            )*
        }
    ) => {
        // The original impl block for the original struct
        impl $name $(<$generic>)? {
            $(
                $( #[$meta] )*
                pub fn $method(mut $self $(, $arg : $arg_ty)*) -> $ret_ty {
                    $($body)*
                }
            )*
        }

        // Implement methods on the new struct that delegate to inner `request`
        impl <C> $crate::request::SendableRequest<C, $name>{

            $(
                $( #[$meta] )*
                pub fn $method(mut self $(, $arg : $arg_ty)*) -> Self {
                    // Delegate the call to `self.request`
                    let request = self.request.$method($($arg),*);
                    self.request = request;
                    self // Return `self` for method chaining
                }
            )*
        }
    };
}

```
---
### cargo expand
https://github.com/dtolnay/cargo-expand

Utility for viewing code after macro expansion

---
#### Before
```
generate_sendable_request_impl! {
    impl XrefBulkRequest {
        /// history defines whether the response should contain
        /// multi-AV records from history (when true) or latest
        /// one only
        pub fn with_history(mut self, history: bool) -> Self {
            self.history = history;
            self
        }

    }
}
```

---
#### After

```
impl XrefBulkRequest {
    /// history defines whether the response should contain
    /// multi-AV records from history (when true) or latest
    /// one only
    pub fn with_history(mut self, history: bool) -> Self {
        self.history = history;
        self
    }
}
impl<C> crate::request::SendableRequest<C, XrefBulkRequest> {
    /// history defines whether the response should contain
    /// multi-AV records from history (when true) or latest
    /// one only
    pub fn with_history(mut self, history: bool) -> Self {
        let request = self.request.with_history(history);
        self.request = request;
        self
    }
}
```
---
## Request validation

---
### Validate crate
https://github.com/Keats/validator/tree/master/validator

Provides common validators and a derive macro to simplify struct validation


---

```
/// Represents an instance of a request to the XREF (TCA-0103) API bulk query endpoint
#[derive(Serialize, Deserialize, Debug, PartialEq, Clone, Validate)]
#[non_exhaustive]
pub struct XrefBulkRequest {
    /// Queried hashes
    #[validate(length(min = 0, max = 100))]
    #[validate(custom(function = "crate::validators::validate_hashes"))]
    pub hashes: Vec<Hash>,
    /// If true the response will contain historic XREF/multi-AV scan records
    pub history: bool,
}
```
---
### Custom validators
```
use validator::ValidationError;

use crate::models::hash::Hash;

/// Validates that a list of hashes is homogenous
/// ie. that all hashes are of the same type
pub(crate) fn validate_hashes(hashes: &[Hash]) -> Result<(), ValidationError> {
    if hashes.len() == 0 {
        return Ok(());
    }

    let hash_type = hashes[0].hash_type();

    if hashes.iter().any(|hash| hash.hash_type() != hash_type) {
        Err(ValidationError::new("Mixed hash types"))
    } else {
        Ok(())
    }
}
```
---

## Responses
```
/// Represents a response from XREF (Historic Multi-AV Scan Records, TCA-0103) API single query endpoint
#[derive(Serialize, Deserialize, Debug, Clone, PartialEq)]
pub struct XrefResponse {
    /// Sha1 hash of sample
    pub sha1: String,
    /// Sha256 hash of sample
    pub sha256: String,
    /// Sha384 hash of sample
    pub sha384: String,
    /// Sha512 hash of sample
    pub sha512: String,
    /// Ripemd160 hash of sample
    pub ripemd160: String,
    ...
    ...
}
```
---
## Serialization with serde
#### https://serde.rs/

Serde is a framework for serializing and deserializing Rust data structures efficiently and generically.

---
### Serde derive macro
Serde provides a derive macro that automatically generates generate implementations of the Serialize and Deserialize traits for data structures 
```
#[derive(Serialize, Deserialize, Debug, Clone, PartialEq)]
pub struct XrefBulkResponse {
    #[serde(default)]
    pub samples: Vec<XrefResponse>,
    // ...
    // ...
}
```
---
### Examples
```
let response = request.send_blocking()?;

// PRESENTATION_NOTE: This can be any serializer
// for any supported binary or text serialization protocol
println!("{}", serde_json::to_string_pretty(&response)?);
println!("{}", serde_xml_rs::to_string(&response)?);
println!("{}", serde_yaml::to_string(&response)?);
```

---
## Errors
Errors are values!!!!

---
### Result type
Fallible functions should return the Result enum
```
enum Result<T, E> {
   Ok(T),
   Err(E),
}
```
---
### Handling errors with match
```
fn map_response(
    response: Result<RlWrapper<SampleWrapper<GoodwareDataResponse>>, HttpClientError>,
) -> Result<Option<GoodwareDataResponse>, GoodwareDataApiError> {
    match response {
        Ok(response) => Ok(Some(response.rl.sample)),
        Err(err) => match err {
            HttpClientError::ResponseError { status_code, .. } => {
                if status_code == 404 {
                    Ok(None)
                } else {
                    Err(err.into())
                }
            }
            _ => Err(err.into()),
        },
    }
}
```
---
### Propagating errors
We can propagate errors with the question mark operators
```
fn send_blocking<C: SyncHttpClient>(
    &self,
    client: &C,
) -> Result<Self::Response, Self::Error> {
    // Propagate validation errors to the client 
    self.validate()?;

    // ...
    // ...

    Ok(response)
}
```

---
### Error trait
```
pub trait Error: Debug + Display {
    // Provided methods
    fn source(&self) -> Option<&(dyn Error + 'static)> { ... }
    // deprecated, replaced by Display
    fn description(&self) -> &str { ... }
    // deprecated, replaced by source
    fn cause(&self) -> Option<&dyn Error> { ... }
    // experimental
    fn provide<'a>(&'a self, request: &mut Request<'a>) { ... }
}
```
---
### Thiserror
https://github.com/dtolnay/thiserror

This library provides a convenient derive macro for the standard library's std::error::Error trait.

---
### HttpClientError
```
/// Represents an error that occured when sending a request with 
/// [crate::client::AsyncHttpClient] or  [crate::client::SyncHttpClient]
#[derive(Error, Debug)]
pub enum HttpClientError {
    /// An response error occcured
    #[error("Http response error (status_code={status_code}, body={body})")]
    ResponseError { status_code: u16, body: String },
    /// Error while connecting to server
    #[error(transparent)]
    ConnectError(Box<dyn std::error::Error + Send + Sync + 'static>),
    /// Timeout error
    #[error(transparent)]
    TimeoutError(Box<dyn std::error::Error + Send + Sync + 'static>),
    /// An unexpected error occured when making the request
    #[error(transparent)]
    UnexpectedError(#[from] Box<dyn std::error::Error + Send + Sync + 'static>),
}
```

---
### API errors
```
/// Represents an error that occured when sending
/// a request to an TitaniumCloud API
#[derive(Error, Debug)]
pub enum TiCloudApiError {
    #[error(transparent)]
    ConnectError(Box<dyn std::error::Error + Send + Sync + 'static>),
    #[error(transparent)]
    TimeoutError(Box<dyn std::error::Error + Send + Sync + 'static>),
    #[error("response error (status_code = {status_code}, message = `{message}`)")]
    ResponseError { status_code: u16, message: String },
    #[error(transparent)]
    ValidationError(#[from] ValidationErrors),
    #[error(transparent)]
    UnexpectedError(Box<dyn std::error::Error + Send + Sync + 'static>),
}

impl From<HttpClientError> for TiCloudApiError {
    fn from(error: HttpClientError) -> Self {
        match error {
            HttpClientError::ResponseError { status_code, body } => Self::ResponseError {
                status_code,
                message: body,
            },
            HttpClientError::UnexpectedError(err) => Self::UnexpectedError(err),
            HttpClientError::ConnectError(err) => Self::ConnectError(err),
            HttpClientError::TimeoutError(err) => Self::TimeoutError(err),
        }
    }
}
```

---
```
/// Represents an error that occured when sending
/// a request to the Sample Exchange API
#[derive(Error, Debug)]
pub enum SampleExchangeApiError {
    #[error("response error (status_code = {status_code}, message = `{message}`)")]
    ResponseError { status_code: u16, message: String },
    #[error(transparent)]
    IoError(#[from] std::io::Error),
    #[error(transparent)]
    ValidationError(#[from] ValidationErrors),
    #[error(transparent)]
    ConnectError(Box<dyn std::error::Error + Send + Sync + 'static>),
    #[error(transparent)]
    TimeoutError(Box<dyn std::error::Error + Send + Sync + 'static>),
    #[error(transparent)]
    UnexpectedError(Box<dyn std::error::Error + Send + Sync + 'static>),
}

impl From<HttpClientError> for SampleExchangeApiError {
    fn from(error: HttpClientError) -> Self {
        match error {
            HttpClientError::ResponseError { status_code, body } => Self::ResponseError {
                status_code,
                message: body,
            },
            HttpClientError::UnexpectedError(err) => Self::UnexpectedError(err),
            HttpClientError::ConnectError(err) => Self::ConnectError(err),
            HttpClientError::TimeoutError(err) => Self::ConnectError(err),
        }
    }
}
```
---
## Documentation

---

![bg contain](./images/crate_docs.png)

---
## Testing
- Unit tests
    - Written alongside impl files
- Doc tests
    - Written inside doc comments
    - Great to have for SDKs
- Integration tests
    - stored in tests/ directory
    - external to our crate

---
### Unit tests
```
pub fn add(a: i32, b: i32) -> i32 {
    a + b
}

// This is a really bad adding function, its purpose is to fail in this
// example.
#[allow(dead_code)]
fn bad_add(a: i32, b: i32) -> i32 {
    a - b
}

#[cfg(test)]
mod tests {
    // Note this useful idiom: importing names from outer (for mod tests) scope.
    use super::*;

    #[test]
    fn test_add() {
        assert_eq!(add(1, 2), 3);
    }

    #[test]
    fn test_bad_add() {
        // This assert would fire and test will fail.
        // Please note, that private functions can be tested too!
        assert_eq!(bad_add(1, 2), 3);
    }
}
```

---
### Doc tests
```
/// ```
/// use std::io;
/// # fn main() -> io::Result<()> {
/// let mut input = String::new();
/// io::stdin().read_line(&mut input)?;
/// # Ok(())
/// # }
/// ``
```

---
### Integrations tests
tests/integration_test.rs:

```
#[test]
fn test_add() {
    assert_eq!(adder::add(3, 2), 5);
}
```

---

## Feature flags
```
[features]
default = [
    "reqwest",
    "automation",
    "network_threat_intelligence",
    "certificate_threat_intelligence",
    "dynamic_analysis",
    "file_threat_intelligence",
    "malware_hunting",
]
# Enables automation APIs
automation = []
# Enables network threat intelligence APIs
network_threat_intelligence = []
# Enables certificate threat intelligence APIs
certificate_threat_intelligence = []
# Enables dynamic analysis APIs
dynamic_analysis = []
# Enables file threat intelligence APIs
file_threat_intelligence = []
# Enables malware hunting APIs
malware_hunting = []
# Enable reqwest client
reqwest = ["dep:reqwest"]
```

---

<!-- Scoped style -->
## rl_ticloud_cli

---

```
rl-ticloud-cli --help
For more info visit https://docs.reversinglabs.com/SpectraIntelligence/

Usage: rl-ticloud-cli [OPTIONS] <COMMAND>

Commands:
  file-threat-intelligence         [aliases: fti]
  certificate-threat-intelligence  [aliases: cti]
  network-threat-intelligence      [aliases: nti]
  automation                       [aliases: aut]
  malware-hunting                  [aliases: mh]
  dynamic-analysis                 [aliases: da]
  help                             Print this message or the help of the given subcommand(s)

Options:
      --config <CONFIG>
          Config file path

      --api-url <API_URL>
          Url of ReversingLabs API

  -u, --username <USERNAME>
          TiCloud username

  -p, --password <PASSWORD>
          TiCloud password

      --proxy <PROXY>
          Proxy url

      --timeout <TIMEOUT>
          Request timeout

  -h, --help
          Print help (see a summary with '-h')

  -V, --version
          Print version

```

---
```
rl-ticloud-cli --config configs/testing.yaml fti av a45ab18fb7a06dd5ecb44bf6c221a951f974059f
{
  "samples": [
    {
      "sha1": "a45ab18fb7a06dd5ecb44bf6c221a951f974059f",
      "sha256": "de054fc4d774d40e24b81cee22c04c7840dae3f82c76e4b07433745fddbc531d",
      "sha384": "9c5309327d6297427d93e0454c16bb67c124685b6c8107ce75114aba9c02ec7b0c5d7762a8b92b59e7d235ffc340679b",
      "sha512": "dc38cdd9d1e9dd81a2470569ab1683b61d5c7d27cd85d9c7032a2c8ac1294165b702f23f4d9c7b141ccf9253cf0a3537aadbc210328592e767a8d2cdc1401fa4",
      "ripemd160": "6f346db7f2f542ca8585d799986265603ea6a0b6",
      "md5": "2effabbb768ab968fd14b24f2984986d",
      "first_seen_on": "2020-05-06T22:05:31",
      "last_seen_on": "2023-05-06T01:15:00",
      "single_scan": false,
      "sample_type": "PDF document, version 1.4",
      "sample_size": 40377,
      "xref": [
        {

```
---
```
cat hashes.txt | head -n 10 | rl-ticloud-cli --config configs/testing.yaml fti av | jq '.samples[].sha1'
"668b0df94c6d12ae86711ce24ce79dbe0ee2d463"
"66776c50bcc79bbcecdbe99960e6ee39c8a31181"
"10411f07640edcaa6104f078af09e2543aa0ca07"
"e005c58331eb7db04782fdf9089111979ce1406f"
"28f4efd9fbb9bb8e14d2946da97eff28fed682c9"
"2027a053de21bd5c783c3f823ed1d36966780ed4"
"69a8ba560ef1aad2b1bc7614c1de8ed22e19deb6"
"7d21c1fb16f819c7a15e7a3343efb65f7ad76d85"
"34f917aaba5684fbe56d3c57d48ef2a1aa7cf06d"
"2bf0e077ab41c6272185c27cddae6e09a40db3cc"
```

---
## main()
```
use clap::Parser;
use rl_ticloud_cli::{args::CliArgs, config::Config};

fn main() -> Result<(), anyhow::Error> {
    // Parse the config
    let args = CliArgs::parse();

    let cmd = args.command;
    let global_args = args.global_args;

    // Builds the config merged with the 
    // global command arguments
    let config = Config::build(global_args)?;
    
    // Executes the command with the config
    cmd.execute(config)
}
```
---
## Arguments
https://github.com/clap-rs/clap

```
/// Cli arguments
#[derive(Parser)]
#[command(
    author,
    version,
    about,
    long_about = "For more info visit https://docs.reversinglabs.com/SpectraIntelligence/"
)]
#[command(propagate_version = true)]
pub struct CliArgs {
    /// Global arguments shared between subcommands
    #[clap(flatten)]
    pub global_args: GlobalArgs,
    /// Subcommand to run
    #[command(subcommand)]
    pub command: Commands,
}
```

---
## Configuration
https://github.com/rust-cli/config-rs
```
/// Cli configuration
#[derive(serde::Deserialize, Clone, Debug)]
pub struct Config {
    pub api_url: String,
    pub username: String,
    pub password: String,
    pub proxy: Option<String>,
    pub timeout: Option<u64>,
}
```
---
```
    pub fn build(global_args: GlobalArgs) -> Result<Self, config::ConfigError> {
        let mut config_builder = config::Config::builder();

        let default_config_path = Path::new(DEFAULT_CONFIG_LOCATION);
        if default_config_path.exists() {
            config_builder = config_builder.add_source(config::File::from(default_config_path));
        }

        if let Some(config_file) = global_args.config {
            config_builder = config_builder.add_source(config::File::from(Path::new(&config_file)));
        }

        let config = config_builder.add_source(
            config::Environment::with_prefix("RL_TICLOUD_CLI")
                .prefix_separator("_")
                .separator("__"),
            )
            .set_override_option("url", global_args.api_url)?
            .set_override_option("username", global_args.username)?
            .set_override_option("password", global_args.password)?
            .set_override_option("proxy", global_args.proxy)?
            .set_override_option("timeout", global_args.timeout)?
            .build()?;

        config.try_deserialize::<Config>()
    }
```
---
## Commands
```
#[derive(Subcommand)]
pub enum Commands {
    #[command(visible_alias = "fti")]
    FileThreatIntelligence(FileThreatIntelligenceCommand),
    #[command(visible_alias = "cti")]
    CertificateThreatIntelligence(CertificateThreatIntelligenceCommand),
    #[command(visible_alias = "nti")]
    NetworkThreatIntelligence(NetworkThreatIntelligenceCommand),
    #[command(visible_alias = "aut")]
    Automation(AutomationCommand),
    #[command(visible_alias = "mh")]
    MalwareHunting(MalwareHuntingCommand),
    #[command(visible_alias = "da")]
    DynamicAnalysis(DynamicAnalysisCommand),
}
```

---
```
impl Commands {
    pub fn execute(self, config: Config) -> Result<(), anyhow::Error> {
        use Commands::*;
        match self {
            FileThreatIntelligence(cmd) => cmd.execute(config),
            CertificateThreatIntelligence(cmd) => cmd.execute(config),
            NetworkThreatIntelligence(cmd) => cmd.execute(config),
            Automation(cmd) => cmd.execute(config),
            MalwareHunting(cmd) => cmd.execute(config),
            DynamicAnalysis(cmd) => cmd.execute(config),
        }
    }
}
```
---
```
#[derive(Debug, Args)]
pub struct CertificateThreatIntelligenceCommand {
    #[command(subcommand)]
    command: CertificateThreatIntelligenceCommands,
}

impl CertificateThreatIntelligenceCommand {
    pub fn execute(self, config: Config) -> Result<(), anyhow::Error> {
        match self.command {
            CertificateThreatIntelligenceCommands::CertificateIndex(cmd) => cmd.execute(config),
            CertificateThreatIntelligenceCommands::CertificateAnalytics(cmd) => cmd.execute(config),
            CertificateThreatIntelligenceCommands::CertificateThumbprintSearch(cmd) => {
                cmd.execute(config)
            }
        }
    }
}

#[derive(Debug, Subcommand)]
pub enum CertificateThreatIntelligenceCommands {
    CertificateIndex(CertificateIndexCommand),
    CertificateAnalytics(CertificateAnalyticsCommand),
    CertificateThumbprintSearch(CertificateThumprintSearchCommand),
}
```
---
```
#[derive(Debug, Args)]
pub struct CertificateIndexCommand {
    hash: String,
    #[arg(long)]
    limit: Option<u32>,
    #[arg(long, default_value_t = false)]
    extended: bool,
    #[arg(long)]
    classification: Option<ClassificationArg>,
    #[arg(long)]
    next_page: Option<String>,
}

impl CertificateIndexCommand {
    pub fn execute(self, config: Config) -> Result<(), anyhow::Error> {
        let client = config.client()?;

        let mut request = client
            .certificate_index()
            .query(Hash::from_str(&self.hash)?)
            .with_extended_response(self.extended)
            .with_classification(self.classification.map(Into::into));

        if let Some(limit) = self.limit {
            request = request.with_limit(limit);
        }

        if let Some(next_page) = self.next_page {
            request = request.with_next_page(Some(Sha1::from_str(&next_page)?));
        }

        let response = request.send_blocking()?;

        print_response(response)?;

        Ok(())
    }
}

```
---
## Autocompletions
https://github.com/clap-rs/clap/tree/master/clap_complete
```
use clap::CommandFactory;
use clap_complete::{generate, shells::Bash};
use std::{fs::File, io, path::PathBuf};

fn main() {
    let mut command = rl_ticloud_cli::args::CliArgs::command();
    let autocompletions_path =
        PathBuf::from(env!("CARGO_MANIFEST_DIR")).join("autocompletions").join("rl-ticloud-cli.bash");

    let mut file =
        File::create(autocompletions_path).expect("Failed to create autocompletion file");

    generate(Bash, &mut command, "rl-ticloud-cli", &mut file);
}
```
---

## Testing
Fixture-based test framework for rust
https://github.com/la10736/rstest
```
use assert_cmd::assert::OutputAssertExt;
use rl_ticloud_sdk::api::automation::sample_exchange::responses::SampleDownloadStatusResponse;
use rstest::rstest;

use crate::helpers::execute_with_serialization;

#[rstest]
#[case(&["automation", "file-download-status", "f1927e7f90416bf39fc7991bbc57e1b3"])]
#[case(&["automation", "file-download-status", "0cf25597343240f88358c694d7ae7e0a", "a9fbb5e28c903900b2eccfc8cb632388"])]

pub fn sample_download_status_subcommand_works(#[case] args: &[&'static str]) {
    execute_with_serialization::<_, _, SampleDownloadStatusResponse>(args)
        .assert()
        .success();
}

```
---
### Debugging
https://mitmproxy.org/

mitmproxy is your swiss-army knife for debugging, testing, privacy measurements, and penetration testing. It can be used to intercept, inspect, modify and replay web traffic such as HTTP/1, HTTP/2, HTTP/3, WebSockets, or any other SSL/TLS-protected protocol

---
## Packaging
https://github.com/cat-in-136/cargo-generate-rpm
```
cargo run --bin generate-autocompletions --features="gen-autocomplete"

cargo build --release --bin rl-ticloud-cli

strip -s target/release/rl-ticloud-cli

cargo generate-rpm --package rl_ticloud_cli

```
---

## Conclusion
Don't write REST API wrappers by hand, it's not worth it.  
Instead focus on writing consistent APIs with correct API specifications and generate the code
![bg left](./images/pain_harold.png)