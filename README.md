
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sabor Colombiano</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f3f3f3;
            margin: 0;
            padding: 0;
        }
        .container {
            width: 90%;
            max-width: 1200px;
            margin: 20px auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }
        .header {
            background: linear-gradient(to right, #fcd116, #003893, #ce1126);
            color: white;
            padding: 20px;
            text-align: center;
        }
        .header h1 {
            margin: 0;
            font-size: 2em;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.4);
        }
        .logo {
            margin: 20px auto;
            text-align: center;
            background: #fcd116;
            padding: 20px;
            border-radius: 10px;
        }
        .logo img {
            max-width: 150px;
            border-radius: 50%;
            border: 4px solid #fcd116;
        }
        .productos {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            padding: 20px;
            justify-content: space-between;
            background: #fcd116;
        }
        .producto {
            text-align: center;
            padding: 10px;
            background: white;
            border: 2px solid #003893;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            flex: 1 1 calc(20% - 15px);
            max-width: calc(20% - 15px);
            transition: transform 0.2s;
        }
        .producto:hover {
            transform: scale(1.05);
        }
        .producto img {
            width: 100%;
            max-width: 100px;
            margin-bottom: 10px;
            border-radius: 8px;
        }
        .cantidad {
            margin: 20px 0;
            text-align: center;
            background: #003893;
            padding: 20px;
            color: white;
        }
        .cantidad input {
            width: 50%;
            padding: 10px;
            font-size: 1em;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .total {
            background: #ce1126;
            color: white;
            font-size: 1.5em;
            font-weight: bold;
            text-align: center;
            padding: 15px;
        }
        .botones {
            text-align: center;
            margin: 20px;
        }
        button {
            background-color: #003893;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1em;
            margin: 5px;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #001f5c;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Sabor Colombiano</h1>
        </div>

        <div class="logo">
            <img src="imagenes/Logo_Restaurante.png.png" alt="Sabor Colombiano">
        </div>

        <div class="cantidad">
            <input type="number" id="cantidad-global" placeholder="Cantidad" min="1">
        </div>

        <div class="productos" id="productos">
        </div>

        <div class="total" id="total">Total: $0</div>

        <div class="botones">
            <button onclick="aplicarDescuento()">Descuento</button>
            <button onclick="borrarCarrito()">Borrar Carrito</button>
        </div>
    </div>

    <script>
        const productos = [
            { nombre: "Bandeja Paisa", precio: 150000, imagen: "Imagenes/Bandeja_paisa.png" },
            { nombre: "Arepa con queso", precio: 100000, imagen: "Imagenes/Arepa_con_queso.png" },
            { nombre: "Papa Rellena", precio: 120000, imagen: "Imagenes/Papa_rellena.png.png" },
            { nombre: "Pollo Crispy", precio: 140000, imagen: "Imagenes/Pollo_crispy.png.png" },
            { nombre: "Picada", precio: 160000, imagen: "Imagenes/Picada.png.png" },
            { nombre: "Tintico", precio: 100000, imagen: "Imagenes/Tintico.png.png" },
            { nombre: "Jugo de Maracuya", precio: 100000, imagen: "Imagenes/Jugo_maracuya.png.png" },
            { nombre: "Pony Malta", precio: 100000, imagen: "Imagenes/Pony_malta.png.png" },
            { nombre: "Arroz con leche", precio: 120000, imagen: "Imagenes/arroz_con_leche.png" },
            { nombre: "Aguardiente", precio: 160000, imagen: "Imagenes/Aguardiente.png" },
            { nombre: "Caja sorpresa", precio: 3000000, imagen: "Imagenes/Caja_Sorpresa.png.png" }
        ];

        let total = 0;
        let descuentoAplicado = false;

        const productosContainer = document.getElementById("productos");
        const totalContainer = document.getElementById("total");

        function actualizarTotal() {
            totalContainer.textContent = `Total: $${total.toLocaleString()}`;
        }

        function agregarProducto(precio, nombreProducto) {
            const cantidadGlobal = parseInt(document.getElementById("cantidad-global").value) || 0;
            if (cantidadGlobal > 0) {
                total += precio * cantidadGlobal;
                actualizarTotal();
            } else {
                alert(`Por favor, ingresa una cantidad válida para ${nombreProducto}.`);
            }
        }

        function borrarCarrito() {
            total = 0;
            descuentoAplicado = false;
            document.getElementById("cantidad-global").value = "";
            actualizarTotal();
        }

        function aplicarDescuento() {
            if (!descuentoAplicado) {
                total = total - (total * 0.4);
                descuentoAplicado = true;
                actualizarTotal();
            } else {
                alert("El descuento ya ha sido aplicado.");
            }
        }

        productos.forEach(producto => {
            const productoDiv = document.createElement("div");
            productoDiv.className = "producto";

            const img = document.createElement("img");
            img.src = producto.imagen;
            img.alt = producto.nombre;

            const nombre = document.createElement("div");
            nombre.textContent = producto.nombre;

            const precio = document.createElement("div");
            precio.textContent = `$${producto.precio.toLocaleString()}`;

            const boton = document.createElement("button");
            boton.textContent = "Añadir";
            boton.onclick = () => agregarProducto(producto.precio, producto.nombre);

            productoDiv.appendChild(img);
            productoDiv.appendChild(nombre);
            productoDiv.appendChild(precio);
            productoDiv.appendChild(boton);

            productosContainer.appendChild(productoDiv);
        });

        actualizarTotal();
    </script>
</body>
</html>
