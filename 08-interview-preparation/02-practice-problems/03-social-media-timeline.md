# 03. Social Media Timeline Practice Problem

## Overview

The social media timeline problem is a common technical interview question that tests a candidate's ability to design a system capable of displaying a user's feed of posts in a scalable and efficient manner. This problem involves understanding data structures, algorithms, and system design principles. In this lesson, we will explore the problem statement, requirements, design considerations, and a sample implementation of a social media timeline service.

## Problem Statement

Design a social media timeline service that provides the following functionalities:

1. **Post Creation**: Allow users to create new posts.
2. **Follow Users**: Enable users to follow other users to see their posts in their timeline.
3. **Display Timeline**: Retrieve and display a user's timeline, which includes posts from users they follow, sorted by the time of creation.
4. **Pagination**: Support pagination for the timeline to efficiently load posts.

## Requirements

### Functional Requirements

1. **Create Post**:

   - Input: A user ID and the content of the post (e.g., text, images).
   - Output: A confirmation of successful post creation.

2. **Follow User**:

   - Input: A follower user ID and a followee user ID.
   - Output: A confirmation of successful follow action.

3. **Get Timeline**:

   - Input: A user ID.
   - Output: A list of posts from users that the specified user follows, sorted by creation time (most recent first).

4. **Pagination**: Allow users to specify the number of posts to retrieve at once and provide a mechanism to fetch more posts.

### Non-Functional Requirements

1. **Scalability**: The service should be able to handle a large number of users and posts efficiently.
2. **Performance**: Retrieving and displaying the timeline should be done quickly, with minimal latency.
3. **Data Persistence**: Store user data, posts, and follow relationships in a persistent storage solution.

## Design Considerations

### Data Storage

- **Database**: A relational database (e.g., PostgreSQL) or a NoSQL database (e.g., MongoDB) can be used to store user profiles, posts, and follow relationships.
- **Data Model**:
  - **Users Table**: Stores user information (user ID, username, etc.).
  - **Posts Table**: Stores posts (post ID, user ID, content, timestamp).
  - **Follows Table**: Stores follow relationships (follower ID, followee ID).

### Data Retrieval

- **Feed Generation**: When a user requests their timeline, the system should retrieve posts from all users they follow. This can be achieved using a JOIN operation in a relational database or aggregation in a NoSQL database.
- **Sorting**: Posts should be sorted by timestamp to display the most recent posts first.

### Pagination

- **Limit and Offset**: Implement pagination using limit and offset parameters to control the number of posts returned in a single request.
- **Cursor-Based Pagination**: Alternatively, consider using cursor-based pagination, which can be more efficient for large datasets.

### API Design

Design a simple RESTful API with the following endpoints:

1. **POST /posts**

   - Request Body: `{ "userId": "123", "content": "This is a new post" }`
   - Response: `{ "status": "success", "postId": "456" }`

2. **POST /follow**

   - Request Body: `{ "followerId": "123", "followeeId": "456" }`
   - Response: `{ "status": "success" }`

3. **GET /timeline/{userId}**

   - Request: `GET /timeline/123`
   - Response: `{ "posts": [ { "postId": "456", "userId": "456", "content": "This is a new post", "timestamp": "2024-08-30T12:00:00Z" }, ... ] }`

4. **GET /timeline/{userId}?limit=10&offset=0**
   - Request: `GET /timeline/123?limit=10&offset=0`
   - Response: Returns the first 10 posts for the user.

## Implementation

### Example Implementation in Python

Here’s a simplified version of how you might implement a social media timeline service in Python using Flask:

```python
from flask import Flask, request, jsonify
from datetime import datetime
from collections import defaultdict

app = Flask(__name__)

# In-memory storage for demonstration purposes
users = {}
posts = []
follows = defaultdict(set)  # follower -> set of followees

@app.route('/posts', methods=['POST'])
def create_post():
    user_id = request.json.get('userId')
    content = request.json.get('content')
    if not user_id or not content:
        return jsonify({"error": "Invalid input"}), 400

    post_id = len(posts) + 1
    timestamp = datetime.utcnow().isoformat()
    posts.append({"postId": post_id, "userId": user_id, "content": content, "timestamp": timestamp})
    return jsonify({"status": "success", "postId": post_id})

@app.route('/follow', methods=['POST'])
def follow_user():
    follower_id = request.json.get('followerId')
    followee_id = request.json.get('followeeId')
    if not follower_id or not followee_id:
        return jsonify({"error": "Invalid input"}), 400

    follows[follower_id].add(followee_id)
    return jsonify({"status": "success"})

@app.route('/timeline/<user_id>', methods=['GET'])
def get_timeline(user_id):
    followed_users = follows.get(user_id, set())
    user_posts = [post for post in posts if post['userId'] in followed_users]

    # Sort posts by timestamp (most recent first)
    user_posts.sort(key=lambda x: x['timestamp'], reverse=True)

    # Pagination
    limit = int(request.args.get('limit', 10))
    offset = int(request.args.get('offset', 0))
    paginated_posts = user_posts[offset:offset + limit]

    return jsonify({"posts": paginated_posts})

if __name__ == '__main__':
    app.run(debug=True)
```

### Explanation of the Implementation

1. **Flask Framework**: The example uses Flask to create a simple RESTful API for the social media timeline service.
2. **In-Memory Storage**: For simplicity, an in-memory list (`posts`) and a dictionary (`follows`) are used to store posts and follow relationships.
3. **Endpoints**:
   - **POST /posts**: Accepts a user ID and content, creates a new post, and returns a success message.
   - **POST /follow**: Accepts follower and followee IDs, updates the follow relationship, and returns a success message.
   - **GET /timeline/{userId}**: Retrieves the timeline for a specified user, filtering and sorting posts from followed users, with support for pagination.

## Conclusion

The social media timeline practice problem provides an excellent opportunity to demonstrate system design, data management, and API development skills. By understanding the requirements, design considerations, and implementation details, candidates can effectively tackle this problem in a technical interview setting. Building a social media timeline service not only tests a candidate's technical abilities but also their understanding of user interactions, data retrieval, and scalability.

Next: [04. Parking Lot Systems](./04-parking-lot-system.md)
