import java.util.Scanner;

public class CalculoVendaSanduiches {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        double valorMaisCaro = 0;
        double totalVendido = 0;

        while (true) {
            System.out.print("Digite o nome do sanduíche (ou 'fim' para encerrar): ");
            String nomeSanduiche = input.nextLine();

            if (nomeSanduiche.equalsIgnoreCase("fim")) {
                break;
            }

            System.out.print("Digite o valor do sanduíche: ");
            double valorSanduiche = input.nextDouble();
            input.nextLine();  // Limpar o buffer do teclado

            totalVendido += valorSanduiche;

            if (valorSanduiche > valorMaisCaro) {
                valorMaisCaro = valorSanduiche;
            }
        }

        input.close();
        
        System.out.println(valorMaisCaro);
        System.out.println(totalVendido);
    }
}

