package routines;

import java.io.FileOutputStream;
import java.io.FileInputStream;
import java.io.IOException;

public class FileUtils {

    // Método para escribir datos en un archivo
    public static void writeToFile(String filePath, String data) throws IOException {
        FileOutputStream fos = new FileOutputStream(filePath);
        fos.write(data.getBytes());
        fos.close();
    }

    // Método para leer datos de un archivo
    public static String readFromFile(String filePath) throws IOException {
        FileInputStream fis = new FileInputStream(filePath);
        StringBuilder content = new StringBuilder();
        int contentInt;
        while ((contentInt = fis.read()) != -1) {
            content.append((char) contentInt);
        }
        fis.close();
        return content.toString();
    }
}
