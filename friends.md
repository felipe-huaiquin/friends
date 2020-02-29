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
WHERE users.first_name LIKE '%Kermit%'
```
3. Consulta que retorna la persona con más amigos. 
```

```
