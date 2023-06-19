<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tabela de Contratos</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f2f2f2;
        }

        h1 {
            text-align: center;
            margin-top: 20px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background-color: #fff;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        th, td {
            padding: 10px;
            text-align: left;
        }

        th {
            background-color: #333;
            color: #fff;
        }

        td {
            border-bottom: 1px solid #ddd;
        }

        .delete-button {
            background-color: #ff5050;
            color: #fff;
            border: none;
            padding: 5px 10px;
            border-radius: 3px;
            cursor: pointer;
        }

        .edit-button {
            background-color: #00cc66;
            color: #fff;
            border: none;
            padding: 5px 10px;
            border-radius: 3px;
            cursor: pointer;
        }

        .add-button {
            background-color: #3399ff;
            color: #fff;
            border: none;
            padding: 5px 10px;
            border-radius: 3px;
            cursor: pointer;
        }

        .upload-button {
            background-color: #ff9933;
            color: #fff;
            border: none;
            padding: 5px 10px;
            border-radius: 3px;
            cursor: pointer;
        }

        .download-button {
            background-color: #6666ff;
            color: #fff;
            border: none;
            padding: 5px 10px;
            border-radius: 3px;
            cursor: pointer;
        }

        .calculator {
            margin-top: 20px;
            padding: 10px;
            background-color: #fff;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        .calculator label {
            display: block;
            margin-bottom: 5px;
        }

        .calculator input[type="number"] {
            width: 100px;
            padding: 5px;
        }

        .calculator select {
            padding: 5px;
        }

        .calculator button {
            margin-top: 10px;
            background-color: #009933;
            color: #fff;
            border: none;
            padding: 5px 10px;
            border-radius: 3px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h1>Tabela de Contratos</h1>

    <table>
        <thead>
            <tr>
                <th>Nº CONTRATO</th>
                <th>Nº PROCESSO</th>
                <th>EMPRESA CONTRATADA</th>
                <th>OBJETO</th>
                <th>Nº EMPENHO</th>
                <th>SITUAÇÃO</th>
                <th>VALOR R$</th>
                <th>ID CONTRATAÇÃO</th>
                <th>DATA DA ASSINATURA</th>
                <th>INÍCIO DA VIGÊNCIA</th>
                <th>FIM DA VIGÊNCIA</th>
                <th></th>
            </tr>
        </thead>
        <tbody id="contract-table-body">
            <!-- Aqui serão adicionadas as linhas da tabela de contratos -->
        </tbody>
    </table>

    <div class="calculator">
        <h2>Calculadora de Vigência</h2>
        <label for="start-date">Data de Assinatura:</label>
        <input type="date" id="start-date">
        <label for="vigency-value">Valor da Vigência:</label>
        <input type="number" id="vigency-value" min="1" step="1">
        <select id="vigency-unit">
            <option value="days">Dias</option>
            <option value="months">Meses</option>
        </select>
        <button onclick="calculateEndDate()">Calcular Fim da Vigência</button>
        <p id="result-vigency"></p>
    </div>

    <div class="upload-download-buttons">
        <h2>Upload e Download de Arquivo PDF</h2>
        <input type="file" id="upload-pdf">
        <button onclick="uploadPDF()">Upload PDF</button>
     
    </div>

    <div class="add-contract">
        <h2>Adicionar Informações de Contrato</h2>
        <label for="contract-number">Nº Contrato:</label>
        <input type="text" id="contract-number">
        <label for="process-number">Nº Processo:</label>
        <input type="text" id="process-number">
        <label for="contracted-company">Empresa Contratada:</label>
        <input type="text" id="contracted-company">
        <label for="contract-object">Objeto:</label>
        <input type="text" id="contract-object">
        <label for="commitment-number">Nº Empenho:</label>
        <input type="text" id="commitment-number">
        <label for="situation">Situação:</label>
        <input type="text" id="situation">
        <label for="contract-value">Valor R$:</label>
        <input type="text" id="contract-value">
        <label for="contract-id">ID Contratação:</label>
        <input type="text" id="contract-id">
        <label for="contract-date">Data de Assinatura:</label>
        <input type="date" id="contract-date">
        <label for="start-vigency-date">Início da Vigência:</label>
        <input type="date" id="start-vigency-date">
        <label for="end-vigency-date">Fim da Vigência:</label>
        <input type="date" id="end-vigency-date">
        <button onclick="addContract()">Adicionar Contrato</button>
    </div>

    <script>
        // Função para adicionar um contrato à tabela
        function addContract() {
            var contractTableBody = document.getElementById("contract-table-body");
            var newRow = document.createElement("tr");

            var contractNumber = document.createElement("td");
            contractNumber.textContent = document.getElementById("contract-number").value;

            var processNumber = document.createElement("td");
            processNumber.textContent = document.getElementById("process-number").value;

            var contractedCompany = document.createElement("td");
            contractedCompany.textContent = document.getElementById("contracted-company").value;

            var contractObject = document.createElement("td");
            contractObject.textContent = document.getElementById("contract-object").value;

            var commitmentNumber = document.createElement("td");
            commitmentNumber.textContent = document.getElementById("commitment-number").value;

            var situation = document.createElement("td");
            situation.textContent = document.getElementById("situation").value;

            var contractValue = document.createElement("td");
            contractValue.textContent = document.getElementById("contract-value").value;

            var contractID = document.createElement("td");
            contractID.textContent = document.getElementById("contract-id").value;

            var contractDate = document.createElement("td");
            contractDate.textContent = document.getElementById("contract-date").value;

            var startVigencyDate = document.createElement("td");
            startVigencyDate.textContent = document.getElementById("start-vigency-date").value;

            var endVigencyDate = document.createElement("td");
            endVigencyDate.textContent = document.getElementById("end-vigency-date").value;

            var deleteButton = document.createElement("td");
            var deleteButtonElement = document.createElement("button");
            deleteButtonElement.textContent = "Deletar";
            deleteButtonElement.classList.add("delete-button");
            deleteButtonElement.onclick = function() {
                deleteContract(this);
            };
            deleteButton.appendChild(deleteButtonElement);

            var editButton = document.createElement("td");
            var editButtonElement = document.createElement("button");
            editButtonElement.textContent = "Editar";
            editButtonElement.classList.add("edit-button");
            editButtonElement.onclick = function() {
                editContract(this);
            };
            editButton.appendChild(editButtonElement);

            newRow.appendChild(contractNumber);
            newRow.appendChild(processNumber);
            newRow.appendChild(contractedCompany);
            newRow.appendChild(contractObject);
            newRow.appendChild(commitmentNumber);
            newRow.appendChild(situation);
            newRow.appendChild(contractValue);
            newRow.appendChild(contractID);
            newRow.appendChild(contractDate);
            newRow.appendChild(startVigencyDate);
            newRow.appendChild(endVigencyDate);
            newRow.appendChild(deleteButton);
            newRow.appendChild(editButton);

            contractTableBody.appendChild(newRow);

            // Limpar os campos de entrada de dados após adicionar o contrato
            document.getElementById("contract-number").value = "";
            document.getElementById("process-number").value = "";
            document.getElementById("contracted-company").value = "";
            document.getElementById("contract-object").value = "";
            document.getElementById("commitment-number").value = "";
            document.getElementById("situation").value = "";
            document.getElementById("contract-value").value = "";
            document.getElementById("contract-id").value = "";
            document.getElementById("contract-date").value = "";
            document.getElementById("start-vigency-date").value = "";
            document.getElementById("end-vigency-date").value = "";
        }

        // Função para deletar um contrato da tabela
        function deleteContract(button) {
            var row = button.parentNode.parentNode;
            row.parentNode.removeChild(row);
        }

        // Função para editar as informações de um contrato
        function editContract(button) {
            var row = button.parentNode.parentNode;
            var cells = row.getElementsByTagName("td");
            var editMode = true;

            for (var i = 0; i < cells.length - 2; i++) {
                var cell = cells[i];
                var cellValue = cell.textContent;
                cell.innerHTML = "<input type='text' value='" + cellValue + "'>";
            }

            var saveButton = document.createElement("button");
            saveButton.textContent = "Salvar";
            saveButton.classList.add("edit-button");
            saveButton.onclick = function() {
                saveContract(this);
            };

            var cancelButton = document.createElement("button");
            cancelButton.textContent = "Cancelar";
            cancelButton.classList.add("delete-button");
            cancelButton.onclick = function() {
                cancelEdit(this);
            };

            var editButtonCell = cells[cells.length - 2];
            editButtonCell.innerHTML = "";
            editButtonCell.appendChild(saveButton);
            editButtonCell.appendChild(cancelButton);
        }

        // Função para salvar as alterações em um contrato
        function saveContract(button) {
            var row = button.parentNode.parentNode;
            var cells = row.getElementsByTagName("td");

            for (var i = 0; i < cells.length - 2; i++) {
                var cell = cells[i];
                var inputValue = cell.getElementsByTagName("input")[0].value;
                cell.textContent = inputValue;
            }

            var editButtonCell = cells[cells.length - 2];
            editButtonCell.innerHTML = "";
            var editButtonElement = document.createElement("button");
            editButtonElement.textContent = "Editar";
            editButtonElement.classList.add("edit-button");
            editButtonElement.onclick = function() {
                editContract(this);
            };
            editButtonCell.appendChild(editButtonElement);
        }

        // Função para cancelar a edição de um contrato
        function cancelEdit(button) {
            var row = button.parentNode.parentNode;
            var cells = row.getElementsByTagName("td");
            var editMode = false;

            for (var i = 0; i < cells.length - 2; i++) {
                var cell = cells[i];
                var inputValue = cell.getElementsByTagName("input")[0].value;
                cell.textContent = inputValue;
            }

            var editButtonCell = cells[cells.length - 2];
            editButtonCell.innerHTML = "";
            var editButtonElement = document.createElement("button");
            editButtonElement.textContent = "Editar";
            editButtonElement.classList.add("edit-button");
            editButtonElement.onclick = function() {
                editContract(this);
            };
            editButtonCell.appendChild(editButtonElement);
        }

        // Função para calcular a data de término da vigência
        function calculateEndDate() {
            var startDate = new Date(document.getElementById("start-date").value);
            var vigencyValue = parseInt(document.getElementById("vigency-value").value);
            var vigencyUnit = document.getElementById("vigency-unit").value;

            if (vigencyUnit === "days") {
                startDate.setDate(startDate.getDate() + vigencyValue);
            } else if (vigencyUnit === "months") {
                startDate.setMonth(startDate.getMonth() + vigencyValue);
            }

            var endDateString = startDate.toISOString().substring(0, 10);
            document.getElementById("result-vigency").textContent = "Fim da Vigência: " + endDateString;
        }

        // Função para realizar o upload de um arquivo PDF
        function uploadPDF() {
            var uploadInput = document.getElementById("upload-pdf");
            var file = uploadInput.files[0];
            var downloadLink = document.getElementById("download-pdf");

            if (file) {
                var fileURL = URL.createObjectURL(file);
                downloadLink.href = fileURL;
                downloadLink.style.display = "inline-block";
            }
        }

        // Função para realizar o download do arquivo PDF
        function downloadPDF() {
            var downloadLink = document.getElementById("download-pdf");
            downloadLink.click();
        }
    </script>
</body>
</html>
