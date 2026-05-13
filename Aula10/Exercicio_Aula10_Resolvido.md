# Exercício Prático: Modelagem e Consultas em MongoDB - RESOLVIDO

## Parte 1: Modelagem de Dados

### 1.1 - Incorporação (Embedding)

**Comando executado:**
```javascript
db.cursos.insertOne({
  nome: "Introdução ao JavaScript",
  instrutor: "João Silva",
  descricao: "Aprenda os fundamentos de JavaScript",
  modulos: [
    {
      nome: "Fundamentos",
      carga_horaria: 10
    },
    {
      nome: "DOM e Eventos",
      carga_horaria: 8
    },
    {
      nome: "Async/Await",
      carga_horaria: 6
    }
  ]
})
Resposta - Em que situação é melhor referenciar?

✅ Quando um instrutor ministra MUITOS cursos (evita duplicação de dados) ✅ Quando os dados do instrutor mudam frequentemente (atualiza em um único lugar) ✅ Para economizar espaço em armazenamento ✅ Exemplo: Se "Maria Santos" ministra 50 cursos, é melhor ter 1 documento de instrutor do que copiar seus dados 50 vezes

db.clientes.find({ email: { $exists: true } })
[
  {
    _id: ObjectId('6a04c67851058f0e7144ba8b'),
    nome: 'Ana',
    idade: 25,
    cidade: 'São Paulo',
    email: 'ana@email.com'
  },
  {
    _id: ObjectId('6a04c67851058f0e7144ba8c'),
    nome: 'Bruno',
    idade: 30,
    cidade: 'Rio de Janeiro',
    email: 'bruno@email.com'
  },
  {
    _id: ObjectId('6a04c67851058f0e7144ba8e'),
    nome: 'Diana',
    idade: 28,
    cidade: 'Campinas',
    email: 'diana@email.com'
  },
  {
    _id: ObjectId('6a04c67851058f0e7144ba8f'),
    nome: 'Eduardo',
    idade: 35,
    cidade: 'São Paulo',
    email: 'edu@email.com'
  }
]
Observação: Carlos não apareceu porque não possui o campo email.


db.clientes.find({ idade: { $gte: 21 } })
[
  {
    _id: ObjectId('6a04c67851058f0e7144ba8b'),
    nome: 'Ana',
    idade: 25,
    cidade: 'São Paulo',
    email: 'ana@email.com'
  },
  {
    _id: ObjectId('6a04c67851058f0e7144ba8c'),
    nome: 'Bruno',
    idade: 30,
    cidade: 'Rio de Janeiro',
    email: 'bruno@email.com'
  },
  {
    _id: ObjectId('6a04c67851058f0e7144ba8d'),
    nome: 'Carlos',
    idade: 22,
    cidade: 'São Paulo'
  },
  {
    _id: ObjectId('6a04c67851058f0e7144ba8e'),
    nome: 'Diana',
    idade: 28,
    cidade: 'Campinas',
    email: 'diana@email.com'
  },
  {
    _id: ObjectId('6a04c67851058f0e7144ba8f'),
    nome: 'Eduardo',
    idade: 35,
    cidade: 'São Paulo',
    email: 'edu@email.com'
  }
]

db.clientes.find({ cidade: "São Paulo", idade: { $lt: 30 } })

[
  {
    _id: ObjectId('6a04c67851058f0e7144ba8b'),
    nome: 'Ana',
    idade: 25,
    cidade: 'São Paulo',
    email: 'ana@email.com'
  },
  {
    _id: ObjectId('6a04c67851058f0e7144ba8d'),
    nome: 'Carlos',
    idade: 22,
    cidade: 'São Paulo'
  }
]
Observação: Apenas Ana e Carlos atendem aos critérios (moram em São Paulo E têm menos de 30 anos).

db.vendas.aggregate([
  {
    $match: {
      status: "concluída"
    }
  },
  {
    $group: {
      _id: "$categoria",
      quantidade_total: { $sum: "$quantidade" },
      valor_total: { $sum: { $multiply: ["$quantidade", "$preco_unitario"] } },
      numero_vendas: { $sum: 1 }
    }
  },
  {
    $sort: {
      quantidade_total: -1
    }
  }
])

[
  {
    _id: 'Cabos',
    quantidade_total: 20,
    valor_total: 500,
    numero_vendas: 2
  },
  {
    _id: 'Periféricos',
    quantidade_total: 16,
    valor_total: 1700,
    numero_vendas: 4
  },
  {
    _id: 'Monitores',
    quantidade_total: 6,
    valor_total: 8400,
    numero_vendas: 4
  }
]

Explicação do Resultado:

Cabos: 20 unidades vendidas, valor total R$ 500,00 (2 transações)
Periféricos: 16 unidades vendidas, valor total R$ 1.700,00 (4 transações)
Monitores: 6 unidades vendidas, valor total R$ 8.400,00 (4 transações)
Os resultados estão ordenados por quantidade decrescente (Cabos > Periféricos > Monitores).



Conceito	Significado	Uso
$exists	Verifica existência de campo	Filtrar documentos que têm/não têm um campo
$gte	Maior ou igual (≥)	Comparar valores numéricos
$lt	Menor que (<)	Comparar valores numéricos
$match	Filtrar documentos	Primeira etapa de agregação (como WHERE)
$group	Agrupar dados	Segunda etapa de agregação (como GROUP BY)
$sum	Somar valores	Calcular totais em agregação
$multiply	Multiplicar valores	Calcular valor total (quantidade × preço)
$sort	Ordenar resultados	Organizar dados em ordem crescente/decrescente
Data de Conclusão: 13 de maio de 2026

