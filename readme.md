## Simple Book API Collection for API tests

|VARIABLE|VALUE|
|---|---|
|baseUrl|https://simple-books-api.glitch.me|
|accessToken|0bc105d04577a5f0f5d878c9a82625ec00ee7d593c8194d963c317d0b3ef5462|
---
### List of Books
GET `/books?type=non-fiction`

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
