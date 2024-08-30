package routines;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class DBUtils {

    /**
     * Verifica si una tabla existe en el esquema especificado y la crea si no existe.
     * 
     * @param conn      Conexión a la base de datos
     * @param schema    Esquema donde se va a buscar/crear la tabla
     * @param tableName Nombre de la tabla a verificar/crear
     * @param columns   Definición de las columnas para la tabla
     * @return          Mensaje indicando el resultado de la operación
     */
    public static String ensureTableExists(Connection conn, String schema, String tableName, String columns) {
        if (conn != null) {
            try {
                Statement stmt = conn.createStatement();
                
                // Consulta para verificar si la tabla existe en el esquema especificado
                String checkTableQuery = "SELECT COUNT(*) FROM all_tables WHERE table_name = '" + tableName.toUpperCase() + "' AND owner = '" + schema.toUpperCase() + "'";
                ResultSet rsCheck = stmt.executeQuery(checkTableQuery);
                
                rsCheck.next();
                int tableCount = rsCheck.getInt(1);
                rsCheck.close();
                
                if (tableCount > 0) {
                    // La tabla existe
                    return "La tabla " + schema + "." + tableName + " ya existe.";
                } else {
                    // La tabla no existe, crearla
                    String createTableSQL = "CREATE TABLE " + schema + "." + tableName + " (" + columns + ")";
                    stmt.executeUpdate(createTableSQL);
                    return "Tabla " + schema + "." + tableName + " creada exitosamente.";
                }
                
            } catch (SQLException e) {
                e.printStackTrace();
                return "Error al verificar o crear la tabla: " + e.getMessage();
            }
        } else {
            return "No se pudo obtener la conexión a la base de datos.";
        }
    }
    
    /**
     * Verifica si un esquema existe en la base de datos Oracle y lo crea si no existe.
     *
     * @param conn            Conexión a la base de datos utilizando un usuario maestro.
     * @param schemaName      Nombre del esquema que deseas verificar/crear.
     * @param schemaPassword  Contraseña para el esquema si necesita ser creado.
     * @return                Mensaje indicando el resultado de la operación.
     */
    public static String ensureSchemaExists(Connection conn, String schemaName, String schemaPassword) {
        if (conn != null) {
            try {
                Statement stmt = conn.createStatement();
                
                // Consulta para verificar si el esquema existe
                String checkSchemaQuery = "SELECT COUNT(*) FROM dba_users WHERE username = UPPER('" + schemaName + "')";
                ResultSet rsCheck = stmt.executeQuery(checkSchemaQuery);
                
                rsCheck.next();
                int schemaCount = rsCheck.getInt(1);
                rsCheck.close();
                
                if (schemaCount > 0) {
                    // El esquema existe
                    return "El esquema " + schemaName + " ya existe.";
                } else {
                    // El esquema no existe, crear el esquema
                    String createSchemaSQL = "CREATE USER " + schemaName + " IDENTIFIED BY " + schemaPassword;
                    stmt.executeUpdate(createSchemaSQL);
                    
                    // Otorgar privilegios básicos al esquema
                    String grantPrivilegesSQL = "GRANT CONNECT, RESOURCE TO " + schemaName;
                    stmt.executeUpdate(grantPrivilegesSQL);
                    
                    return "Esquema " + schemaName + " creado exitosamente.";
                }
                
            } catch (SQLException e) {
                e.printStackTrace();
                return "Error al verificar o crear el esquema: " + e.getMessage();
            }
        } else {
            return "No se pudo obtener la conexión a la base de datos.";
        }
    }
    
    /**
     * Elimina todos los registros de una tabla especificada.
     *
     * @param conn       Conexión a la base de datos.
     * @param schema     Esquema de la tabla.
     * @param tableName  Nombre de la tabla de la que se desean eliminar los datos.
     * @return           Mensaje indicando si la operación fue exitosa o no.
     */
    public static String deleteAllDataFromTable(Connection conn, String schema, String tableName) {
        if (conn != null) {
            try {
                Statement stmt = conn.createStatement();

                // Comando SQL para eliminar todos los datos de la tabla
                String deleteSQL = "DELETE FROM " + schema + "." + tableName;
                stmt.executeUpdate(deleteSQL);

                return "Todos los datos de la tabla " + schema + "." + tableName + " han sido eliminados.";

            } catch (SQLException e) {
                e.printStackTrace();
                return "Error al eliminar los datos de la tabla: " + e.getMessage();
            }
        } else {
            return "No se pudo obtener la conexión a la base de datos.";
        }
    }
    
    /**
     * Combina las operaciones de asegurar que el esquema y la tabla existen, y luego borra los datos de la tabla si es necesario.
     *
     * @param conn           Conexión a la base de datos
     * @param schemaName     Nombre del esquema que deseas verificar/crear
     * @param schemaPassword Contraseña para el esquema si necesita ser creado
     * @param tableName      Nombre de la tabla que deseas verificar/crear
     * @param columns        Definición de las columnas para la tabla
     * @param resetData      Indica si los datos deben ser eliminados después de crear/verificar la tabla
     * @return               Mensaje indicando el resultado de las operaciones
     */
    public static String setupSchemaTableAndResetData(Connection conn, String schemaName, String schemaPassword, String tableName, String columns, boolean resetData) {
        String resultMessage = "";

        // Asegurar que el esquema existe
        resultMessage += ensureSchemaExists(conn, schemaName, schemaPassword) + "\n";

        // Asegurar que la tabla existe
        resultMessage += ensureTableExists(conn, schemaName, tableName, columns) + "\n";

        // Eliminar los datos de la tabla si resetData es verdadero
        if (resetData) {
            resultMessage += deleteAllDataFromTable(conn, schemaName, tableName) + "\n";
        }

        return resultMessage;
    }
}
