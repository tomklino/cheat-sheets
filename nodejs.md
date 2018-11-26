# nodejs cheat-sheet

## function for handling http responses
```js
function handleResponse(res) {
  let data ='';
  res.on('data', (chunk) => { data += chunk; })
  res.on('end', () => console.log(data))
}

//usage:
http.get('http://example.com', handleResponse)
```
