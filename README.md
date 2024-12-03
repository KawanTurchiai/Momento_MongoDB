# Atividade Momento MongoDB

Este repositório contém as atividades realizadas utilizando o MongoDB para gerenciar informações da empresa fake chamada **Momento**. O objetivo é gerenciar dados dos funcionários e departamentos, assim como realizar consultas e agregações no banco de dados.

## Tarefas Realizadas

Abaixo estão as tarefas realizadas, juntamente com as respectivas consultas MongoDB utilizadas:

### 1. Quantos funcionários da empresa **Momento** trabalham no departamento de vendas?

**Resultado:** 10 funcionários

Consulta MongoDB:
```javascript
db.funcionarios.countDocuments({ cargo: /vendas/i })
```
### 2. Inclusão de informações no departamento de Tecnologia
Instrução: Inclua suas próprias informações no departamento de Tecnologia da empresa.

Resultado: Registro inserido com sucesso.

Consulta MongoDB:
```
javascript
Copiar código
db.funcionarios.insertOne({
  nome: 'Kawan Barbosa Turchiai',
  telefone: '11 95113-5113',
  cargo: 'Mobile Developer',
  salario: 27000,
  departamento: ObjectId("85992103f9b3e0b3b3c1fe74")
})
```
3. Quantos funcionários a empresa possui no total?
Resultado: 24 funcionários

Consulta MongoDB:

javascript
Copiar código
db.funcionarios.countDocuments({})
4. Quantos funcionários existem no Departamento de Tecnologia?
Resultado: 6 funcionários

Consulta MongoDB:

javascript
Copiar código
db.funcionarios.countDocuments({ departamento: ObjectId('85992103f9b3e0b3b3c1fe74') })
5. Qual a média salarial do Departamento de Tecnologia?
Resultado: A média salarial é de R$ 8.300

Consulta MongoDB:

javascript
Copiar código
db.funcionarios.aggregate([
  { $match: { departamento: ObjectId("85992103f9b3e0b3b3c1fe74") } },
  { $group: { _id: "$departamento", media: { $avg: "$salario" } } }
])
6. Quanto o departamento de Vendas gasta em salários?
Resultado: O total gasto em salários é de R$ 61.100

Consulta MongoDB:

javascript
Copiar código
db.funcionarios.aggregate([
  { $match: { departamento: ObjectId("5992103f9b3e0b3b3c1e3e3f") } },
  { $group: { _id: "$departamento", TotalSalario: { $sum: "$salario" } } }
])
7. Criação do Departamento de Inovações
Instrução: Adicionar o novo departamento de Inovações ao banco de dados.

Resultado: Departamento de Inovações criado com sucesso.

Consulta MongoDB (exemplo de criação de departamento):

javascript
Copiar código
db.departamentos.insertOne({
  nome: 'Inovações',
  localizacao: 'Brasil',
  descricao: 'Departamento focado em novas soluções tecnológicas.'
})
8. Inclusão de funcionários no Departamento de Inovações
Instrução: Incluir alguns funcionários no novo departamento de Inovações.

9. Quantos funcionários a empresa Momento possui agora?
Resultado: [Número de funcionários após a inserção].

Consulta MongoDB:

javascript
Copiar código
db.funcionarios.countDocuments({})
10. Quantos funcionários possuem cônjuges?
Resultado: [Número de funcionários com cônjuges].

Consulta MongoDB:

javascript
Copiar código
db.funcionarios.countDocuments({ cônjuge: { $exists: true } })
11. Qual a média salarial de todos os funcionários da empresa, excluindo o CEO?
Resultado: [Média salarial excluindo o CEO].

Consulta MongoDB:

javascript
Copiar código
db.funcionarios.aggregate([
  { $match: { cargo: { $ne: 'CEO' } } },
  { $group: { _id: null, mediaSalarial: { $avg: "$salario" } } }
])
12. Qual o departamento com a maior média salarial?
Resultado: [Departamento com maior média salarial].

Consulta MongoDB:

javascript
Copiar código
db.funcionarios.aggregate([
  { $group: { _id: "$departamento", mediaSalarial: { $avg: "$salario" } } },
  { $sort: { mediaSalarial: -1 } },
  { $limit: 1 }
])
13. Qual o departamento com o menor número de funcionários?
Resultado: [Departamento com menor número de funcionários].

Consulta MongoDB:

javascript
Copiar código
db.funcionarios.aggregate([
  { $group: { _id: "$departamento", totalFuncionarios: { $sum: 1 } } },
  { $sort: { totalFuncionarios: 1 } },
  { $limit: 1 }
])
14. Pensando na relação quantidade e valor unitário, qual o produto mais valioso da empresa?
Resultado: [Produto mais valioso].

Consulta MongoDB:

javascript
Copiar código
db.produtos.aggregate([
  { $project: { nome: 1, valorTotal: { $multiply: ["$quantidade", "$valorUnitario"] } } },
  { $sort: { valorTotal: -1 } },
  { $limit: 1 }
])
15. Qual o produto mais vendido da empresa?
Resultado: [Produto mais vendido].

Consulta MongoDB:

javascript
Copiar código
db.produtos.aggregate([
  { $group: { _id: "$nome", totalVendido: { $sum: "$quantidade" } } },
  { $sort: { totalVendido: -1 } },
  { $limit: 1 }
])
16. Qual o produto menos vendido da empresa?
Resultado: [Produto menos vendido].

Consulta MongoDB:

javascript
Copiar código
db.produtos.aggregate([
  { $group: { _id: "$nome", totalVendido: { $sum: "$quantidade" } } },
  { $sort: { totalVendido: 1 } },
  { $limit: 1 }
])
