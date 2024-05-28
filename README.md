import java.io.*;
import java.net.*;

public class SocketClient {
    public static void main(String[] args) {
        String serverIp = "10.130.129.103";
        int serverPort = 12345;
        String messageToSend = "MTk4Mw==";
        
        try (Socket socket = new Socket(serverIp, serverPort)) {
            // Enviar mensagem ao servidor
            OutputStream output = socket.getOutputStream();
            output.write(messageToSend.getBytes());
            output.flush();
            
            // Receber resposta do servidor
            InputStream input = socket.getInputStream();
            ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();
            byte[] buffer = new byte[1024];
            int bytesRead;
            while ((bytesRead = input.read(buffer)) != -1) {
                byteArrayOutputStream.write(buffer, 0, bytesRead);
            }
            
            // Converter bytes recebidos em String
            String response = new String(byteArrayOutputStream.toByteArray(), "UTF-8");
            
            // Salvar resposta em arquivo
            try (BufferedWriter writer = new BufferedWriter(new FileWriter("server_response.txt"))) {
                writer.write(response);
            }
            
            System.out.println("Resposta do servidor salva em 'server_response.txt'");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
