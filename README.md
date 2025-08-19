# 🏠 Casa Inteligente

Este proyecto integra **Arduino** y una **aplicación de escritorio (VB.NET / Windows Forms)** para el control y monitoreo de una casa inteligente.  
Permite encender y apagar luces, visualizar lecturas de sensores (humedad, luz y movimiento) y subir los datos en tiempo real a **Firebase Realtime Database**.

---

## 📂 Estructura del proyecto

```
CASA-INTELIGENTE/
├── arduino/                # Código para Arduino
│   └── casahogar.ino
├── app-winforms/           # Aplicación de escritorio (VB.NET)
│   ├── Form1.vb
│   ├── Form1.Designer.vb
│   ├── conexion.vb
│   ├── App.config
│   └── ...
├── README.md               # Este archivo
```

---

## ⚙️ Requisitos

### Hardware
- Arduino UNO (o compatible)
- Sensores:
  - Humedad del suelo → conectado a **A0**
  - Sensor de luz (LDR) → conectado a **A1**
  - Sensor PIR → conectado a **D5**
- LEDs de control conectados a **pines 6 a 13**

### Software
- [Arduino IDE](https://www.arduino.cc/en/software) (para cargar `casahogar.ino`)
- Visual Studio 2019/2022 (con soporte **VB.NET**)
- .NET Framework 4.x (recomendado 4.7+)
- Paquete NuGet: **FirebaseDatabase.net**

---

## 🚀 Instalación y ejecución

### 1. Clonar repositorio
```bash
git clone https://github.com/tu-usuario/casa-inteligente.git
cd casa-inteligente
```

### 2. Cargar Arduino
1. Abrir `arduino/casahogar.ino` en el **Arduino IDE**.
2. Seleccionar la placa y puerto correcto.
3. Cargar el sketch en el Arduino.
4. Verificar que el monitor serie muestre las lecturas (`humedad`, `luz`, `movimiento`).

### 3. Configurar la App de Escritorio
1. Abrir la carpeta `app-winforms/` en **Visual Studio**.
2. Editar el archivo `conexion.vb` con la URL de tu **Firebase**:
   ```vbnet
   Private Shared firebaseUrl As String = "https://<TU_PROYECTO>.firebaseio.com/"
   ```
   ⚠️ Asegúrate de **no dejar espacios** al final de la URL.
3. Si tu Firebase requiere autenticación, añade el **AuthToken** en la inicialización del `FirebaseClient`.
4. Compilar el proyecto (`Ctrl+Shift+B`).

### 4. Ejecutar
- Conecta el Arduino y verifica el puerto COM.
- Corre la aplicación.
- Deberías poder:
  - Encender/apagar luces con los botones.
  - Visualizar en tiempo real los valores de los sensores.
  - Ver los datos guardados en **Firebase Realtime Database** en el nodo `lecturas`.

---

## 📡 Comunicación Arduino ↔ PC

- **Baudrate**: `9600`
- **Protocolo serial**:
  - Arduino envía cada 1s:
    ```
    humedad: XX%
    luz: YY%
    movimiento: Detectado/No detectado
    ```
  - PC envía comandos:
    - `a/b` → Pin 13 ON/OFF
    - `c/d` → Pin 12 ON/OFF
    - ...
    - `o/p` → Pin 6 ON/OFF
    - `1` → Todos ON
    - `0` → Todos OFF

---

## 🛠 Mejoras futuras
- Autodetección del puerto COM.
- Normalización de lecturas (usar JSON en lugar de texto plano).
- Dashboard web/móvil conectado a Firebase.
- Alertas push o correo cuando se detecte movimiento.

---

## 📜 Licencia
Este proyecto está bajo la licencia MIT.  
¡Si lo usas, comparte y mejora! 🙌
