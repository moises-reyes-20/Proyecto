<?php 
$mensaje = "";
$contra = "";
if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $nombre = trim($_POST["nombre"]);
    $fecha_nacimiento = $_POST["FechaNac"];
    $fecha_registro = $_POST["Fecha_Reg"];

    // Convertir fechas a objetos DateTime
    $fecha_nac = new DateTime($fecha_nacimiento);
    $fecha_reg = new DateTime($fecha_registro);
    $hoy = new DateTime();
    // Calcular la edad 
    $edad = $hoy->diff($fecha_nac)->y;

    // Obtener el día de la semana (1 = lunes, 7 = domingo)
    $dia_semana_registro = $fecha_reg->format("N");

    // Validación 

    if($nombre == " "){
     $mensaje = "Por favor ingresa tu nombre";
    }
    elseif ($edad < 18) {
        $mensaje = "Error: debes ser mayor de 18 años para registrarte.";
    } elseif ($dia_semana_registro >= 6) {
        $mensaje = "Error: No puedes registrarte en fin de semana.";
    } else {
        $mensaje = "Registro exitoso de: " . htmlspecialchars($nombre);
    }
}
?>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registro Alumno</title>
    <style>
        .alert-success { color: green; font-weight: bold; }
        .alert-danger { color: red; font-weight: bold; }
    </style>
</head>
<body>
    <form method="post">
        <label for="Nombre">Nombre</label><br>
        <input type="text" name="nombre" require ><br>
        <label for="FechaNac">Fecha Nacimiento</label><br>
        <input type="date" name="FechaNac" require><br>
        <label for="FechaReg">Fecha Registro</label><br>
        <input type="date" name="Fecha_Reg" id="FechaRegistro" require ><br><br>
        <br><input type="time" name="Tiempo" id="tiempo">
        <button type="submit">Registrarse</button>
    </form>
    
    <?php if (!empty($mensaje)): ?>
        <div class="<?= strpos($mensaje, 'exitoso') !== false ? 'alert-success' : 'alert-danger' ?>">
            <?= $mensaje ?>
        </div>
    <?php endif; ?>

    <script>
        document.getElementById("FechaRegistro").addEventListener("input", function() {
            let fecha = new Date(this.value);
            let diaSemana = fecha.getDay(); // 0 = domingo, 6 = sábado 

            if (diaSemana === 5 || diaSemana === 6) {
                alert("No puedes registrarte en fines de semana. Selecciona otro día.");
                this.value = "";
            }
        });
    </script>
</body>
</html>
