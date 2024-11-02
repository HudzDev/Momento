## Quantos funcionarios da empresa Momento trabalham no departamento de vendas?
 
<pre>R: 10</pre>
 
<pre>db.funcionarios.countDocuments({departamento: ObjectId("85992103f9b3e0b3b3c1fe71") })</pre>
 
## Inclua suas próprias informações no departamento de Tecnologia da empresa.
 
<pre>db.funcionarios.insertOne({ 
  nome: 'Hudson de Souza', 
  telefone: '(011) 00000-0000', 
  email: 'hudsonsouza@proa', 
  dataAdmissao: '2024-09-24', 
  cargo: 'Web Developer', 
  salario: 20000, 
  departamento: ObjectId('85992103f9b3e0b3b3c1fe74') })</pre>
 
## Agora diga, quantos funcionários temos ao total na empresa?
 
<pre>R: 24</pre>
 
<pre>db.funcionarios.countDocuments()</pre>
 
## E quanto ao Departamento de Tecnologia?
 
<pre>R: 6</pre>
 
<pre>db.funcionarios.countDocuments({departamento: ObjectId("85992103f9b3e0b3b3c1fe74") })</pre>
 
## Qual a média salarial do departamento de tecnologia?
 
<pre>R: 7.133</pre>
 
<pre>db.funcionarios.aggregate([ 
{ $match: {departamento: ObjectId("85992103f9b3e0b3b3c1fe74")} }, 
{ $group: 
{ _id: null, 
  totalSalarios: {$sum: "$salario"}, 
  totalFuncionarios: {$sum: 1}} 
}, 
{ $project: 
{ _id: 0, 
  totalSalarios: 1, 
  mediaSalarios: { $divide: ["$totalSalarios", "$totalFuncionarios"] }} 
} 
])</pre>
 
## Quanto o departamento de Vendas gasta em salários?
 
<pre>R: 95.100</pre>
 
<pre>db.funcionarios.aggregate([ 
{ $match: {departamento: ObjectId("85992103f9b3e0b3b3c1fe71")} },
{ $group: {_id: null, 
totalSalarios: {$sum: "$salario"}} } ]) </pre>
 
## Um novo departamento foi criado. O departamento de Inovações. Ele será locado no Brasil. Por favor, adicione-o no banco de dados da empresa colocando quaisquer informações que você achar relevantes.
 
<pre>db.escritorios.insertOne( 
{ nome: "Titanium Mind Office", 
  endereco: "Avenida Paulista", 
  telefone: "+55 988888888", 
  pais: "BR", 
  suprimentos: 
[ { 
  produto: "PCs Gamers", 
  quantidade: 5, 
  precoUnitario: 250.000 
}, 
{ 
  produto: "Impressoras", 
  quantidade: 3, 
  precoUnitario: 3.000 
},  
{ 
  produto: "Cafeteira", 
  quantidade: 2, 
  precoUnitario: 550 
}, 
{ 
  produto: "Lousa Digital", 
  quantidade: 1, 
  precoUnitario: 10.000 
}, 
{ 
  produto: "Projetor", 
  quantidade: 1, 
  precoUnitario: 5.000 
} ] } </pre>

<pre>db.departamentos.insertOne({
nome: "Inovacoes",
escritorio: ObjectId ("66f34452b4ce25097d7800ce") })</pre>

## O departamento de Inovações está sem funcionários. Inclua alguns colegas de turma nesse departamento.

<pre>db.funcionarios.insertMany([
{ nome: "Maykon Silva",
  telefone: "999999991",
  email: "maykonsilva@proa",
  dataAdmissao: "2024-09-24",
  cargo: "Back-End",
  salario: 20000,
  departamento: ObjectId("66f2d06d29e51cd5c5853984")
},
{ nome: "Matheus Oliveira",
  telefone: "999999992",
  email: "matheusoliveira@proa",
  dataAdmissao: "2024-09-24",
  cargo: "Full-Stack",
  salario: 5,
  departamento: ObjectId("66f2d06d29e51cd5c5853984")
},
{ nome: "Murilo Coelho",
  telefone: "999999993",
  email: "murilocoelho@proa",
  dataAdmissao: "2024-09-24",
  cargo: "P.O",
  salario: 25000,
  departamento: ObjectId("66f2d06d29e51cd5c5853984")
}
])</pre>
 
## Quantos funcionarios a empresa Momento tem agora?
 
<pre>R: 27</pre>

<pre>db.funcionarios.countDocuments()</pre>
 
## Quantos funcionários da empresa Momento possuem conjuges?

<pre>R: 7</pre>

<pre>db.funcionarios.countDocuments({ "dependentes.conjuge": { $exists: true } })</pre>
 
## Qual a média salarial dos funcionários da empresa Momento, excluindo-se o CEO?

<pre>R: 10.757</pre>

<pre>db.funcionarios.aggregate([
{ $match: {cargo: { $ne: "CEO" }} },
{ $group: 
{ _id: null,
  totalSalarios: {$sum: "$salario"},
  totalFuncionarios: {$sum: 1}}
},
{ $project: 
{ _id: 0,
  totalSalarios: 1,
  mediaSalarios: { $divide: ["$totalSalarios", "$totalFuncionarios"] }}
}
])</pre>

## Qual a média salarial do departamento de tecnologia?
 
<pre>R: considerando que mudei para o departamento de Inovações a resposta muda para 4560.</pre>

<pre>db.funcionarios.aggregate([
{ $match: {departamento: ObjectId("85992103f9b3e0b3b3c1fe74")} },
{ $group: 
{ _id: null,
  totalSalarios: {$sum: "$salario"},
  totalFuncionarios: {$sum: 1}}
},
{ $project: 
{ _id: 0,
  totalSalarios: 1,
  mediaSalarios: { $divide: ["$totalSalarios", "$totalFuncionarios"] }}
}
])</pre>

## Qual o departamento com a maior média salarial?

<pre>R: com apenas um funcionário, o departamento Executivo tem a maior média salarial de 71 mil</pre>

<pre>db.funcionarios.aggregate([
{ $group: 
{ _id: "$departamento", 
  totalSalarios: { $sum: "$salario" }, 
  totalFuncionarios: { $sum: 1 }} },
{ $project: 
{ departamento: "$_id", 
  _id: 0, 
  totalSalarios: 1, 
  mediaSalarios: { $divide: ["$totalSalarios", "$totalFuncionarios"] }} },
{ $sort: 
{ mediaSalarios: -1 }},
{ $limit: 1 }
])</pre>

## Qual o departamento com o menor número de funcionários?

<pre>R: com o total de 0 funcionários, os departamentos de Marketing, Financeiro e Dados, possuem o menor número de funcionários</pre>

<pre>db.funcionarios.countDocuments({departamento: ObjectId("85992103f9b3e0b3b3c1fe72") })</pre>

<pre>db.funcionarios.countDocuments({departamento: ObjectId("85992103f9b3e0b3b3c1fe73") })</pre>

<pre>db.funcionarios.countDocuments({departamento: ObjectId("85992103f9b3e0b3b3c1fe76") })</pre>

## Pensando na relação quantidade e valor unitario, qual o produto mais valioso da empresa?

<pre>R: o produto mais valioso é o Uniforme do Superman custando R$300</pre>

<pre>db.vendas.aggregate([
{ $sort: { valor: -1 } },
{ $limit: 1 }
])</pre>
 
## Qual o produto mais vendido da empresa?

<pre>R: Laço da Verdade sendo vendido 12 vezes</pre>

<pre>db.vendas.aggregate([
{ $group: 
{ _id: "$produto", 
  totalQuantidadesVendidas: { $sum: "$quantidade" }} },
{ $sort: { totalQuantidadesVendidas: -1 }},
{ $limit: 1 }
])</pre>
 
## Qual o produto menos vendido da empresa?

<pre>R: Uniforme do Superman com 2 vendas</pre>

<pre>db.vendas.aggregate([
{ $group: 
{ _id: "$produto", 
  totalQuantidadesVendidas: { $sum: "$quantidade" }} },
{ $sort: { totalQuantidadesVendidas: +1 }},
{ $limit: 1 }
])</pre>
