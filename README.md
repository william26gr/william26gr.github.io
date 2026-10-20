<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Calculadora de Propinas</title>
  <style>
    body { font-family: sans-serif; max-width: 400px; margin: 40px auto; padding: 20px; border: 1px solid #ccc; border-radius: 8px; }
    input, button { width: 100%; padding: 10px; margin-top: 10px; box-sizing: border-box; }
    button { background-color: #2ea44f; color: white; border: none; font-weight: bold; cursor: pointer; }
    #resultado { margin-top: 20px; font-weight: bold; color: #0969da; }
  </style>
</head>
<body>

  <h2>💰 Calculadora de Propinas</h2>
  <label for="total">Total de la cuenta (€):</label>
  <input type="number" id="total" placeholder="Ej: 50">

  <label for="porcentaje">Porcentaje de propina (%):</label>
  <input type="number" id="porcentaje" value="10">

  <button onclick="calcularPropina()">Calcular Total</button>

  <div id="resultado"></div>

  <script>
    function calcularPropina() {
      const total = parseFloat(document.getElementById('total').value);
      const porcentaje = parseFloat(document.getElementById('porcentaje').value);
      
      if (isNaN(total) || isNaN(porcentaje)) {
        document.getElementById('resultado').innerText = "Por favor, introduce números válidos.";
        return;
      }

      const propina = total * (porcentaje / 100);
      const totalFinal = total + propina;

      document.getElementById('resultado').innerHTML = `
        Propina: ${propina.toFixed(2)}€<br>
        <strong>Total a pagar: ${totalFinal.toFixed(2)}€</strong>
      `;
    }
  </script>

</body>
</html>
