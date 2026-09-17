# Detector de Placas Colombianas

Aplicación móvil para tomar fotografías de vehículos, enviarlas a un servidor y detectar placas colombianas mediante un modelo personalizado YOLOv8.

## ¿Qué contiene el proyecto?

- Aplicación móvil desarrollada con Expo y React Native.
- Acceso a la cámara mediante Expo Camera.
- Servidor Python alojado en AWS.
- Modelo YOLOv8 `best.pt` para localizar placas.
- Recuadro y nivel de confianza sobre cada placa detectada.
- Procesamiento OCR para intentar leer las letras y números de la placa.

## Funcionamiento

```text
Celular toma la fotografía
        ↓
Expo envía la imagen al servidor AWS
        ↓
YOLOv8 encuentra la placa y genera el recuadro
        ↓
El OCR procesa el recorte de la placa
        ↓
La aplicación muestra el resultado
```

## Rutas principales



```text
IP: 34.236.46.110
Puerto: 8080
```

## Encender el servidor

Desde PowerShell:

```powershell
ssh -i 
```

Dentro de AWS:

```bash
cd /home/ubuntu/proyecto
source venv/bin/activate
sudo fuser -k 8080/tcp 2>/dev/null || true
nohup python3 app.py > app.log 2>&1 &
sleep 5
sudo lsof -i :8080
tail -n 50 app.log
```

Si el entorno virtual se llama `.venv`, usar:

```bash
source .venv/bin/activate
```

## Encender Expo Go

En otra ventana de PowerShell:

```powershell
cd 
npx expo start 
```

Después, abrir Expo Go en el celular y escanear el código QR.

## Datos de conexión en la aplicación

```text
IP del servidor: 34.236.46.110
Puerto: 8080
```

## Verificar errores del servidor

```bash
tail -f /home/ubuntu/proyecto/app.log
```

Para dejar de ver el registro sin apagar el servidor, usar `Ctrl + C`.

## Nota

El modelo YOLOv8 localiza la placa y genera el recuadro. La lectura de caracteres depende del OCR y puede requerir una fotografía clara, cercana y con buena iluminación.
