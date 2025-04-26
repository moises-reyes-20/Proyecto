<?php 
class RegistroAlumno {
    public $mensaje = "";

    public function registrar($nombre, $matricula, $correo, $contraseña, $fecha_nacimiento, $fecha_registro, $hora_registro, $area) {
        // Validación 
        if(empty($nombre) || empty($matricula) || empty($correo) || empty($contraseña)){
            $this->mensaje = "Por favor completa todos los campos.";
        } else {
            $this->mensaje = "Registro exitoso de: " . htmlspecialchars($nombre) . "<br>Matrícula: " . htmlspecialchars($matricula) . "<br>Correo Institucional: " . htmlspecialchars($correo) . "<br>Fecha de Nacimiento: " . htmlspecialchars($fecha_nacimiento) . "<br>Fecha de Registro: " . htmlspecialchars($fecha_registro) . "<br>Hora de Registro: " . htmlspecialchars($hora_registro) . "<br>Área seleccionada: " . htmlspecialchars($area);
        }
    }
}

$registro = new RegistroAlumno();

if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $nombre = trim($_POST["nombre"]);
    $matricula = trim($_POST["matricula"]);
    $correo = trim($_POST["correo"]);
    $contraseña = trim($_POST["contraseña"]);
    $fecha_nacimiento = $_POST["FechaNac"];
    $fecha_registro = $_POST["Fecha_Reg"];
    $hora_registro = $_POST["Tiempo"];
    $area = $_POST["area"];

    $registro->registrar($nombre, $matricula, $correo, $contraseña, $fecha_nacimiento, $fecha_registro, $hora_registro, $area);
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
        <label for="Nombre">Nombre Completo</label><br>
        <input type="text" name="nombre" required ><br>
        <label for="Matricula">Matrícula</label><br>
        <input type="text" name="matricula" required ><br>
        <label for="Correo">Correo Institucional</label><br>
        <input type="email" name="correo" required ><br>
        <label for="Contraseña">Contraseña</label><br>
        <input type="password" name="contraseña" required ><br>
        <label for="FechaNac">Fecha Nacimiento</label><br>
        <input type="date" name="FechaNac" required><br>
        <label for="FechaReg">Fecha Registro</label><br>
        <input type="date" name="Fecha_Reg" required ><br>
        <label for="Tiempo">Hora de Registro</label><br>
        <input type="time" name="Tiempo" required><br>
        <label for="Area">Área</label><br>
        <select name="area" required>
            <option value="Laboratorio de informatica">Laboratorio de informática</option>
            <option value="Informática">Informática</option>
            <option value="Auditorio">Auditorio</option>
        </select><br><br>
        <button type="submit">Registrarse</button>
    </form>
    
    <?php if (!empty($registro->mensaje)): ?>
        <div class="<?= strpos($registro->mensaje, 'exitoso') !== false ? 'alert-success' : 'alert-danger' ?>">
            <?= $registro->mensaje ?>
        </div>
    <?php endif; ?>
</body>
</html>
