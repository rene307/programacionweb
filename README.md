# programacionweb

from flask import Flask, render_template, request

app = Flask(__name__)
@app.route("/")
def index():
    return render_template("index.html")

@app.route("/ejercicio1", methods=["GET", "POST"])
def ejercicio1():
    if request.method == "POST":
        # Procesar notas
        nota1 = float(request.form.get("nota1", 0))
        nota2 = float(request.form.get("nota2", 0))
        nota3 = float(request.form.get("nota3", 0))
        asistencia = float(request.form.get("asistencia", 0))
        promedio = (nota1 + nota2 + nota3) / 3
        estado = "APROBADO" if promedio >= 40 and asistencia >= 75 else "REPROBADO"
        return render_template("formulario_notas.html", promedio=promedio, estado=estado)
    return render_template("formulario_notas.html")

@app.route("/ejercicio2", methods=["GET", "POST"])
def ejercicio2():
    if request.method == "POST":
        # Procesar nombres
        nombres = [
            request.form.get("nombre1", ""),
            request.form.get("nombre2", ""),
            request.form.get("nombre3", "")
        ]
        nombre_largo = max(nombres, key=len)
        return render_template("formulario_nombres.html", nombre_largo=nombre_largo, largo=len(nombre_largo))
    return render_template("formulario_nombres.html")



if __name__ == "__main__":
    app.run(debug=True)
---------------------------------------------------------------------------------------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Botones</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 100px;
        }
        .button {
            display: block;
            margin: 10px auto;
            padding: 10px 20px;
            font-size: 18px;
            color: white;
            background-color: #007BFF;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            text-decoration: none;
            width: 100px;
            height: 50px;

        }
        .button:hover {
            background-color: #0056b3;
        }
    </style>
---------------------------------------------------------------------------------------------------------------------------------------------------------
    <link rel="stylesheet" href="styles.css">

</head>
<body>
    <h1>Bienvenido</h1>
    <a href="/ejercicio1" class="button">Ejercicio 1</a>
    <a href="/ejercicio2" class="button">Ejercicio 2</a>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulario de Notas</title>
    <style>
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

form {
    background-color: #ffffff;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    max-width: 400px;
    width: 100%;
}

h1 {
    text-align: center;
    color: #333333;
    margin-bottom: 20px;
}

label {
    display: block;
    font-weight: bold;
    margin-bottom: 5px;
    color: #555555;
}

input {
    width: 100%;
    padding: 10px;
    margin-bottom: 15px;
    border: 1px solid #cccccc;
    border-radius: 5px;
    font-size: 14px;
}

button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px 15px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
    width: 100%;
}

button:hover {
    background-color: #0056b3;
}

h3 {
    text-align: center;
    color: #333333;
    margin-top: 20px;
}






</style>
---------------------------------------------------------------------------------------------------------------------------------------------------------
</head>
<body>
    <h1>Formulario de Notas</h1>
    <form method="POST">
        <label for="nota1">Nota 1:</label>
        <input type="number" id="nota1" name="nota1" required>
        <br>
        <label for="nota2">Nota 2:</label>
        <input type="number" id="nota2" name="nota2" required>
        <br>
        <label for="nota3">Nota 3:</label>
        <input type="number" id="nota3" name="nota3" required>
        <br>
        <label for="asistencia">Asistencia (%):</label>
        <input type="number" id="asistencia" name="asistencia" required>
        <br><br>
        <button type="submit">Enviar</button>
    </form>

    {% if promedio is not none %}
        <h3>Promedio: {{ promedio }}</h3>
        <h3>Estado: {{ estado }}</h3>
    {% endif %}
</body>
</html>


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulario de Nombres</title>

    <style>
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

form {
    background-color: #ffffff;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    max-width: 400px;
    width: 100%;
}

h1 {
    text-align: center;
    color: #333333;
    margin-bottom: 20px;
}

label {
    display: block;
    font-weight: bold;
    margin-bottom: 5px;
    color: #555555;
}

input {
    width: 100%;
    padding: 10px;
    margin-bottom: 15px;
    border: 1px solid #cccccc;
    border-radius: 5px;
    font-size: 14px;
}

button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px 15px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
    width: 100%;
}

button:hover {
    background-color: #0056b3;
}

h3 {
    text-align: center;
    color: #333333;
    margin-top: 20px;
}


</style>



</head>
<body>
    <h1>Formulario de Nombres</h1>
    <form method="POST">
        <label for="nombre1">Nombre 1:</label>
        <input type="text" id="nombre1" name="nombre1" required>
        <br>
        <label for="nombre2">Nombre 2:</label>
        <input type="text" id="nombre2" name="nombre2" required>
        <br>
        <label for="nombre3">Nombre 3:</label>
        <input type="text" id="nombre3" name="nombre3" required>
        <br><br>
        <button type="submit">Enviar</button>
    </form>

    {% if nombre_largo is not none %}
        <h3>El nombre con más caracteres es: {{ nombre_largo }}</h3>
        <h3>Cantidad de caracteres: {{ largo }}</h3>
    {% endif %}
</body>
</html>






    
