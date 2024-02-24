# Rust Actix Web Service in Docker

Welcome to the Rust Actix Web Service repository! This project is a robust web service built with the Actix framework in Rust, and it's containerized using Docker for seamless deployment and scalability.

## Docker

While Rust creates binaries, these binaries are not portable across different operating systems. This is where Docker comes in. Docker allows us to package our application along with all its dependencies into a single image that can be run on any machine that has Docker installed, regardless of the operating system.

## Getting Started

1. Create a new Rust project:

```bash
cargo new rust_actix
```

1. Add the following dependencies to the `Cargo.toml` file:

```toml
[dependencies]
actix-web = "4"
```

3. Replace the contents of the `src/main.rs` file with your web service code. For example, the following code sets up a simple web service with two routes, one for a `GET` request and another for a `POST` request:

```rust
use actix_web::{get, post, web, App, HttpResponse, HttpServer, Responder};

#[get("/")]
async fn hello() -> impl Responder {
    HttpResponse::Ok().body("Hello world!")
}

#[post("/echo")]
async fn echo(req_body: String) -> impl Responder {
    HttpResponse::Ok().body(req_body)
}

async fn manual_hello() -> impl Responder {
    HttpResponse::Ok().body("Hey there!")
}
```

4. Add the actix web service to the `main` function:

```rust
#[actix_web::main]
async fn main() -> std::io::Result<()> {
    HttpServer::new(|| {
        App::new()
            .service(hello)
            .service(echo)
            .route("/hey", web::get().to(manual_hello))
    })
    .bind(("127.0.0.1", 8080))?
    .run()
    .await
}
```

5. Create a new file called `Dockerfile` in the root of the project directory.

6. Build the Docker image:

```bash
docker build -t yourusername/yourrepository .
```

7. Run the Docker container:

```bash
docker run -p 8080:8080 yourusername/yourrepository
```

Visit `http://127.0.0.1:8080/` in your web browser. You should see the your web service running there.

## Conclusion

With this project, we've demonstrated how to containerize a Rust Actix Web Service using Docker. This allows us to run our application on any machine with Docker installed, regardless of the operating system.

---