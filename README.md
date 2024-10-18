# Atividade Momento MongoDB

* Quantos funcionarios da empresa Momento trabalham no departamento de vendas? ```10 funcionários```
```
  db.funcionarios.countDocuments ({cargo: /vendas/i})
```

* Inclua suas próprias informações no departamento de Tecnologia da empresa. ```Inserido ```
```
db.funcionarios.insertOne ({
nome : 'Kawan Barbosa Turchiai',
telefone : '11 95113-5113',
Cargo : 'Mobile Developer',
salario : 27000,
departamento : ObjectId("85992103f9b3e0b3b3c1fe74")
})
```

* Agora diga, quantos funcionários temos ao total na empresa? ```24 Funcionários```
```
db.funcionarios.countDocuments ({})
```
* E quanto ao Departamento de Tecnologia? ```6 funcionários```
```
db.funcionarios.countDocuments ({departamento: ObjectId('85992103f9b3e0b3b3c1fe74')})
```

* Qual a média salarial do departamento de tecnologia? ```A média é 8.300```
```
db.funcionarios.aggregate([
  { $match: { departamento: ObjectId("85992103f9b3e0b3b3c1fe74") } },
  { $group: { _id: "$departamento", media: { $avg: "$salario" } } }
])
```

* Quanto o departamento de Vendas gasta em salários? ```61100```
```
db.funcionarios.aggregate([
  { $match: { departamento: ObjectId("5992103f9b3e0b3b3c1e3e3f") } },
  { $group: { _id: "$departamento", TotalSalario: { $sum: "$salario" } } }
])
```

* Um novo departamento foi criado. O departamento de Inovações. 
Ele será locado no Brasil. Por favor, adicione-o no banco de dados da empresa colocando quaisquer informações que você achar relevantes.

* O departamento de Inovações está sem funcionários. Inclua alguns colegas de turma nesse departamento.  

* Quantos funcionarios a empresa Momento tem agora?

* Quantos funcionários da empresa Momento possuem conjuges?

* Qual a média salarial dos funcionários da empresa Momento, excluindo-se o CEO?

* Qual a média salarial do departamento de tecnologia? 

* Qual o departamento com a maior média salarial?

* Qual o departamento com o menor número de funcionários?

* Pensando na relação quantidade e valor unitario, qual o produto mais valioso da empresa?

* Qual o produto mais vendido da empresa?

* Qual o produto menos vendido da empresa?
