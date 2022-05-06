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
    cargahoraria ENUM('desung', 'desenvolvimento', 'infra') NOT NULL,
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