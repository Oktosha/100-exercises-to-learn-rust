The final exercise is open-ended: build an **asynchronous REST API** for the
ticket management system you've grown throughout the course.

Your API should let a client:

- **create** a ticket — `POST /tickets`
- **list** every ticket — `GET /tickets`
- **retrieve** a single ticket — `GET /tickets/{id}`
- **update** a ticket — `PATCH /tickets/{id}`

`Cargo.toml` is visible and yours to edit: add any crates you need from
[crates.io](https://crates.io). We suggest [`axum`](https://docs.rs/axum) — it's
an industry standard and is nicely supported by RustRover — together with
[`tokio`](https://docs.rs/tokio) and [`serde`](https://docs.rs/serde), but you're
free to pick a different stack.

Store the tickets in memory behind some shared state. That state is touched by
many requests at once, so it needs a lock: think about whether a
[`Mutex`](https://docs.rs/tokio/latest/tokio/sync/struct.Mutex.html) or an
[`RwLock`](https://docs.rs/tokio/latest/tokio/sync/struct.RwLock.html) is the
better fit for an API that reads far more often than it writes.

## Running it

```bash
cargo run
```

The server listens on `http://127.0.0.1:3000`. Open it in your browser — the
root path and `GET /tickets` both answer plain browser requests, so you can
watch your tickets appear as you create them.

## Testing it

There are no automated tests for this exercise — the design is yours. To drive
the API, use the ready-made requests in [`requests.http`](requests.http): open
it in RustRover and run each request with the HTTP client (click the ▶ icon in
the gutter). They create a ticket, list all tickets, fetch and patch it, and
check that a missing ticket returns `404`.

Stuck? You can peek at the reference solution at any time.
