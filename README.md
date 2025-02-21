<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Controle - Mecânica de Carros</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #eef2f3, #d1d8e0);
            min-height: 100vh;
        }
        h1 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 30px;
            font-size: 2.5em;
            text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.1);
        }
        .container {
            max-width: 900px;
            margin: 40px auto;
            background: #ffffff;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        form {
            display: grid;
            gap: 15px;
            margin-bottom: 30px;
        }
        label {
            color: #34495e;
            font-weight: 600;
            font-size: 1.1em;
        }
        input, textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #dfe6e9;
            border-radius: 8px;
            font-size: 1em;
            transition: border-color 0.3s ease, box-shadow 0.3s ease;
        }
        input:focus, textarea:focus {
            border-color: #0984e3;
            box-shadow: 0 0 8px rgba(9, 132, 227, 0.3);
            outline: none;
        }
        button {
            background: linear-gradient(45deg, #0984e3, #00d2d3);
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            font-size: 1.1em;
            cursor: pointer;
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(9, 132, 227, 0.4);
        }
        button:active {
            transform: translateY(0);
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 30px;
            background: #fff;
            border-radius: 10px;
            overflow: hidden;
        }
        th, td {
            padding: 15px;
            text-align: left;
        }
        th {
            background: linear-gradient(45deg, #2c3e50, #34495e);
            color: white;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        td {
            border-bottom: 1px solid #ecf0f1;
            color: #2d3436;
        }
        tr:nth-child(even) {
            background-color: #f8f9fa;
        }
        tr:hover {
            background-color: #dfe6e9;
            transition: background-color 0.2s ease;
        }
        .search-section {
            display: flex;
            gap: 10px;
            margin: 20px 0;
            align-items: center;
        }
        .search-section label {
            margin: 0;
        }
        .search-section input {
            flex: 1;
        }
        .search-section button {
            background: linear-gradient(45deg, #e17055, #d63031);
        }
        .search-section button:hover {
            box-shadow: 0 5px 15px rgba(214, 48, 49, 0.4);
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Sistema de Controle - Mecânica de Carros</h1>

        <form id="servicoForm">
            <label for="cliente">Nome do Cliente:</label>
            <input type="text" id="cliente" required>
            
            <label for="cpf">CPF (somente números):</label>
            <input type="text" id="cpf" pattern="\d{11}" title="Digite 11 números" required>
            
            <label for="servico">Serviço Prestado:</label>
            <input type="text" id="servico" required>
            
            <label for="valor">Valor Pago (R$):</label>
            <input type="number" id="valor" step="0.01" min="0" required>
            
            <label for="observacoes">Observações:</label>
            <textarea id="observacoes" rows="3"></textarea>
            
            <button type="submit">Cadastrar Serviço</button>
        </form>

        <div class="search-section">
            <label for="buscar">Buscar por Nome ou CPF:</label>
            <input type="text" id="buscar" placeholder="Digite Nome ou CPF">
            <button onclick="buscarServico()">Buscar</button>
        </div>

        <table id="tabelaServicos">
            <thead>
                <tr>
                    <th>Cliente</th>
                    <th>CPF</th>
                    <th>Serviço</th>
                    <th>Valor (R$)</th>
                    <th>Observações</th>
                </tr>
            </thead>
            <tbody id="listaServicos"></tbody>
        </table>
    </div>

    <script>
        let servicos = [];

        function atualizarTabela(filtro = "") {
            const listaServicos = document.getElementById("listaServicos");
            listaServicos.innerHTML = "";
            servicos.filter(s => s.cliente.includes(filtro) || s.cpf.includes(filtro)).forEach(servico => {
                const row = document.createElement("tr");
                row.innerHTML = `
                    <td>${servico.cliente}</td>
                    <td>${servico.cpf}</td>
                    <td>${servico.servico}</td>
                    <td>${servico.valor.toFixed(2)}</td>
                    <td>${servico.observacoes}</td>
                `;
                listaServicos.appendChild(row);
            });
        }

        document.getElementById("servicoForm").addEventListener("submit", function(event) {
            event.preventDefault();
            servicos.push({
                cliente: document.getElementById("cliente").value,
                cpf: document.getElementById("cpf").value,
                servico: document.getElementById("servico").value,
                valor: parseFloat(document.getElementById("valor").value),
                observacoes: document.getElementById("observacoes").value
            });
            atualizarTabela();
            this.reset();
        });

        function buscarServico() {
            atualizarTabela(document.getElementById("buscar").value);
        }
    </script>
</body>
</html>
