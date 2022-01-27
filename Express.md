## hello world
```javascript
const express = require('express')
const app = express()
app.get('/', (req,res) => {
    res.send('Hello World!')
})
//when get a request of '/', send 'hello world'.
app.listen(3000, () => {
    console.log('server running at port 3000')
})
```

## routing
* how the application response to certain endpoints (uri and http request)
this is handled as:
```javascript
app.METHOD(PATH, HANDLER)
```
where, 
* app: the espress instance
* method: the http request
* path: uri
* handler: the function to execute

### example:
```
app.post('/', (req,res) => {
    res.send('post!')
})
```
* when recieving the post request under root uri, send 'post!'.

### request and response
* req inheriants from http.IncommingMessage. It has such attributes: 
    * method, url, statuscode, ...... (see node.js documentation)
* the express extension has the following in addition:
    * query (e.g. search parameter), app, baseUrl, body, cookies.....

* res inheriants from http.response
    * res.statusCode, res.end('hello world'), res.send()......

## routing example: CRUD
### get list: GET /todos
```javascript
app.get('/todos', (req, res) => {
    fs.readFile('./db.json', 'utf8', (err, data) => {
        if (err) {
            return res.status(500).json({
                error: err.message
            })
        }
        const db = JSON.parse(data)
        res.status(200).json(db.todos)
    })
    // res.send('get /todos') for testing purpose
})
```
### get item according to id: GET /todos/:id
```javascript
app.get('/todos/:id', (req, res) => {
    fs.readFile('./db.json', 'utf8', (err, data) => {
        if (err) {
            return res.status(500).json({
                error: err.message
            })
        }
        const db = JSON.parse(data)
        const todo = db.todos.find(todo => todo.id === Number.parseInt(req.params.id))
        if (!todo){
            return res.status(404).end()
        }
        res.status(200).json(todo)
    })
    
    // res.send('get /todos/${req.params.id}') for testing
})
```
### add list item: POST /todos
```javascript
app.post('/todos', (req, res) => {
    res.send('post /todos')
})
```
### mofify list item: PATCH /todos
```javascript
app.patch('/todos/:id', (req, res) => {
    res.send('patch /todos/${req.params.id}')
})
```
### delete list item: DELETE /todos/:id
```javascript
app.delete('/todos', (req, res) => {
    res.send('delete /todos/${req.params.id}')
})
```
