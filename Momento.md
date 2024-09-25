# Momento
 
<pre>Vamos fazer algumas perguntas para brincar de análise exploratória de dados com MongoDB.</pre>
 
## Quantos funcionarios da empresa Momento trabalham no departamento de vendas?
 
<pre>R: 10.
 
db.funcionarios.countDocuments({departamento: ObjectId("85992103f9b3e0b3b3c1fe71") })</pre>
 
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
 
<pre>R: 24.
 
db.funcionarios.countDocuments()</pre>
 
## E quanto ao Departamento de Tecnologia?
 
<pre>R: 6.
 
db.funcionarios.countDocuments({departamento: ObjectId("85992103f9b3e0b3b3c1fe74") })</pre>
 
## Qual a média salarial do departamento de tecnologia?
 
<pre>R: 7133.
 
db.funcionarios.aggregate([ 
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
 
<pre>R: 95100.
 
db.funcionarios.aggregate([ 
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
