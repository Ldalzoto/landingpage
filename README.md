<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Landing Page - Nova Visita</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      background-color: #f4f4f4;
    }
    form {
      background-color: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      max-width: 500px;
      margin: auto;
    }
    label, input {
      display: block;
      width: 100%;
      margin-bottom: 10px;
    }
    button {
      background-color: #4CAF50;
      color: white;
      padding: 10px;
      border: none;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <h2>Formulário de Visita</h2>
  
  <form id="visitaForm">
    <label for="nome">Nome Completo:</label>
    <input type="text" id="nome" name="nome" placeholder="" required>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" placeholder="" required>

    <label for="telefone">Telefone:</label>
    <input type="tel" id="telefone" name="telefone" placeholder="" required>

    <button type="button" onclick="enviarFormulario()">Enviar</button>
  </form>

  <script>
    async function enviarFormulario() {
      // Coletar os valores do formulário
      const nome = document.getElementById('nome').value;
      const email = document.getElementById('email').value;
      const telefone = document.getElementById('telefone').value;

      // Criar o objeto no formato JSON
      const visitaData = {
        visita: {
          observacao: "Nova Visita Unidade Padrão",
          pessoa: {
            nome: nome,
            tipoPessoa: "F", // Sempre pessoa física
            email: email,
            contatos: [
              {
                telefone: telefone,
                tipo: "M",  // Tipo de telefone fixo como Móvel
                principal: true
              }
            ]
          },
          procedencia: {
            descricao: "SITE"  // Informação fixa na retaguarda
          }
        }
      };

      try {
        // Fazer a requisição para a API
        const response = await fetch('https://web.foccolojas.com.br/foccolojas/api/comercial/v1/14233/visitas', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJVc3VhcmlvIjoiMzUyMjgiLCJpc3MiOiJGb2NjbyBTaXN0ZW1hcyBkZSBHZXN0YW8iLCJGQUJSSUNBIjoiRk9DQ09MT0pBUyIsImp0aSI6IjA2OTZiYjIwLTYyMjMtNGExYy05ZWJmLWUxNWM3NDM4N2I5YyJ9.oe7gvxeDop2FAnop5YraAgjyvnZrFc2IVgmMxveiBkU'
          },
          body: JSON.stringify(visitaData)
        });

        if (response.ok) {
          const jsonResponse = await response.json();
          alert('Visita registrada com sucesso!');
          console.log(jsonResponse);
        } else {
          alert('Erro ao enviar os dados.');
        }
      } catch (error) {
        console.error('Erro:', error);
        alert('Falha ao conectar com o servidor.');
      }
    }
  </script>

</body>
</html>
