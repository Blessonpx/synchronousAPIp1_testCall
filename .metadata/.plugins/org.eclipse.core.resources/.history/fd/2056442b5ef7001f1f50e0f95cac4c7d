package synchronousAPIp1;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.PrintWriter;
import java.net.InetSocketAddress;
import java.net.ServerSocket;
import java.net.Socket;

public class SynchronousEcho {
	public static void main(String[] args) throws Throwable{
		ServerSocket  server = new ServerSocket();
		server.bind(new InetSocketAddress(3000));
		while(true) {
			Socket socket = server.accept();
			System.out.println("Client connected: " + socket.getInetAddress());
            new Thread(clientHandler(socket)).start(); // Run handler in new thread
		}
	}
	
	private static Runnable clientHandler(Socket socket) {
		return()->{
			try(
					BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
					PrintWriter writer = new PrintWriter(new OutputStreamWriter(socket.getOutputStream()),true)
				)
			{
				String line = "";
				while((line = reader.readLine()) != null && !line.equalsIgnoreCase("/quit")) {
					System.out.println("Received: " + line);
                    writer.println("~"+line); // Echo back to client
				}
				System.out.println("Client disconnected.");
				}catch(IOException e) {
						e.printStackTrace();
				}finally {
					try {
	                    socket.close();
	                } catch (IOException e) {
	                    e.printStackTrace();
	                }
				}
		};		
	}
}
