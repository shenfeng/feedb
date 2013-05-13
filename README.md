# Feedb

A special key-value storage server written in go and mmap.


### Motivation

Rssminer's disk usage can save roughly 50% with this storage server.
Key is integer. Think about MySQL's primary key: auto-increment from small number. The intended usage is store metadata in MySQL, use the generated primary key to key the large chunk of data to feedb.


### Save data
```sh
# body len byte of data
POST http://127.0.0.1/d/feeds?id=:key&len=:len
```

### Get data

```sh
GET http://127.0.0.1/d/feeds/:key
# optional parameter  &text=1, output Content-Type: text/plain to the HTTP Response, useful for browser debug
# optional parameter  &deflate=1, output "Content-Encoding", "deflate" to the HTTP Response, useful for browser debug
```

### MultiGet data

Return a json response

```js
[{Id: 111, Data: "this is data of key 111"},
{Id: 112, Data: "this is data2 of key 112"}]

```

```sh
GET http://127.0.0.1/d/feeds/:key1-key2
# optional parameter  &deflate=1, will deflate the stored data
```
