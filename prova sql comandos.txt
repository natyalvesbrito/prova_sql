CREATE TABLE produtos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    preco DECIMAL(10, 2) NOT NULL);

CREATE TABLE categorias (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);

CREATE TABLE produtos_categorias (
    produto_id INTEGER REFERENCES produtos(id),
    categoria_id INTEGER REFERENCES categorias(id),
    PRIMARY KEY (produto_id, categoria_id)
);

------ questão 3 -----
SELECT 
	nome AS "Produto", 
	preco AS "Valor"
FROM produtos
WHERE preco > 100
ORDER BY preco,nome

INSERT INTO produtos (nome, preco)
VALUES ('produto2', 90)

-------- questão 4 -----
SELECT 
	id,
	preco
FROM produtos
WHERE preco > (SELECT AVG(preco) FROM produtos);

------ questão 5 ---------
SELECT 
    c.nome AS Categoria,
    AVG(p.preco) AS PrecoMedio
FROM categorias c
JOIN produtos_categorias pc ON c.id = pc.categoria_id
JOIN produtos p ON pc.produto_id = p.id
GROUP BY c.nome
ORDER BY c.nome;

------ questão 6 --------
CREATE TABLE turma (
    id_turma SERIAL PRIMARY KEY,
    codigo_turma VARCHAR(20) NOT NULL,
    nome_turma VARCHAR(100) NOT NULL
);

CREATE TABLE aluno (
    id_aluno SERIAL PRIMARY KEY,
    nome_aluno VARCHAR(100) NOT NULL,
    aluno_alocado BOOLEAN,
    id_turma INT,
    FOREIGN KEY (id_turma) REFERENCES turma(id_turma)
);

----------- questão 7 ----------
INSERT INTO turma (codigo_turma, nome_turma)
VALUES 
	('#0001', 'turma_a'),
	('#0002', 'turma_b');
	
SELECT * FROM turma
SELECT * FROM aluno

INSERT INTO aluno (nome_aluno, id_turma)
VALUES
	('João', 1),
	('Maria', 2);
	
INSERT INTO aluno (nome_aluno)
VALUES
	('José'),
	('Vânia'),
	('Michelly');
	
UPDATE aluno
SET aluno_alocado = 
CASE 
	WHEN id_turma NOTNULL THEN True
	ELSE False
 END;

