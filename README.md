# Atividade Momento MongoDB

Este repositório contém as atividades realizadas utilizando o MongoDB para gerenciar informações da empresa **Momento**. Abaixo estão as tarefas realizadas e as respectivas consultas ao banco de dados.

## 1. Quantos funcionários da empresa Momento trabalham no departamento de vendas?
**Resultado:** ```10 funcionários```

``` 
db.funcionarios.countDocuments({ cargo: /vendas/i })
```

## 2. Inclua suas próprias informações no departamento de Tecnologia da empresa.
**Resultado** ```Inserido```

```
db.funcionarios.insertOne ({
nome : 'Kawan Barbosa Turchiai',
telefone : '11 95113-5113',
Cargo : 'Mobile Developer',
salario : 27000,
departamento : ObjectId("85992103f9b3e0b3b3c1fe74")
})
```

## 3. quantos funcionários temos ao total na empresa?
**Resultado** ```24 Funcionários```

```
db.funcionarios.countDocuments ({})
* E quanto ao Departamento de Tecnologia?
6 funcionários

db.funcionarios.countDocuments ({departamento: ObjectId('85992103f9b3e0b3b3c1fe74')})
* Qual a média salarial do departamento de tecnologia?
A média é 8.300

db.funcionarios.aggregate([
  { $match: { departamento: ObjectId("85992103f9b3e0b3b3c1fe74") } },
  { $group: { _id: "$departamento", media: { $avg: "$salario" } } }
])
```
## 4. Quantos funcionários estão no Departamento de Tecnologia?</h2>
**Resultado** ```6 funcionários```

```
db.funcionarios.countDocuments({
departamento: ObjectId('85992103f9b3e0b3b3c1fe74')})
```

## 5. Qual a média salarial do departamento de Tecnologia?
**Resultado** ```A soma dos salários de 5 funcionários é 22800```

```
db.funcionarios.aggregate([{
$match:{departamento: ObjectId('85992103f9b3e0b3b3c1fe74')}},
{$group:{_id: 0 ,
soma_salario: {$sum: "$salario"},
somafun: {$sum:1}}}])
```
  
## 6. Quanto o departamento de Vendas gasta em salários?
**Resultado** ```61100```

```
db.funcionarios.aggregate([
  { $match: { departamento: ObjectId("5992103f9b3e0b3b3c1e3e3f") } },
  { $group: { _id: "$departamento", TotalSalario: { $sum: "$salario" } } }
])
```

## 7. Um novo departamento foi criado: Inovações
### O departamento de Inovações será locado no Brasil. Incluindo-o no banco de dados da empresa:
**Resultado** ```Inserido```

```
db.departamentos.insertOne({
'nome':'inovações',
'escritorio':ObjectId()
})
``````

## 8. Inclua alguns colegas de turma no Departamento de Inovações.
**Resultado** ```Inserido```
```
db.funcionarios.insertMany([{
'nome':'Gustavo Correia',
'telefone':'11 99999998',
'email':'Gustavocorreia10@gmail.com',
'cargo': 'devops',
'salario':'35000',
'departamento':ObjectId('66fae0d1d9a9e8ffbb9fac8c')
}])

db.funcionarios.insertMany([{
'nome':'Lucas Miranda',
'telefone':'11 25619932',
'email':'miranda555@hotmail.com',
'cargo': 'frontend',
'salario':'5000',
'departamento':ObjectId('66fae0d1d9a9e8ffbb9fac8c')
}])
```

## 9. Quantos funcionários a empresa Momento tem agora?</h2>
**Resultado** ```A empresa está com 27 funcionários.```

```
db.funcionarios.countDocuments()
```

## 10. Quantos funcionários da empresa possuem cônjuges?</h2>
**Resultado** ```7 funcionários possuem cônjuges.```
```
db.funcionarios.countDocuments({
"dependentes.conjuge":{$exists: true}})
```

## 11. Qual a média salarial dos funcionários da empresa, excluindo-se o CEO?
**Resultado** ```Resultado: 8587.2```
```
db.funcionarios.aggregate([{
$match:{cargo:{$ne:'CEO'}}},
{$group:{_id: 0 ,soma_salario:
{$sum: "$salario"},
somafun: {$sum:1}}},
{$project:{_id: null,calculo:
{$divide:['$soma_salario',
'$somafun'] }}}])
```


## 12. Qual o departamento com a maior média salarial?

**Resultado** ```O departamento com a maior média salarial é o Executivo. Resultado: 71000 ```
 ```
db.funcionarios.aggregate([{
$group:{ _id: '$departamento',
contagem: {$sum:1},
salario_contagem:{$sum:'$salario'}}},
{$project:{calculo:{$divide:['$salario_contagem','$contagem']}}},
{$sort:{"calculo":-1}}])
```


## 13. Qual o departamento com o menor número de funcionários?

**Resultado** ```O departamento Executivo consta apenas com uma pessoa.```

```
db.funcionarios.aggregate([{$group:{ _id: '$departamento',
contagem: {$sum:1}}},
{$sort:{"contagem":1}},
{$limit:1}])
```

## 14. Qual o produto mais valioso da empresa?
**Resultado** ```Sabre de Luz (Mace Windu), Preço Unitário: 990.29```
```
db.vendas.aggregate([{
$sort:{quantidade:1}},
{$sort:{precoUnitario:-1}}])
```


## 15. Qual o produto mais vendido da empresa?</h2>
**Resultado** ``` Uniforme de Moléculas Instáveis, Quantidade: 10 ```
```
db.vendas.aggregate([{
$sort:{quantidade:-1}},
{$limit:1}])
```

