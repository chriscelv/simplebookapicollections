# Simple Book API Collection for API tests

|VARIABLE|VALUE|
|---|---|
|baseUrl|https://simple-books-api.glitch.me|
|accessToken|<YOUR TOKEN>|
---
## API Status
GET `/status/`
### Tests
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

const response = pm.response.json();

console.log(response.status);
console.log(response['status']);

pm.test("Status should be OK", () => {
    pm.expect(response.status).to.eql("OK");
});

postman.setNextRequest("List of books");
```
---
## List of Books
GET `/books?type=non-fiction`
### Query Params
|KEY|VALUE|
|--|--|
|type|non-fiction
|limit|5|
### Tests
```
pm.test("Status code is 200", () => {
    pm.response.to.have.status(200);
});
const response = pm.response.json();
const nonFictionBooks = response.filter((book) => book.available === true);
const book = nonFictionBooks[0];
pm.test("Book found", () => {
    pm.expect(book).to.be.an('object');
    pm.expect(book.available).to.be.true;
    pm.expect(book.type).to.eql('non-fiction');
});
pm.globals.set("bookId", book.id);

```
---
## Single Book
GET `/books/:bookId`
### Path Variables
|KEY|VALUE|
|--|--|
|bookId|1|
### Tests
```
pm.test("Status code is 200", () => {
    pm.response.to.have.status(200);
});
const response = pm.response.json();

pm.test("Is in stock", () => {
    pm.expect(response['current-stock']).to.be.above(0);
});
```
---
## Order Book
POST `/orders`
### Body
```
{
    "bookId": {{bookId}},
    "customerName": "${{$randomFullName}}"
}
```
---
## All Book Orders
GET `/orders`
### Tests
```
    pm.test("Status code is 200", () => {
    pm.response.to.have.status(200);
});
```
---
## Book Order
GET `/orders/:orderId`
### Tests
```
    pm.test("Status code is 200", () => {
    pm.response.to.have.status(200);
});
```
---

