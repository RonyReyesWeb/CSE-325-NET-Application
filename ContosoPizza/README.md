# W01 Assignment Notes — Build .NET Applications with C#

## 1. Web API with ASP.NET Core Controllers — Evidence

### Pizza list (existing content + additional record)

The `PizzaService` in-memory data store was seeded with an additional third
pizza (`Pepperoni`) beyond the two provided by the module (`Classic Italian`
and `Veggie`).

**GET all pizzas** — `GET {{ContosoPizza_HostAddress}}/pizza/`

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
  {
    "id": 1,
    "name": "Classic Italian",
    "isGlutenFree": false
  },
  {
    "id": 2,
    "name": "Veggie",
    "isGlutenFree": true
  },
  {
    "id": 3,
    "name": "Pepperoni",
    "isGlutenFree": false
  }
]
```

### CRUD operation evidence (request + response + status code)

**GET by id** — `GET {{ContosoPizza_HostAddress}}/pizza/3`

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "id": 3,
  "name": "Pepperoni",
  "isGlutenFree": false
}
```
Status: **200 OK**

---

**POST (create)** — `POST {{ContosoPizza_HostAddress}}/pizza/`

Request body:
```json
{
    "name": "Hawaiian",
    "isGlutenFree": false
}
```

Response:
```
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
Location: https://localhost:7056/Pizza/4

{
  "id": 4,
  "name": "Hawaiian",
  "isGlutenFree": false
}
```
Status: **201 Created**

---

**PUT (update)** — `PUT {{ContosoPizza_HostAddress}}/pizza/4`

Request body:
```json
{
    "id": 4,
    "name": "Hawaiian Deluxe",
    "isGlutenFree": false
}
```

Response:
```
HTTP/1.1 204 No Content
```
Status: **204 No Content**

---

**DELETE** — `DELETE {{ContosoPizza_HostAddress}}/pizza/4`

Response:
```
HTTP/1.1 204 No Content
```
Status: **204 No Content**

---
