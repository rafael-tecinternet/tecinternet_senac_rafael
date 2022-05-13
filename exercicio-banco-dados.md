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
1 - SELECT * FROM alunos WHERE datanascimento < 2009-12-31;

2 - SELECT nome, primeiranota, segundanota, (primeiranota + segundanota)/2 AS 'média' FROM alunos;

3- 

```