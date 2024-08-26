# SHOPIFY Docs

## Autenticação

Autenticação na API segue o seguinte formato

```py
import shopify

shop_url = "SHOP_NAME.myshopify.com" # quickstart-0e80e1d5.myshopify.com
api_version = '2024-07'

session = shopify.Session(shop_url, api_version, ACCESS_TOKEN)
shopify.ShopifyResource.activate_session(session)

...
# Code Here
...

shopify.ShopifyResource.clear_session()
```

Também é possivel criar Sessões temporarias utilizando WITH:

```py
with shopify.Session.temp(shop_url, api_version, ACCESS_TOKEN):
    # Code here
```

## Como funciona?

A libraria da [Shopify para Python](https://github.com/Shopify/shopify_python_api?tab=readme-ov-file#getting-started) é orientada a objetos, você pode criar, atualizar, procurar e deletar objetos dentro da loja utilizando Classes e Objetos
`<br>`
[Todas as Classes e atributos](https://shopify.dev/docs/api/admin-rest/2024-07/resources/product)

> [!IMPORTANT]
> A Livraria parece ainda não suportar Asyncs e conecções persistentes

## GET

```py
products = shopify.Product.find() # Pega todos os produtos
```
```py
product = shopify.Product.find(PRODUCT_ID) # pega as informações do produto com id PRODUCT_ID
```
```py
products = shopify.Product.find(ids="12312321,321332332") # Pega os dois produtos com Ids 12312321 e 321332332
```
Todos os filtros estão dentro da [documentação](https://shopify.dev/docs/api/admin-rest/2024-07/resources/product#get-products?ids=632910392,921728736)

## POST

```py
product = shopify.Product() # Criação do objeto Product
product.title = "Produto Teste" # Nome do produto
product.save() # POST do produto
product.id # 123323123123

image = shopify.Image(dict(product_id=product.id)) # Criação do objeto Image e vinculo ao produto
image.src = "URL" # URL da imagem a ser colocada
image.save() # Salvamento da Imagem dentro do produto
```

Também é possivel salvar vários objetos vinculados

```py
img1 = shopify.Image() # Criação do primeiro objeto Image
img1.src = "URL1"

img2 = shopify.Image() # Criação do segundo objeto Image
img2.src = "URL2"

product = shopify.Product() # Criação do objeto Product
product.title = "Produto Teste Imagens"
product.images = [img1, img2] # Vinculo dos objetos Image com Product
product.save() # Salva o produto junto com os objetos Image
```

## UPDATE

```py
product = shopify.Product() # Cria objeto product

product.id = 8058206552246 # Vincula o ID do produto com o do produto 8058206552246
product.title = "Nome Atualizado" # Muda o nome do produto

product.save() # Salva as novas informações do produto e não altera as não especificadas
```

Há também outro jeito de pegar o produto a ser atualizado utilizando um GET

```py
product = shopify.Product.find(8058206552246) # Já pega o produto com ID 8058206552246 e suas informações

product.title = "Nome Atualizado" # Muda o nome do produto

product.save() # Salva as novas informações do produto e não altera as não especificadas
```

## DELETE

```py
product = shopify.Product() # Cria objeto product
product.id = 8058206552246 # Vincula o ID do produto com o do produto 8058206552246

product.destroy() # Deleta o produto
```

Há também outro jeito de pegar o produto a ser atualizado utilizando um GET

```py
product = shopify.Product.find(8058206552246) # Já pega o produto com ID 8058206552246 e suas informações

product.destroy() # Deleta o produto
```
