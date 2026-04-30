respostas exercicio aula 09



use loja_virtual

db.produtos.insertOne({
  nome: "Smartphone Galaxy A15",
  categoria: "Eletronicos",
  preco: 1299.90,
  marca: "Samsung"
})


db.produtos.insertMany([
  {
    nome: "Livro MongoDB na Pratica",
    categoria: "Livros",
    preco: 79.90,
    autor: "Joao Silva"
  },
  {
    nome: "Camiseta Basica",
    categoria: "Roupas",
    preco: 49.90,
    tamanho: "M",
    cor: "Preta"
  }
])

db.produtos.find()


db.produtos.find().pretty()

db.produtos.find({ categoria: "Livros" })

db.produtos.find({ preco: { $gt: 100 } })


db.produtos.updateOne(
  { nome: "Smartphone Galaxy A15" },
  { $set: { preco: 1199.90 } }
)

db.produtos.updateMany(
  {},
  { $set: { estoque: 10 } }
)

db.produtos.find().pretty()

db.produtos.createIndex({ nome: 1 })


db.produtos.createIndex({ categoria: 1, preco: -1 })

db.produtos.getIndexes()


db.produtos.find()


db.produtos.find({ preco: { $gt: 100 } })

db.produtos.find({ categoria: "Eletronicos" })

db.produtos.find({}, { nome: 1, preco: 1, _id: 0 })


db.produtos.updateOne(
  { nome: "Smartphone Galaxy A15" },
  { $set: { preco: 1199.90 } }
)


db.produtos.updateMany(
  {},
  { $set: { estoque: 10 } }
)


db.produtos.updateMany(
  { categoria: "Roupas" },
  { $set: { promocao: true } }
)


db.produtos.deleteOne({ nome: "MongoDB na Pratica" })

db.produtos.find()

db.produtos.deleteOne({ nome: "Camiseta Basica" })

db.produtos.deleteMany({ categoria: "Roupas" })

db.produtos.find()

db.produtos.deleteMany({ categoria: "Calcados" })