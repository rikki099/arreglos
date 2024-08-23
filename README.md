# arreglos
import java.util.ArrayList;
import java.util.Random;
import java.util.Scanner;

public class AdivinaPalabra {
    private static ArrayList<String> palabras = new ArrayList<>();
    private static final int OPORTUNIDADES_INICIALES = 5;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        palabras.add("HONDURAS");
        palabras.add("COLOMBIA");
        palabras.add("ARGENTINA");
        palabras.add("GUATEMALA");
        palabras.add("NICARAGUA");
        palabras.add("COSTARICA");
        palabras.add("PANAMA");
        palabras.add("VENEZUELA");
        palabras.add("MEXICO");
        palabras.add("PERU");

        int opcion;
        do {
            // Menú principal
            System.out.println("\n--- Menú Principal ---");
            System.out.println("1. Jugar");
            System.out.println("2. Cambiar Palabras");
            System.out.println("3. Salir");
            System.out.print("Seleccione una opción: ");
            opcion = scanner.nextInt();
            scanner.nextLine(); // Consumir la línea

            switch (opcion) {
                case 1:
                    jugar(scanner);
                    break;
                case 2:
                    cambiarPalabras(scanner);
                    break;
                case 3:
                    System.out.println("¡Hasta luego!");
                    break;
                default:
                    System.out.println("Opción no válida. Intente de nuevo.");
            }
        } while (opcion != 3);
    }

    private static void jugar(Scanner scanner) {
        Random random = new Random();
        String palabraAdivinar = palabras.get(random.nextInt(palabras.size()));
        char[] palabraOculta = new char[palabraAdivinar.length()];
        int oportunidades = OPORTUNIDADES_INICIALES;
        boolean palabraAdivinada = false;

        for (int i = 0; i < palabraOculta.length; i++) {
            palabraOculta[i] = '_';
        }


        while (oportunidades > 0 && !palabraAdivinada) {
            System.out.println("\nOportunidades restantes: " + oportunidades);
            System.out.println(palabraOculta);

            System.out.print("Ingrese un carácter: ");
            char letra = scanner.nextLine().toUpperCase().charAt(0);

            boolean acierto = false;
            for (int i = 0; i < palabraAdivinar.length(); i++) {
                if (palabraAdivinar.charAt(i) == letra) {
                    palabraOculta[i] = letra;
                    acierto = true;
                }
            }

            if (acierto) {
                System.out.println("¡Le pegaste a un carácter!");
            } else {
                System.out.println("Ese carácter no está en la palabra.");
                oportunidades--;
            }

            palabraAdivinada = true;
            for (char c : palabraOculta) {
                if (c == '_') {
                    palabraAdivinada = false;
                    break;
                }
            }
        }

        if (palabraAdivinada) {
            System.out.println("\n¡Felicidades! Adivinaste la palabra: " + palabraAdivinar);
        } else {
            System.out.println("\nSe te acabaron las oportunidades. La palabra era: " + palabraAdivinar);
        }
    }

    private static void cambiarPalabras(Scanner scanner) {
        System.out.println("\n--- Cambiar Palabras ---");
        System.out.println("Palabras actuales:");
        for (int i = 0; i < palabras.size(); i++) {
            System.out.println((i + 1) + ". " + palabras.get(i));
        }

        System.out.println("\n¿Desea cambiar alguna palabra? (s/n)");
        String respuesta = scanner.nextLine();

        if (respuesta.equalsIgnoreCase("s")) {
            for (int i = 0; i < palabras.size(); i++) {
                System.out.print("Ingrese la nueva palabra para la posición " + (i + 1) + ": ");
                palabras.set(i, scanner.nextLine().toUpperCase());
            }
            System.out.println("Las palabras han sido actualizadas.");
        } else {
            System.out.println("No se realizaron cambios.");
        }
    }
}
