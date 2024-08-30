# 02. Distributed Key-Value Store Practice Problem

## Overview

A distributed key-value store is a type of database that uses a simple key-value pair as its data model and is designed to scale out across multiple servers. This practice problem is commonly encountered in technical interviews, assessing a candidate's understanding of distributed systems, data consistency, fault tolerance, and scalability. In this lesson, we will explore the problem statement, requirements, design considerations, and a sample implementation of a distributed key-value store.

## Problem Statement

Design a distributed key-value store that supports the following functionalities:

1. **Put**: Store a key-value pair in the distributed system.
2. **Get**: Retrieve the value associated with a given key.
3. **Delete**: Remove a key-value pair from the store.
4. **Replication**: Ensure that data is replicated across multiple nodes for fault tolerance.
5. **Consistency**: Define how the system will handle consistency, particularly in the presence of network partitions or node failures.

## Requirements

### Functional Requirements

1. **Put Operation**:

   - Input: A key (e.g., "user:123") and a value (e.g., "John Doe").
   - Output: A confirmation of successful storage.

2. **Get Operation**:

   - Input: A key (e.g., "user:123").
   - Output: The associated value (e.g., "John Doe") or an error if the key does not exist.

3. **Delete Operation**:

   - Input: A key (e.g., "user:123").
   - Output: A confirmation of successful deletion or an error if the key does not exist.

4. **Replication**: Data should be replicated across multiple nodes to ensure availability and fault tolerance.

5. **Consistency**: Define the consistency model (e.g., eventual consistency, strong consistency) and how it will be maintained.

### Non-Functional Requirements

1. **Scalability**: The system should be able to scale horizontally by adding more nodes.
2. **Fault Tolerance**: The system should remain operational even in the event of node failures.
3. **Performance**: Operations (put, get, delete) should be performed with minimal latency.

## Design Considerations

### Data Storage

- **Key-Value Pair**: Each entry in the store consists of a unique key and its associated value.
- **Data Partitioning**: Use consistent hashing to distribute data across multiple nodes, ensuring even load distribution and easy scalability.

### Replication

- **Replication Strategy**: Implement a replication strategy to ensure data durability and availability. Common strategies include:
  - **Master-Slave Replication**: One node acts as the master (primary), while others are slaves (replicas) that receive updates from the master.
  - **Multi-Master Replication**: Multiple nodes can accept write operations, allowing for higher availability.

### Consistency Model

- **Eventual Consistency**: Ensure that all updates will eventually propagate to all replicas, allowing for temporary inconsistencies.
- **Strong Consistency**: Ensure that all nodes reflect the most recent write before any read operation is allowed.

### API Design

Design a simple RESTful API with the following endpoints:

1. **PUT /store**

   - Request Body: `{ "key": "user:123", "value": "John Doe" }`
   - Response: `{ "status": "success" }`

2. **GET /store/{key}**

   - Request: `GET /store/user:123`
   - Response: `{ "value": "John Doe" }` or an error message if the key does not exist.

3. **DELETE /store/{key}**
   - Request: `DELETE /store/user:123`
   - Response: `{ "status": "success" }` or an error message if the key does not exist.

## Implementation

### Example Implementation in Python

Here’s a simplified version of how you might implement a distributed key-value store in Python using Flask and a basic in-memory storage mechanism:

```python
from flask import Flask, request, jsonify
import hashlib
import random

app = Flask(__name__)

# In-memory storage for demonstration purposes
store = {}
replica_nodes = ['node1', 'node2', 'node3']  # Simulated nodes

def hash_key(key):
    """Hash the key to determine the node."""
    return int(hashlib.md5(key.encode()).hexdigest(), 16) % len(replica_nodes)

@app.route('/store', methods=['PUT'])
def put_value():
    key = request.json.get('key')
    value = request.json.get('value')
    if not key or value is None:
        return jsonify({"error": "Invalid input"}), 400

    # Determine the node for the key
    node = replica_nodes[hash_key(key)]
    store[key] = value  # Simulate storage on the chosen node
    return jsonify({"status": "success", "node": node})

@app.route('/store/<key>', methods=['GET'])
def get_value(key):
    value = store.get(key)
    if value is not None:
        return jsonify({"value": value})
    return jsonify({"error": "Key not found"}), 404

@app.route('/store/<key>', methods=['DELETE'])
def delete_value(key):
    if key in store:
        del store[key]
        return jsonify({"status": "success"})
    return jsonify({"error": "Key not found"}), 404

if __name__ == '__main__':
    app.run(debug=True)
```

### Explanation of the Implementation

1. **Flask Framework**: The example uses Flask to create a simple RESTful API for the key-value store.
2. **In-Memory Storage**: For simplicity, an in-memory dictionary (`store`) is used to store key-value pairs.
3. **Hashing**: The `hash_key` function determines which node should store the data based on the hashed key.
4. **Endpoints**:
   - **PUT /store**: Accepts a key and value, stores it, and returns a success message.
   - **GET /store/{key}**: Retrieves the value for a given key or returns an error if the key does not exist.
   - **DELETE /store/{key}**: Deletes the specified key and returns a success message or an error if the key does not exist.

## Conclusion

The distributed key-value store practice problem provides an excellent opportunity to demonstrate system design and implementation skills. By understanding the requirements, design considerations, and implementation details, candidates can effectively tackle this problem in a technical interview setting. Building a distributed key-value store not only tests a candidate's technical abilities but also their understanding of distributed systems, data consistency, and fault tolerance.

Next: [03. Social Media Timeline](./03-social-media-timeline.md)
