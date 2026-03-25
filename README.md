Atividade - Livro pontução

Turma34/Petropolis

Alunos:João Pedro Mazzotti de Almeida Ricken, Thiago Sinesio da Silva, João Gabriel Farias Machado, Paulo Guilherme , Emanuel

Consultas:

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
WHERE l.id_livro = 1
GROUP BY l.titulo;
