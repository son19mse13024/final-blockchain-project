Install the dependencies,
```sh
$ cd python_blockchain_app
$ pip install -r requirements.txt
```

Start a node server

```sh
$ export FLASK_APP=node_server.py
$ flask run --port 8000
```

Run the application on a different terminal session,

```sh
$ python run_app.py
```

The application running at [http://localhost:5000](http://localhost:5000).

Requests to register the nodes at port `8001` and `8002` with the already running `8000`.

```sh
# already running
$ flask run --port 8000 &
# spinning up new nodes
$ flask run --port 8001 &
$ flask run --port 8002 &
```


```sh
curl -X POST \
  http://127.0.0.1:8001/register_with \
  -H 'Content-Type: application/json' \
  -d '{"node_address": "http://127.0.0.1:8000"}'
```

```sh
curl -X POST \
  http://127.0.0.1:8002/register_with \
  -H 'Content-Type: application/json' \
  -d '{"node_address": "http://127.0.0.1:8000"}'
```

When mine the transactions, all the nodes in the network will update the chain.

```sh
$ curl -X GET http://localhost:8001/chain
$ curl -X GET http://localhost:8002/chain
```