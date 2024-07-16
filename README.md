### Informe de Inspección de Código Fuente

#### Proyecto: Aplicación de Punto de Venta en Java FX con PostgreSQL

#### Estructura del Proyecto:
- **Aplicación**: Java FX
- **Base de Datos**: PostgreSQL

---

### Errores Identificados y Soluciones:

1. **Error: Uso Incorrecto de Constante `yes`**
   - **Archivo:** `ControlesBasicos.java`
   - **Mensaje de Error:**
     ```java
     if (pregunta == yes) {
     ```
   - **Solución:**
     ```java
     if (pregunta == JOptionPane.YES_OPTION) {
     ```
     

2. **Error: Clase `PreparedStatement` No Encontrada**
   - **Archivo:** `ProductoController.java`
   - **Mensaje de Error:**
     ```java
     java: cannot find symbol
       symbol:   class PreparedStatement
     ```
   - **Solución:**
     ```java
     import java.sql.PreparedStatement;
     ```

3. **Error: Variable `n` No Declarada**
   - **Archivo:** `ProductoController.java`
   - **Mensaje de Error:**
     ```java
     java: cannot find symbol
       symbol:   variable n
     ```
   - **Solución:**
     ```java
     int n = estado.executeUpdate(); // Añadir declaración de `n`
     ```

4. **Error: Uso Incorrecto de Variable `Options`**
   - **Archivo:** `RegistroController.java`
   - **Mensaje de Error:**
     ```java
     java: cannot find symbol
       symbol:   variable Options
     ```
   - **Solución:**
     ```java
     cbAddsex.setItems(options); // Cambiar `Options` a `options`
     ```

5. **Error: Componentes de Tiempo de Ejecución de JavaFX Faltantes**
   - **Mensaje de Error:**
     ```
     Error: JavaFX runtime components are missing, and are required to run this application
     ```
   - **Solución:**
     Asegurarse de incluir las bibliotecas de JavaFX en la configuración de ejecución de IntelliJ IDEA.

6. **Error: Conexión Rechazada a PostgreSQL**
   - **Mensaje de Error:**
     ```
     Connection refused. Check that the hostname and port are correct and that the postmaster is accepting TCP/IP connections.
     ```
   - **Solución:**
     Verificar la configuración de conexión a la base de datos y asegurarse de que el servidor PostgreSQL esté ejecutándose y aceptando conexiones.

7. **Error: Permiso Denegado al Restaurar Backup**
   - **Mensaje de Error:**
     ```
     C:: Permission denied
     ```
   - **Solución:**
     Utilizar `pg_restore` para restaurar el backup:
     ```bash
     pg_restore -U postgres -d ventas C:\Users\julio\Downloads\Punto de Venta\javaFX-PostgreSQL\ventas.backup
     ```

8. **Error: Mensaje de Error en Registro de Usuario**
   - **Descripción:**
     El mensaje mostrado al registrar un usuario exitosamente era incorrecto, indicando un fallo en lugar de éxito.
   - **Código Original:**
     ```java
     if (n > 0) {
         JOptionPane.showMessageDialog(null, "Fallo el registro");
     }
     ```
   - **Solución:**
     ```java
     if (n > 0) {
         JOptionPane.showMessageDialog(null, "Usuario registrado correctamente");
     }
     ```

9. **Error: Índice de Columna Fuera de Rango**
   - **Mensaje de Error:**
     ```
     Error org.postgresql.util.PSQLException: The column index is out of range: 6, number of columns: 5.
     ```
   - **Solución:**
     Se eliminó el `+1` en el límite del bucle `for` que itera sobre las columnas del `ResultSet`:
     ```java
     for(int i = 1 ; i <= rs.getMetaData().getColumnCount(); i++){ // Se quitó el +1 aquí
     ```

10. **Error: Cambio de Nombre de Tabla**
    - **Descripción:**
      La tabla `category` no existía en la base de datos, el nombre correcto era `categoria`.
    - **Código Original:**
      ```java
      String slqCategoria = "SELECT idcategoria, nombre_categoria FROM category";
      ```
    - **Solución:**
      ```java
      String slqCategoria = "SELECT idcategoria, nombre_categoria FROM categoria";
      ```

---

### Resumen:

El informe detalla los errores encontrados durante la inspección del código y las soluciones implementadas para corregirlos. Con estas correcciones, la aplicación de Punto de Venta en Java FX con PostgreSQL debería funcionar correctamente.
