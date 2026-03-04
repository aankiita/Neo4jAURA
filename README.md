# Neo4jAURA

LOAD CSV WITH HEADERS 
FROM 'https://raw.githubusercontent.com/krishnaik06/graph-dataset/refs/heads/main/users_social.csv' 
AS row
CREATE (:User {
    userId: toInteger(row.userId),
    name: row.name,
    age: toInteger(row.age),
    city: row.city
});

<img width="1038" height="694" alt="image" src="https://github.com/user-attachments/assets/c763f235-8506-4180-a453-5c16ad3f0374" />

LOAD CSV WITH HEADERS 
FROM 'https://raw.githubusercontent.com/krishnaik06/graph-dataset/refs/heads/main/posts.csv' 
AS row

MATCH (u:User {userId: toInteger(row.userId)})

CREATE (u)-[:POSTED]->(:Post {
    postId: toInteger(row.postId),
    content: row.content,
    timestamp: datetime(row.timestamp)
});

<img width="663" height="511" alt="image" src="https://github.com/user-attachments/assets/6e121fbe-c292-43fd-8050-add2c7c7cc90" />



LOAD CSV WITH HEADERS 
FROM 'https://raw.githubusercontent.com/krishnaik06/graph-dataset/refs/heads/main/relationships.csv' 
AS row

MATCH (u1:User {userId: toInteger(row.userId1)}),
      (u2:User {userId: toInteger(row.userId2)})

CREATE (u1)-[:FRIEND]->(u2),
       (u2)-[:FRIEND]->(u1);
<img width="1572" height="776" alt="image" src="https://github.com/user-attachments/assets/fcfcbab4-4b23-4f87-a645-9b55f70c5019" />
