// Aula prática: CRUD no MongoDB com mongosh
// Banco: loja_virtual
// Coleção: produtos

// 1) Selecionar/criar o banco de dados loja_virtual
use loja_virtual

// 2) Inserir produtos
db.produtos.insertOne({
  nome: "Smartphone Galaxy A15",
  categoria: "Eletronicos",
  preco: 1299.90,
  marca: "Samsung",
  armazenamento: "128GB",
  cor: "Azul"
})

db.produtos.insertMany([
  {
    nome: "MongoDB na Pratica",
    categoria: "Livros",
    preco: 79.90,
    autor: "Joao Silva",
    editora: "Tech Books",
    paginas: 320
  },
  {
    nome: "Camiseta Basica",
    categoria: "Roupas",
    preco: 49.90,
    tamanho: "M",
    cor: "Preta",
    material: "Algodao"
  }
])

// 3) Consultas
// 3.1 listar todos os produtos
db.produtos.find().pretty()

// 3.2 buscar produtos com preco superior a 100
db.produtos.find({ preco: { $gt: 100 } }).pretty()

// 3.3 listar produtos da categoria Eletronicos
db.produtos.find({ categoria: "Eletronicos" }).pretty()

// 3.4 buscar apenas nome e preco
db.produtos.find({}, { nome: 1, preco: 1, _id: 0 }).pretty()

// 4) Atualizações
// 4.1 atualizar preço de um produto específico
db.produtos.updateOne(
  { nome: "Smartphone Galaxy A15" },
  { $set: { preco: 1199.90 } }
)

// 4.2 adicionar campo estoque para todos os produtos
db.produtos.updateMany(
  {},
  { $set: { estoque: 50 } }
)

// 4.3 marcar roupas em promoção
db.produtos.updateMany(
  { categoria: "Roupas" },
  { $set: { promocao: true } }
)

// 5) Exclusões
// 5.1 remover um produto específico
db.produtos.deleteOne({ nome: "MongoDB na Pratica" })

// 5.2 remover todos os produtos da categoria Calcados
db.produtos.deleteMany({ categoria: "Calcados" })
