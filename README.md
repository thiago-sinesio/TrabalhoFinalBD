Atividade - Livro pontução

Turma34/Petropolis

Alunos:João Pedro Mazzotti de Almeida Ricken, Thiago Sinesio da Silva, João Gabriel Farias Machado, Paulo Guilherme , Emanuel

Consultas:
1) Livros emprestados
SELECT DISTINCT l.titulo
FROM livro l
INNER JOIN emprestimo e 
    ON l.id_livro = e.id_livro;

-- 2) Livros não emprestados
SELECT l.titulo
FROM livro l
LEFT JOIN emprestimo e 
    ON l.id_livro = e.id_livro
WHERE e.id_livro IS NULL;

-- 3) Total de empréstimos
SELECT COUNT(*) AS total_emprestimos
FROM emprestimo;

-- 4) Quantidade de livros por autor
SELECT a.nome, COUNT(l.id_livro) AS quantidade_livros
FROM autor a
LEFT JOIN livro l 
    ON a.id_autor = l.id_autor
GROUP BY a.nome;

-- 5) Livros do mais caro ao mais barato
SELECT l.titulo, e.valor_emprestimo
FROM livro l
INNER JOIN emprestimo e 
    ON l.id_livro = e.id_livro
ORDER BY e.valor_emprestimo DESC;

-- 6) Apagar autor (cascade)
DELETE FROM autor
WHERE id_autor = 1;

-- 7) Total arrecadado por livro
SELECT l.titulo, SUM(e.valor_emprestimo) AS total_arrecadado
FROM livro l
INNER JOIN emprestimo e 
    ON l.id_livro = e.id_livro
WHERE l.id_livro = 2
GROUP BY l.titulo;


CRIAÇÃO DO BANCO (DDL)

-- TABELA AUTOR
CREATE TABLE autor (
    id_autor SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);

-- TABELA LIVRO
CREATE TABLE livro (
    id_livro SERIAL PRIMARY KEY,
    titulo VARCHAR(150) NOT NULL,
    id_autor INT NOT NULL,
    FOREIGN KEY (id_autor)
        REFERENCES autor(id_autor)
        ON DELETE CASCADE
        ON UPDATE NO ACTION OU ON UPDATE RESTRICT
);

-- TABELA USUARIO
CREATE TABLE usuario (
    id_usuario SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL
);

-- TABELA EMPRESTIMO
CREATE TABLE emprestimo (
    id_emprestimo SERIAL PRIMARY KEY,
    data_emprestimo DATE NOT NULL,
    data_devolucao DATE,
    valor_emprestimo DECIMAL(10,2),
    id_usuario INT NOT NULL,
    id_livro INT NOT NULL,
    FOREIGN KEY (id_usuario)
        REFERENCES usuario(id_usuario)
        ON DELETE CASCADE,
    FOREIGN KEY (id_livro)
        REFERENCES livro(id_livro)
        ON DELETE CASCADE
);

Utilização dos INSERTS 



-- AUTORES
INSERT INTO autor (nome) VALUES
('Machado de Assis'),
('Clarice Lispector'),
('Jorge Amado');

-- LIVROS (4 livros, um deles sem empréstimo)
INSERT INTO livro (titulo, id_autor) VALUES
('Dom Casmurro', 1),
('Memórias Póstumas', 1),
('A Hora da Estrela', 2),
('Capitães da Areia', 3);

-- USUÁRIOS
INSERT INTO usuario (nome, email) VALUES
('João Silva', 'joao@email.com'),
('Maria Souza', 'maria@email.com'),
('Carlos Lima', 'carlos@email.com');

-- EMPRÉSTIMOS (LIVRO 2 NAO FOI EMPRESTADO)
INSERT INTO emprestimo (data_emprestimo, data_devolucao, valor_emprestimo, id_usuario, id_livro) VALUES
('2026-03-01', '2026-03-10', 10.00, 1, 1),
('2026-03-05', '2026-03-12', 15.00, 2, 3),
('2026-03-08', '2026-03-15', 12.50, 3, 1);





