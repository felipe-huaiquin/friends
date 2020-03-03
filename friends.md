# Friends

1. Consulta para obtener las amistades de cada usuario. La consulta devuelve el nombre y apellido del usuario y el de sus amigos, ordenados de manera ascendente por el primer nombre del usuario.
```
SELECT users.first_name, users.last_name, users2.first_name AS friend_fname, users2.last_name AS friend_lname
FROM users
LEFT JOIN friendships ON  friendships.user_id = users.id
LEFT JOIN users AS users2 ON  friendships.friend_id = users2.id
WHERE users2.id IS NOT NULL
ORDER BY users.first_name ASC;
```
2. Consulta para obtener todos los amigos de Kermit. La consulta devuelve el nombre completo de todos sus amigos.
```
SELECT users.first_name, users.last_name, users2.first_name AS friend_fname, users2.last_name AS friend_lname
FROM users
LEFT JOIN friendships ON friendships.friend_id = users.id
LEFT JOIN users AS users2 ON friendships.user_id = users2.id
WHERE users.first_name LIKE '%Kermit%';
```
3. Consulta que retorna la persona con más amigos. 
```
SELECT test.name, MAX(number_friends)
FROM (SELECT CONCAT(users.first_name," ",users.last_name) AS name, COUNT(users.id) AS number_friends
FROM users
LEFT JOIN friendships ON friendships.user_id = users.id
LEFT JOIN friendships AS friendships2 ON friendships2.friend_id = users.id
GROUP BY users.id
) AS test;
```
4. Consulta para insertar un nuevo usuario a la base de datos y hacerlo amigo de: Eli Byers, Kermit The Frog y Marky Mark.
```
INSERT INTO users (first_name, last_name, created_at, updated_at)
VALUES ('Mento','Lathum',NOW(),NOW())
INSERT INTO friendships (user_id, friend_id,created_at, updated_at)
VALUES
	('6','2',NOW(),NOW()),
    ('6','4',NOW(),NOW()),
    ('6','5',NOW(),NOW());
```
5. Consulta que retorna los amigos de Eli Bayers.
```
SELECT CONCAT(users2.first_name," ",users2.last_name) AS friend_name
FROM users
LEFT JOIN friendships ON friendships.user_id = users.id
LEFT JOIN users AS users2 ON friendships.friend_id = users2.id
WHERE users.id = 2;
```
6. Consulta que elimina a Marky Mark de los amigos de Eli Bayers.
```
DELETE FROM friendships
WHERE user_id = 2 AND friend_id = 5;
```
7. Consulta que devuelve todos los amigos, mostrando solo el nombre y apellidos de ambos.
```
SELECT CONCAT(users.first_name," ",users.last_name) AS user_name, CONCAT(users2.first_name," ",users2.last_name) AS friend_name
FROM users
LEFT JOIN friendships ON friendships.user_id = users.id
LEFT JOIN users AS users2 ON friendships.friend_id = users2.id
WHERE friendships.friend_id IS NOT NULL
ORDER BY user_name DESC;
```