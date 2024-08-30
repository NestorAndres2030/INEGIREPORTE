package routines;

import java.util.Calendar;
import java.util.Date;

public class GeneradorFechas {

    /**
     * Regresa un String de la fecha actual del sistema
     * con el último día del mes en formato DD-MM-AAAA.
     */
    public static String getFechaConUltimoDiaDelMes () {
    	Date currentDate = new Date();

    	Calendar calendar = Calendar.getInstance();
    	calendar.setTime(currentDate);

    	int currentMonth = calendar.get(Calendar.MONTH);
    	int currentYear = calendar.get(Calendar.YEAR);
    	calendar.set(Calendar.DAY_OF_MONTH, calendar.getActualMaximum(Calendar.DAY_OF_MONTH));
    	int lastDayOfCurrentMonth = calendar.get(Calendar.DAY_OF_MONTH);

    	return lastDayOfCurrentMonth + "-" + (currentMonth + 1) + "-" + currentYear;
    }
    
    public static String getMesAnteriorConUltimoDiaDelMes () {
    	Date currentDate = new Date();
    	
    	Calendar calendar = Calendar.getInstance();
    	calendar.setTime(currentDate);

    	calendar.setTime(currentDate);
    	calendar.add(Calendar.MONTH, -1);
    	int previousMonth = calendar.get(Calendar.MONTH);
    	int previousYear = calendar.get(Calendar.YEAR);
    	calendar.set(Calendar.DAY_OF_MONTH, calendar.getActualMaximum(Calendar.DAY_OF_MONTH));
    	int lastDayOfPreviousMonth = calendar.get(Calendar.DAY_OF_MONTH);

    	return lastDayOfPreviousMonth + "-" + (previousMonth + 1) + "-" + previousYear;
    }
}
