# Convertidor de Unidades (Bytes / KB / MB / GB)

> Aplicación de escritorio en Java  para convertir entre unidades de almacenamiento (Byte, Kilobyte, Megabyte, Gigabyte). La conversión se realiza usando factores de potencia de 2 (1 KB = 1024 bytes).

---

##  Resumen

Este proyecto contiene una interfaz gráfica creada con NetBeans (archivo `.form`) y la clase principal `Convertidor.java`. La aplicación permite al usuario introducir una **cantidad**, seleccionar la **unidad de origen** y la **unidad destino**, y obtener el **resultado** de la conversión.



---

##  Archivos principales

* `Convertidor.java` — Clase principal con GUI y la lógica de conversión.
* `Convertidor.form` — Formulario generado por NetBeans que describe la disposición visual de los componentes.

---

## Funcionalidad exacta

* Convierte entre las 4 unidades: **Byte**, **Kilobyte**, **Megabyte**, **Gigabyte**.
* Usa factores de potencia de 2 (base 1024):

  * 1 Kilobyte = 1024 Bytes
  * 1 Megabyte = 1024 Kilobytes = 1024² Bytes
  * 1 Gigabyte = 1024 Megabytes = 1024³ Bytes
* Validaciones básicas en la entrada para permitir solo números y un punto decimal.
* Botón **Convertir**: realiza la conversión.
* Botón **Borrar**: limpia `txtCantidad` y `txtResultado`.

---

##  Interfaz (componentes clave)

* `JTextField txtCantidad` — entrada del valor a convertir.
* `JComboBox<String> u1` — unidad de origen (Byte, Kilobyte, Megabyte, Gigabyte).
* `JComboBox<String> u2` — unidad destino (Byte, Kilobyte, Megabyte, Gigabyte).
* `JButton jButton1` — botón "Convertir".
* `JButton jButton2` — botón "Borrar".
* `JTextField txtResultado` — campo no editable que muestra el resultado.

---

## Lógica de conversión



```java
private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {
    double resultado = 0;
    try {
        double cantidad = Double.parseDouble(txtCantidad.getText());

        String unidadOrigen = (String) u1.getSelectedItem();
        String unidadDestino = (String) u2.getSelectedItem();

        double bytes = 0;

        switch (unidadOrigen) {
            case "Byte":
                bytes = cantidad;
                break;
            case "Kilobyte":
                bytes = cantidad * Math.pow(2, 10);
                break;
            case "Megabyte":
                bytes = cantidad * Math.pow(2, 20);
                break;
            case "Gigabyte":
                bytes = cantidad * Math.pow(2, 30);
                break;
        }

        switch (unidadDestino) {
            case "Byte":
                resultado = bytes;
                break;
            case "Kilobyte":
                resultado = bytes / Math.pow(2, 10);
                break;
            case "Megabyte":
                resultado = bytes / Math.pow(2, 20);
                break;
            case "Gigabyte":
                resultado = bytes / Math.pow(2, 30);
                break;
        }

        txtResultado.setText(Double.toString(resultado));

    } catch (NumberFormatException e) {
        txtResultado.setText("Ingrese un número");
    }
}
```

### Validación de entrada (permitir solo números y un punto)

```java
private void txtCantidadKeyTyped(java.awt.event.KeyEvent evt) {
    char c = evt.getKeyChar();
    if (!Character.isDigit(c) && c != '.' && c != '') {
        evt.consume();
    }
    if (c == '.' && txtCantidad.getText().contains(".")) {
        evt.consume();
    }
}
```

### Borrar campos

```java
private void jButton2ActionPerformed(java.awt.event.ActionEvent evt) {
    txtCantidad.setText("");
    txtResultado.setText("");
}
```

---




##  Autor

Sandoval Reyes Miguel



