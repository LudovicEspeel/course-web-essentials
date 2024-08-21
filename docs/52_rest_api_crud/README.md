# Build REST-API's for CRUD interactions

First we need to decide what API End Points we will be using:

* **Create** : POST `/<path>/` - the frontend will do a POST request to `/<path>/` with the data in the body (JSON). 
* **Read** : GET `/<path>/:<parameter>` - the frontend will do a GET request to `/<path>/`, if needed with a `:<parameter>`
* **Update** : PUT `/<path>/:<parameter>` - the frontend will do a PUT request to `/<path>/` with a `:<parameter>`, again with the data in the body (JSON)
* **Delete** : DELETE `/<path>/:<parameter>` - the frontend will do a DELETE request to `/<path>/` with a `:<parameter>`

Example:

```js
// Route for 'GET /products'
app.get('/products', db.getAllProducts);

// Route for 'GET /products/id'
app.get('/products/:id', db.getOneProduct);

// Route for 'POST /products
app.post('/products', db.createNewProduct);

// Route for 'PUT /products/id'
app.put('/products/:id', db.updateOneProduct);

// Route for 'DELETE /products/id'
app.delete('/products/:id', db.deleteOneProduct);
```



<!-- TODO : Uit te werken -->