# SISTEMAS_DISTRIBUIDOS
\\\CLIENT
import java.rmi.*;
import java.util.*;

public class client {
    public static void main(String[] args) throws Exception
    {
        Scanner sc = new Scanner(System.in);
        while (true) {
            // MENU
            System.out.println(
                "\n1.Adição\n2.Subtração\n3.multiplicação\n4.divisão");
            System.out.println("Qual a opção:");
            int opt = sc.nextInt();
            if (opt == 4) {
                break;
            }
            System.out.println(
                "Entre com primeiro número:");
            int a = sc.nextInt();
            System.out.println("Entre com segundo número:");
            int b = sc.nextInt();
            int n;
            switch (opt) {
            case 1: 
                
                AddInterface obj
                        = (AddInterface)Naming.lookup("ADD");
                n = obj.add(a, b);
                System.out.println("Adição= " + n);
                break;
            case 2:
                SubInterface obj1
                        = (SubInterface)Naming.lookup("ADD");
                n = obj1.sub(a, b);
                System.out.println("Substração= " + n);
                break;
            case 3:
                MulInterface obj2
                        = (MulInterface)Naming.lookup("ADD");
                n = obj2.mul(a, b);
                System.out.println("Multiplicação = " + n);
                break;
            case 4:
                DivInterface obj3
                        = (DivInterface)Naming.lookup("ADD");
                n = obj3.div(a, b);
                System.out.println("Divisão = " + n);
                break;
                
            }
        }
    }
    
}

\\\ SERVER
import java.rmi.*;
import java.rmi.registry.*;

public class Server {
    
    public static void main(String[] args) throws Exception
    {
  
        Impl obj = new Impl();
  
        
        Naming.rebind("ADD", obj);
  
        System.out.println("Servidor Iniciado");
    }
    
}

\\\IMPL
import java.rmi.*;
import java.rmi.server.*;

/**
 *
 * @author SÁVIO FRANÇA
 */
public class Impl extends UnicastRemoteObject
    implements AddInterface, SubInterface, MulInterface,
               DivInterface {
    
    public Impl() throws Exception { super(); }
    
    public int add(int x, int y) { return x + y; }
    public int sub(int x, int y) { return x - y; }
    public int mul(int x, int y) { return x * y; }
    public int div(int x, int y) { return x / y; }
    
}

\\\ADIÇÃO
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface AddInterface extends Remote {
    
    public int add(int x, int y) throws RemoteException;
    
}

\\\MULTIPLICAÇÃO
import java.rmi.Remote;
import java.rmi.RemoteException;
public interface MulInterface extends Remote {
    // Declaring the method prototype
    public int mul(int x, int y) throws RemoteException;
    
}


\\\SUBTRAÇÃO
import java.rmi.Remote;
import java.rmi.RemoteException;
public interface SubInterface extends Remote {
    
    public int sub(int x, int y) throws RemoteException;
    
}


\\\DIVISÃO
import java.rmi.Remote;
import java.rmi.RemoteException;
public interface DivInterface extends Remote {
    
    public int div(int x, int y) throws RemoteException;
    
}
