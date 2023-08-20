# Exploring-Neo4j
Exploring Neo4j for an email model

# Gmail Data Model
Draw a simple graph data model for the following Gmail scenario
- “Student 1” sent an email message to Professor
- “Student 1” CC-ed the email to Teammates 
- “Student 1” also BCC-ed the email to any names of your friends

## Explanation of Data Model

### Types of nodes
- Users: User nodes include properties such as their name, email address, and username. I have not distinguished between senders and receivers as separate node types since all users can both receive and send emails. Instead, we use relationships to connect users and emails.
- Emails: Email nodes include only the content of the email considering the scope of this
assignment’s requirements. Email nodes can have encryption types, attachments, calendar
invites, flags for priority, etc.

### Types of relationships
- To: (Email -> Primary recipient)
- From: (Email -> Sender)
- Sends: (Sender -> Email)
- CC: (Email -> Copied recipient)
- BCC: (Email -> (Blind) Copied recipient)

### Example Query
```
CREATE (:User {name: "Student 1", email:
"s1@gmail.com", username: "stu1"})
CREATE (:Email {content: "Hi Professor, I found the class to
be very useful and interesting. I am sure it will be helpful in the
future."})
MATCH (sender:User {email: "s1@gmail.com"}), (primary:User
{email: "prof@gmail.com"}),
(cc1:User {email: "s2@gmial.com"}), (cct2:User {email:
"s3.student@gmail.com"}), (bcc:User {email: "s4s4@gamil.com"}),
(email: Email {content: "Hello Professor, I found the NoSQL class
to be very useful and interesting. I am sure it will be helpful in the
future."})CREATE (sender)-[:Sends]->(email), (email)-[:From]->(sender),
(email)-[:To]->(primary), (email)-[:CC]->(cc1), (email)-[:CC]->(cc2),
(email)-[:BCC]->(bcc)
```
