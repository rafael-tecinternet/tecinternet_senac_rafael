```sql
CREATE TABLE cursos (
    id TINYINT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(30) NOT NULL,
    cargahoraria TINYINT NOT NULL,
    professor_id TINYINT
);

CREATE TABLE professores (
    id TINYINT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL,
    cargahoraria ENUM('desing', 'desenvolvimento', 'infra') NOT NULL,
    curso_id TINYINT NOT NULL
);

CREATE TABLE alunos (
    id TINYINT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL,
    datanascimento DATE NOT NULL,
    primeiranota TINYINT NOT NULL,
    segundanota TINYINT NOT NULL,
    curso_id TINYINT NOT NULL
);
```


```sql
ALTER TABLE alunos
    ADD CONSTRAINT fk_alunos_cursos
    FOREIGN KEY(curso_id) REFERENCES cursos(id);
```
```sql
ALTER TABLE cursos
    ADD CONSTRAINT fk_cursos_professores1
    FOREIGN KEY(professor_id) REFERENCES professores(id);
```
```sql
ALTER TABLE professores
    ADD CONSTRAINT fk_professores_cursos1
    FOREIGN KEY(curso_id) REFERENCES cursos(id);
```


```sql
INSERT INTO `cursos` (`id`, `titulo`, `cargahoraria`, `professor_id`) VALUES (NULL, 'Front-End', '40', NULL);

INSERT INTO `professores` (`id`, `nome`, `cargahoraria`, `curso_id`) VALUES (NULL, 'Lemmy Kilmister', 'desing', '4');

INSERT INTO `alunos` (`id`, `nome`, `datanascimento`, `primeiranota`, `segundanota`, `curso_id`) VALUES (NULL, 'Rafael', '1994-10-11', '7', '9', '5')
```
```sql


1 - SELECT * FROM alunos WHERE datanascimento < '2009-01-01';

2 - SELECT nome, primeiranota, segundanota, ROUND(((primeiranota + segundanota)/2),2) AS 'média' FROM alunos;

3- SELECT titulo AS 'Cursos', (cargahoraria * 0.25) AS 'Limite de faltas' FROM cursos ORDER BY titulo;

4- SELECT nome AS 'Professores', areadeatuacao AS 'Área' FROM professores WHERE areadeatuacao = 'desenvolvimento';

5- SELECT areadeatuacao AS 'Área', COUNT(nome) AS 'Professores' FROM professores GROUP BY areadeatuacao;

6- SELECT alunos.nome AS 'Alunos', cursos.titulo AS 'Curso', cursos.cargahoraria AS 'Carga Horaria'
FROM alunos INNER JOIN cursos
ON alunos.curso_id = cursos.id;

7- SELECT professores.nome AS 'Professores', cursos.titulo AS 'Curso' 
FROM professores INNER JOIN cursos
ON professores.curso_id = cursos.id
ORDER BY professores.nome;

8- SELECT alunos.nome AS 'Alunos', cursos.titulo AS 'Cursos', professores.nome AS 'Professor'
FROM alunos INNER JOIN cursos
ON alunos.curso_id = cursos.id
INNER JOIN professores
ON professores.curso_id = cursos.id;

9- SELECT cursos.titulo AS 'Cursos', COUNT(alunos.curso_id) AS 'Quantidade'
FROM alunos LEFT JOIN cursos
ON alunos.curso_id = cursos.id
GROUP BY cursos
ORDER BY cursos.titulo DESC;

10- SELECT alunos.nome AS 'Alunos', alunos.primeiranota AS 'Nota 1', alunos. segundanota AS 'Nota 2', ROUND(((primeiranota + segundanota)/2),2) AS 'Média', cursos.titulo 
FROM alunos INNER JOIN cursos
ON alunos.curso_id = cursos.id
WHERE cursos.titulo = 'Front-End' OR cursos.titulo = 'Back-End'
GROUP BY alunos.nome
ORDER BY alunos.nome;

11- UPDATE cursos SET titulo = 'AdobeXD' WHERE id = 4;
    UPDATE cursos SET cargahoraria = 15 WHERE id = 4;

12- DELETE FROM alunos WHERE id = 3 OR id = 4;

13- SELECT alunos.nome AS 'Alunos', cursos.titulo AS 'Curso' 
FROM alunos LEFT JOIN cursos 
ON alunos.curso_id = cursos.id
GROUP BY alunos;
```
### Desafio
```sql
SELECT nome AS 'Aluno', TIMESTAMPDIFF(YEAR, datanascimento, CURDATE()) AS 'Idade' FROM alunos;

SELECT nome, ROUND(((primeiranota + segundanota)/2), 2) AS 'media' FROM alunos WHERE ROUND(((primeiranota + segundanota)/2), 2) >= 7.0 ;


SELECT nome, ROUND(((primeiranota + segundanota)/2), 2) AS 'media' FROM alunos WHERE ROUND(((primeiranota + segundanota)/2), 2) < 7.0 ;

SELECT COUNT(id) AS 'Alunos com nota maior ou igual a 7' FROM alunos WHERE ROUND(((primeiranota + segundanota)/2), 2) >= 7.0 ;

```