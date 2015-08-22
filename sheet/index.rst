
Catálogo de productos
#####################

.. literalinclude:: ../products.json
    :language: json

Ejemplos de consultas
=====================

Todos los productos:

.. code-block:: coffee

    db.products.find()

Todos los teléfonos:

.. code-block:: coffee

    db.products.find({ type: "phone" })

Nombre e identificador de los teléfonos:

.. code-block:: coffee

    db.products.find({ type: "phone" }, { _id: 1, name: 1 })

Todos los accesorios seleccionando campos:

.. code-block:: coffee

    db.products.find({ type: "accessory" }, { name: 1, for: 1 })

Todos los accesorios seleccionando campos, evitando que se muestre *_id*:

.. code-block:: coffee

    db.products.find({ type: "accessory" }, { _id: 0, name: 1, for: 1 })

Todos los accesorios para *ac3*:

.. code-block:: coffee

    db.products.find({ type: "accessory", for: "ac3" }, { _id: 0, name: 1 })

Todos los productos disponibles:

.. code-block:: coffee

    db.products.find({ $or: [{ available: true }, { type: "service" }] })

Todos los accesorios para *ac3* ordenados por precio:

.. code-block:: coffee

    db.products.find({ type: "accessory", for: "ac3" }}).sort({ price: 1 })

Todos los productos de precio inferior o igual a 40 euros:

.. code-block:: coffee

    db.products.find({ price: { $lte: 40 }}, { _id: 0, name: 1, price: 1 })

Límites y precios de las tarifas de datos:

.. code-block:: coffee

    db.products.find({ "limits.data": { $exists: 1 }},
        { _id: 0, name: 1, "limits.data.n": 1, "limits.data.units": 1 })

Número de fundas para *ac3*:

.. code-block:: coffee

    db.products.find({ for: "ac3", type: "case" }).count()

Producto más caro de cada tipo:

.. code-block:: coffee

    db.products.aggregate([ { $match: { price: { $exists: 1 }}},
        { $group: { _id: "$type", max_price: { $max: "$price" }}} ])

Añadir un nuevo producto:

.. code-block:: coffee

    db.products.insert({ _id: "ac8", name: "AC8 Phone", type: "phone", price: 330 })

Cambiar el precio de un producto:

.. code-block:: coffee

    db.products.update({ _id: "ac8" }, { $set: { price: 400 }})
