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