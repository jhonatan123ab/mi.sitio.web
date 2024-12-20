# mi.sitio.web
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pedido de Plantas - Vivero</title>
    <style>
        body {
            font-family: 'Olivia', cursive;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
            background-image: url('https://www.toptal.com/designers/subtlepatterns/uploads/leaves.png');
            background-repeat: repeat;
            color: #333;
        }
        header {
            background-color: #4caf50;
            color: white;
            text-align: center;
            padding: 1rem 0;
            font-size: 1.5rem;
        }
        main {
            padding: 2rem;
            max-width: 600px;
            margin: 2rem auto;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }
        form {
            display: flex;
            flex-direction: column;
        }
        label {
            margin-top: 1rem;
            font-weight: bold;
            color: #2c3e50;
        }
        input, select, button {
            margin-top: 0.5rem;
            padding: 0.5rem;
            font-size: 1rem;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            background-color: #4caf50;
            color: white;
            border: none;
            cursor: pointer;
            font-weight: bold;
        }
        button:hover {
            background-color: #45a049;
        }
        .plantas-container {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin-top: 1rem;
        }
        .planta {
            width: 48%;
            text-align: center;
        }
        .planta img {
            width: 100%;
            height: auto;
            border-radius: 8px;
        }
        .planta label {
            display: block;
            margin-top: 0.5rem;
        }
        .cantidad {
            margin-top: 0.5rem;
        }
        .error {
            color: red;
            font-size: 0.9rem;
            margin-top: 0.5rem;
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Olivia&display=swap" rel="stylesheet">
</head>
<body>
    <header>
        <h1>Pedido de Plantas</h1>
        <p>Selecciona las plantas que deseas y completa tus datos</p>
    </header>
    <main>
        <form id="pedidoForm">
            <div class="plantas-container">
                <div class="planta">
                    <img src=https://www.google.com/url?sa=i&url=https%3A%2F%2Felpais.com%2Festilo-de-vida%2F2024-06-28%2Fpor-que-las-rosas-ya-no-huelen-como-antes-asi-es-la-rosa-narcea-que-rompe-este-mito.html&psig=AOvVaw3e_DNyvwbHf-1gLU2iV3Fy&ust=1734818183779000&source=images&cd=vfe&opi=89978449&ved=0CBQQjRxqFwoTCOjThdmrt4oDFQAAAAAdAAAAABAE" alt="Rosas">
                    <label><input type="checkbox" name="plantas" value="rosas"> Rosas</label>
                    <input type="number" name="cantidad_rosas" class="cantidad" placeholder="Cantidad" min="1">
                </div>
                <div class="planta">
                    <img src="https://cdn.pixabay.com/photo/2017/06/20/20/18/bougainvillea-2424434_1280.jpg" alt="Buganvilias">
                    <label><input type="checkbox" name="plantas" value="buganvilias"> Buganvilias</label>
                    <input type="number" name="cantidad_buganvilias" class="cantidad" placeholder="Cantidad" min="1">
                </div>
                <div class="planta">
                    <img src="https://cdn.pixabay.com/photo/2020/06/17/20/43/plant-5310040_1280.jpg" alt="Pedros">
                    <label><input type="checkbox" name="plantas" value="pedros"> Pedros</label>
                    <input type="number" name="cantidad_pedros" class="cantidad" placeholder="Cantidad" min="1">
                </div>
                <div class="planta">
                    <img src="https://cdn.pixabay.com/photo/2015/07/27/19/44/hydrangea-863056_1280.jpg" alt="Hortencias">
                    <label><input type="checkbox" name="plantas" value="hortencias"> Hortencias</label>
                    <input type="number" name="cantidad_hortencias" class="cantidad" placeholder="Cantidad" min="1">
                </div>
                <div class="planta">
                    <img src="https://cdn.pixabay.com/photo/2016/11/08/05/26/oranges-1804038_1280.jpg" alt="Frutales">
                    <label><input type="checkbox" name="plantas" value="frutales"> Frutales</label>
                    <input type="number" name="cantidad_frutales" class="cantidad" placeholder="Cantidad" min="1">
                </div>
                <div class="planta">
                    <img src="https://cdn.pixabay.com/photo/2016/12/18/13/45/pine-1910488_1280.jpg" alt="Pinos">
                    <label><input type="checkbox" name="plantas" value="pinos"> Pinos</label>
                    <input type="number" name="cantidad_pinos" class="cantidad" placeholder="Cantidad" min="1">
                </div>
            </div>

            <label for="nombre">Nombre:</label>
            <input type="text" id="nombre" name="nombre" required>

            <label for="numero">Número de Teléfono:</label>
            <input type="tel" id="numero" name="numero" pattern="\+591\s\d{8}" placeholder="+591 71234567" required>

            <label for="localidad">Localidad:</label>
            <input type="text" id="localidad" name="localidad" required>

            <div id="error" class="error"></div>

            <button type="submit">Enviar Pedido</button>
        </form>
    </main>
    <script>
        document.getElementById('pedidoForm').addEventListener('submit', function(event) {
            event.preventDefault();

            const errorDiv = document.getElementById('error');
            errorDiv.textContent = '';

            const plantasSeleccionadas = Array.from(document.querySelectorAll('input[name="plantas"]:checked'));
            if (plantasSeleccionadas.length === 0) {
                errorDiv.textContent = 'Por favor, selecciona al menos una planta y su cantidad.';
                return;
            }

            let detallePlantas = '';
            let valid = true;

            plantasSeleccionadas.forEach(planta => {
                const cantidadInput = planta.parentElement.querySelector('.cantidad');
                const cantidad = cantidadInput ? cantidadInput.value : 0;

                if (!cantidad || cantidad <= 0) {
                    valid = false;
                }

                detallePlantas += `- ${planta.nextElementSibling.textContent.trim()} (Cantidad: ${cantidad})\n`;
            });

            if (!valid) {
                errorDiv.textContent = 'Por favor, indica cantidades válidas para las plantas seleccionadas.';
                return;
            }

            const nombre = document.getElementById('nombre').value;
            const numero = document.getElementById('numero').value;
            const localidad = document.getElementById('localidad').value;

            const mensaje = `Pedido de Plantas:\n${detallePlantas}- Nombre: ${nombre}\n- Número: ${numero}\n- Localidad: ${localidad}`;
            
            const url = `https://wa.me/59178313242?text=${encodeURIComponent(mensaje)}`;
            window.open(url, '_blank');
        });
    </script>
</body>
</html>

