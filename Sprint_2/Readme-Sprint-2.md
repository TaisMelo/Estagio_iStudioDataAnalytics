E1  

Apresente a query para listar todos os livros publicados após 2014. Ordenar pela coluna cod, em ordem crescente, as linhas.  Atenção às colunas esperadas no resultado final: cod, titulo, autor, editora, valor, publicacao, edicao, idioma

Resposta: 

SELECT * FROM livro
WHERE publicacao >'2014-12-31'
ORDER BY cod 

E2

Apresente a query para listar os 10 livros mais caros. Ordenar as linhas pela coluna valor, em ordem decrescente.  Atenção às colunas esperadas no resultado final:  titulo, valor.

Resposta:

SELECT titulo, valor
FROM livro 
ORDER BY valor DESC 
LIMIT 10

E3

Apresente a query para listar as 5 editoras com mais livros na biblioteca. O resultado deve conter apenas as colunas quantidade, nome, estado e cidade. Ordenar as linhas pela coluna que representa a quantidade de livros em ordem decrescente.

Resposta:

SELECT count(livro.editora) AS quantidade, editora.nome, endereco.estado, endereco.cidade 
FROM editora
INNER JOIN endereco ON editora.endereco = endereco.codendereco
INNER JOIN livro ON livro.editora = editora.codeditora 
group by livro.editora 
ORDER BY quantidade DESC 
limit 5


E4
Apresente a query para listar a quantidade de livros publicada por cada autor. Ordenar as linhas pela coluna nome (autor), em ordem crescente. Além desta, apresentar as colunas codautor, nascimento e quantidade (total de livros de sua autoria).

Resposta:

SELECT autor.codautor, autor.nome, autor.nascimento, COUNT (livro.titulo)
 as quantidade 
FROM autor
LEFT JOIN livro ON autor.codautor = livro.autor 
GROUP BY autor.nome
ORDER BY autor.nome ASC 

E5

Apresente a query para listar o nome dos autores que publicaram livros através de editoras NÃO situadas na região sul do Brasil. Ordene o resultado pela coluna nome, em ordem crescente.

Resposta:

SELECT autor.nome
FROM autor
LEFT JOIN livro l on autor.codautor = l.autor
INNER JOIN editora e on e.codeditora = l.editora
INNER JOIN endereco e2 on e2.codendereco = e.endereco
WHERE  e2.estado <> 'RIO GRANDE DO SUL' AND e2.estado <> 'PARANÁ'
ORDER BY autor.nome ASC

E6
Apresente a query para listar o autor com maior número de livros publicados. O resultado deve conter apenas as colunas codautor, nome, quantidade_publicacoes.

Resposta:

SELECT autor.codautor, autor.nome, COUNT (livro.titulo)
 as quantidade_publicacoes
FROM autor
INNER JOIN livro ON autor.codautor = livro.autor 
GROUP BY autor.nome
ORDER BY quantidade_publicacoes DESC 
LIMIT 1

E7

Apresente a query para listar o nome dos autores com nenhuma publicação. Apresentá-los em ordem crescente.

Resposta:

SELECT autor.nome 
FROM autor
LEFT JOIN livro on autor.codautor = livro.autor 
WHERE autor.codautor = livro.autor ISNULL 