# Banco-de-dados
--Encontrar a nota máxiam, a minima e a média de horas de sono--
```
SELECT 
MAX(nota_exame) AS nota_maxima,
MIN(nota_exame) AS nota_minima,
AVG(horas_de_sono) AS media_horas_sono
FROM notas_alunos;
```
-- Contar quantos alunnos tiraram menos de 25 no exame:
```
SELECT COUNT(id_aluno) AS total_alunos_baixo_desempenho
FROM notas_alunos
WHERE nota_exame < 25.0;
```
-- lista as 5 alunos com as maiores notas no exame (nota_exame), mostrando a nota e as horas estudadas:
```
SELECT id_aluno, nota_exame, horas_estudadas
FROM notas_alunos
ORDER BY nota_exame desc
LIMIT 5;
```
-- Listar todos os alunos ordenados do menos para o maior percentual de precença:
```
SELECT id_aluno, percental_presenca
FROM notas_alunos
ORDER BY percentual_presenca ASC;
```

-- Filtragem avançada (goup by, having)
-- Classificar os alunos por faixa de notas_anteriores
-- ex: Faixa A:>90, Faixa B: >70-90, Faixa C <7- e calcular a nota_exame média para cada faixa

```sql
SELECT
   case
      when notas_anteriores > 90 then 'Faixa A (>90)'
      when notas_anteriores BETWEEN 70 AND 90 then ' Faixa B (70-90)'
      ELSE 'Faixa C (<70)'
   END AS faixa_notas_anteriores,
   AVG(nota_exame) AS media_nota_exame,
   COUNT(id_aluno) AS total_alunos
   AVG(notas_anteriores) AS media_notas_anteriores,
   AVG(notas_anteriores + nota_exame)/2 AS media_final
FROM notas_alunos
GROUP BY faixa_notas_anteriores
ORDER BY media_nota_exame DESC;

-- Encontrar a média de notas_exame apenas para os alunos que 
-- tiveram mais de 90% de presença (percentual_presenca):
SELECT AVG(nota_exame) AS media_exame_alta_presenca
FROM notas_alunos
WHERE percentual_presenca > 90.0;
```
