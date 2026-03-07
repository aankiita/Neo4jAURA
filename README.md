# Neo4jAURA
--------
# CREATE USERS
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
----------
# CREATE USER POSTS

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

-----------
# BIDIRECTIONAL FRIEND

LOAD CSV WITH HEADERS 
FROM 'https://raw.githubusercontent.com/krishnaik06/graph-dataset/refs/heads/main/relationships.csv' 
AS row

MATCH (u1:User {userId: toInteger(row.userId1)}),
      (u2:User {userId: toInteger(row.userId2)})

CREATE (u1)-[:FRIEND]->(u2),
       (u2)-[:FRIEND]->(u1);
       
<img width="1572" height="776" alt="image" src="https://github.com/user-attachments/assets/fcfcbab4-4b23-4f87-a645-9b55f70c5019" />

------------
# GET ALL USER 
MATCH (u:User) RETURN u;

<img width="1589" height="705" alt="image" src="https://github.com/user-attachments/assets/2f421861-321d-4843-8fee-bb385d91d473" />

--------
# RETRIVE ALL POST
MATCH (p:Post) RETURN p;

<img width="1339" height="761" alt="image" src="https://github.com/user-attachments/assets/1f58a6e9-0469-4560-916d-1f4ea073fbe5" />

---------
# RETRIVE THE ALL POST OF THE FRIEND OF JOHN
MATCH (u:User {name:'John'}) - [: FRIEND] -(f:User)-[:POSTED]->(p:Post) return f.name,p.content; 

<img width="1574" height="690" alt="image" src="https://github.com/user-attachments/assets/400c4b18-98b2-477c-8e2c-47fe97b776fa" />


--------
# NUMBER OF FRIEND EACH USER HAVE
MATCH (u:User)-[:FRIEND]-(f:User)
RETURN u.name, COUNT(f) AS numberoffriends
ORDER BY numberoffriends DESC;

<img width="1577" height="600" alt="image" src="https://github.com/user-attachments/assets/202187a1-a1a9-4726-8900-b80b4480555b" />


# ACTOR ACTED IN WHICH MOVIE

<img width="1139" height="649" alt="image" src="https://github.com/user-attachments/assets/a4e9b24c-2b28-4867-bf09-8d4d58a14bf6" />




