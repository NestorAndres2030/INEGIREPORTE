package routines;

import java.sql.Connection;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Calendar;
import java.util.Date;

public class PrepararJob {

	/**
     * Elimina los registros de una tabla con la fecha actual del sistema..
     */
    public static void borrarRegistrosPorMesAnio(Connection conn, String nombreTabla, String nombreColumnaFecha, Date fechaBuscar) {

    	Calendar calendar = Calendar.getInstance();
    	calendar.setTime(fechaBuscar);

    	int currentMonth = calendar.get(Calendar.MONTH);
    	int currentYear = calendar.get(Calendar.YEAR);

    	try {
    		Statement stmt = conn.createStatement();

	    	System.out.println(nombreTabla + " dice: Eliminando pre-registros...");
	
			String deleteQuery = "DELETE FROM REPREG." + nombreTabla + " WHERE TRUNC(" + nombreColumnaFecha + ", 'MM') = TO_DATE('" + currentYear + "' || '-' || '" + (currentMonth + 1) + "', 'YYYY-MM')";
			stmt.executeUpdate(deleteQuery);
			
			conn.commit();
			stmt.close();
			
			System.out.println(nombreTabla + " dice: Pre-registros eliminados");
    	} catch (SQLException e) {
            try {
				conn.rollback();
			} catch (SQLException e1) {
				e1.printStackTrace();
				System.out.println(nombreTabla + " dice: Error al hacer Rolled back en el metodo borrarRegistrosPorMesAnio");
			}
            e.printStackTrace();
            System.out.println(nombreTabla + " dice: Rolled back.");
        }
    }
}
