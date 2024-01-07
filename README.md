Desenvolver um sistema de cadastro de produtos com operações CRUD (Create, Read, Update, Delete) em um site de roupas envolve uma combinação de HTML, CSS e JavaScript no lado do cliente, e uma linguagem de servidor (como PHP, Node.js, etc.) para lidar com as operações no banco de dados. Aqui está um exemplo simples usando HTML, CSS e JavaScript no cliente e PHP no servidor:

HTML (index.html)
html
Copy code
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="styles.css">
  <title>Cadastro de Produtos</title>
</head>
<body>
  <h1>Cadastro de Produtos</h1>

  <div id="product-form">
    <label for="productName">Nome do Produto:</label>
    <input type="text" id="productName" required>

    <label for="productPrice">Preço:</label>
    <input type="number" id="productPrice" required>

    <button onclick="addProduct()">Adicionar Produto</button>
  </div>

  <div id="product-list"></div>

  <script src="script.js"></script>
</body>
</html>
CSS (styles.css)
css
Copy code
body {
  font-family: Arial, sans-serif;
  margin: 20px;
}

#product-form {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input, button {
  margin-bottom: 10px;
}
JavaScript (script.js)
javascript
Copy code
document.addEventListener('DOMContentLoaded', function () {
  // Carregar produtos existentes na página carregamento
  loadProducts();

  // Adicionar um produto
  window.addProduct = function () {
    const name = document.getElementById('productName').value;
    const price = document.getElementById('productPrice').value;

    if (name && price) {
      // Enviar dados para o servidor (usando AJAX ou Fetch API)
      // Aqui, suponha que você está usando uma função PHP chamada addProduct.php
      fetch('addProduct.php', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ name, price }),
      })
      .then(response => response.json())
      .then(data => {
        if (data.success) {
          loadProducts(); // Recarregar a lista de produtos
        } else {
          alert('Erro ao adicionar o produto.');
        }
      })
      .catch(error => console.error('Erro:', error));
    }
  };

  // Carregar produtos existentes
  function loadProducts() {
    // Aqui, você faria uma solicitação ao servidor para obter a lista de produtos
    // Suponha que você tenha uma função PHP chamada getProducts.php
    fetch('getProducts.php')
      .then(response => response.json())
      .then(products => displayProducts(products))
      .catch(error => console.error('Erro:', error));
  }

  // Exibir produtos na página
  function displayProducts(products) {
    const productListDiv = document.getElementById('product-list');
    productListDiv.innerHTML = ''; // Limpar lista antes de atualizar

    products.forEach(product => {
      const productDiv = document.createElement('div');
      productDiv.innerHTML = `
        <p><strong>${product.name}</strong> - R$ ${product.price}</p>
        <button onclick="deleteProduct(${product.id})">Excluir</button>
      `;
      productListDiv.appendChild(productDiv);
    });
  }

  // Excluir um produto
  window.deleteProduct = function (productId) {
    // Enviar dados para o servidor (usando AJAX ou Fetch API)
    // Aqui, suponha que você está usando uma função PHP chamada deleteProduct.php
    fetch('deleteProduct.php', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ id: productId }),
    })
    .then(response => response.json())
    .then(data => {
      if (data.success) {
        loadProducts(); // Recarregar a lista de produtos
      } else {
        alert('Erro ao excluir o produto.');
      }
    })
    .catch(error => console.error('Erro:', error));
  };
});
Este é apenas um exemplo básico e genérico. Certifique-se de adaptar o código conforme necessário para atender aos requisitos específicos do seu projeto, especialmente nas operações do servidor (adicionar, obter, excluir produtos).
