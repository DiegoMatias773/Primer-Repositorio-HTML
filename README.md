# Primer-Repositorio-HTML
Saludos soy Diego Matias, un estudiante de Primer Semestre de la Carrera Ingeniería en Software. Mi repositorio trata sobre proyectos y prácticas de programación que he realizado en este semestre que ha sido clave para encaminarme a este mundo de la programación. Durante este primer proyecto nos enseñaron sobre las etiquetas de HTML. A continuación adjunto un ejemplo de una página en HTML que Calcula el total de la factura dependiendo del día y si el pago es con tarjeta decredito
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calcular Factura de Restaurante</title>
</head>
<body>
    <h1>Calcular Factura de Restaurante</h1>
    <script src="../js/ejercicios.js"></script>

    <label for="subtotal">Subtotal de la factura:</label>
    <input type="number" id="subtotal" placeholder="Ingresa el subtotal"><br><br>

    <label for="diaSemana">Día de la semana:</label>
    <select id="diaSemana">
        <option value="lunes">Lunes</option>
        <option value="martes">Martes</option>
        <option value="miércoles">Miércoles</option>
        <option value="jueves">Jueves</option>
        <option value="viernes">Viernes</option>
        <option value="sábado">Sábado</option>
        <option value="domingo">Domingo</option>
    </select><br><br>

    <label for="personas">Número de personas en la mesa:</label>
    <input type="number" id="personas" placeholder="Ingresa el número de personas"><br><br>

    <label>
        <input type="checkbox" id="pagoConTarjeta"> Pago con tarjeta de crédito
    </label><br><br>

    <button onclick="calcularTotal()">Calcular Total</button>
    <p id="resultado"></p>

    <script>
        function calcularTotalFactura(subtotal, diaSemana, personas, pagoConTarjeta) {
            let total = subtotal;

            // Aplica descuento del 15% si es lunes o miércoles y hay más de 4 personas
            if ((diaSemana === "lunes" || diaSemana === "miércoles") && personas > 4) {
                total -= subtotal * 0.15;
            }

            // Aplica recargo del 10% si es fin de semana (sábado o domingo)
            if (diaSemana === "sábado" || diaSemana === "domingo") {
                total += subtotal * 0.10;
            }

            // Aplica comisión del 5% si se paga con tarjeta de crédito
            if (pagoConTarjeta) {
                total += subtotal * 0.05;
            }

            return total;
        }

        function calcularTotal() {
            const subtotal = parseFloat(document.getElementById("subtotal").value);
            const diaSemana = document.getElementById("diaSemana").value;
            const personas = parseInt(document.getElementById("personas").value);
            const pagoConTarjeta = document.getElementById("pagoConTarjeta").checked;
            const resultado = document.getElementById("resultado");

            if (isNaN(subtotal) || isNaN(personas) || subtotal <= 0 || personas <= 0) {
                resultado.textContent = "Por favor, ingresa valores válidos.";
                return;
            }

            const totalAPagar = calcularTotalFactura(subtotal, diaSemana, personas, pagoConTarjeta);
            resultado.textContent = `El total a pagar es: $${totalAPagar.toFixed(2)}`;
        }
    </script>
</body>
</html>
