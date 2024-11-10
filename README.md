# POWERSHELL-WINDOWS
Mi perfil de powershell basada en linux
Sí, en PowerShell también puedes crear alias de comandos como en Termux para facilitar su uso y hacerlos más cortos, de forma similar a los alias en Linux o en el archivo `.bashrc`.

### 1. Crear un alias en PowerShell

Para crear un alias temporal que se mantenga solo durante la sesión actual de PowerShell, puedes usar el comando `Set-Alias`. Por ejemplo, para crear un alias `mv` que haga referencia a `Move-Item`:

```powershell
Set-Alias mv Move-Item
```

Ahora, cuando escribas `mv`, funcionará igual que `Move-Item`.

### 2. Crear un alias para que se mantenga de forma permanente

Para hacer que el alias sea persistente (es decir, que se mantenga entre sesiones de PowerShell), tienes que agregar el alias al perfil de PowerShell. El perfil de PowerShell es como el archivo `.bashrc` en Linux/Termux.

1. Primero, verifica si tienes un perfil configurado usando:

   ```powershell
   Test-Path $PROFILE
   ```

   Si devuelve `False`, significa que el archivo de perfil no existe, y debes crearlo.

2. Para crear el archivo de perfil, usa el siguiente comando:

   ```powershell
   New-Item -Path $PROFILE -ItemType File -Force
   ```

3. Abre el perfil en un editor (puedes usar `notepad`):

   ```powershell
   notepad $PROFILE
   ```

4. Dentro del archivo, agrega el alias que quieres. Por ejemplo, para hacer un alias de `mv` para `Move-Item`:

   ```powershell
   Set-Alias mv Move-Item
   ```

   Puedes guardar este archivo y cerrar el editor. Ahora, cada vez que abras PowerShell, el alias estará disponible.

### 3. Crear una función personalizada para simplificar más

Si también quieres eliminar la necesidad de escribir `-Destination`, puedes crear una función personalizada en lugar de un alias. Por ejemplo, podrías crear una función llamada `mv` que acepte el nombre de archivo y la ruta de destino sin necesidad de usar `-Destination`:

1. Abre nuevamente tu archivo de perfil:

   ```powershell
   notepad $PROFILE
   ```

2. Agrega la siguiente función en el archivo:

   ```powershell
   function mv {
       param (
           [string]$source,
           [string]$destination
       )
       Move-Item $source -Destination $destination
   }
   ```

   Ahora, puedes usar `mv` de la siguiente manera:

   ```powershell
   mv archivo.txt C:\ruta\de\destino
   ```

   Esto moverá el archivo sin necesidad de usar `-Destination`.

### 4. Recargar tu perfil

Para aplicar los cambios inmediatamente, puedes recargar tu perfil sin reiniciar PowerShell usando el siguiente comando:

```powershell
. $PROFILE
```

Ahora, cada vez que uses PowerShell, podrás usar `mv` como alias de `Move-Item`, o como función personalizada para mover archivos fácilmente.
