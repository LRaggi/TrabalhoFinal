# TrabalhoFinal
# Classe Main
import java.util.List;
import java.util.Date;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        GerenciadorDoacoes gerenciador = new GerenciadorDoacoes();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\n===== Menu =====");
            System.out.println("1. Fazer Doação");
            System.out.println("2. Total de Doações");
            System.out.println("3. Listar Doações");
            System.out.println("4. Sair");
            System.out.print("Escolha uma opção: ");

            int opcao = scanner.nextInt();
            scanner.nextLine();  // Consumir a quebra de linha após o número

            switch (opcao) {
            
                case 1:
                    System.out.print("Selecione o tipo de doação: ");
                    System.out.println("\n1. Alimentos");
                    System.out.println("2. Medicamentos");
                    System.out.println("3. Água");
                    System.out.println("4. Ração");
                    System.out.println("5. Roupas");
                    System.out.println("6. Dinheiro");
                    String tipoStr = scanner.nextLine();
                    int tipo = Integer.parseInt(tipoStr);
                    if (tipo == 1) {
                      System.out.println("Digite o tipo de alimento e a pesagem de cada embalagem: ");
                        String alimento = scanner.nextLine();
                    }
                    if (tipo == 2) {
                        System.out.println("Digite o tipo de medicamento: ");
                        String medicamento = scanner.nextLine();
                    }
                    if (tipo == 3) {
                        System.out.println( "As garrafas devem ser apenas de um tipo de litragem. Digite o tipo de garrafa a ser doada: ");
                        String agua = scanner.nextLine();
                    }
                    if (tipo == 4) {
                        System.out.println("Digite o tipo de ração: ");
                        String racao = scanner.nextLine();
                    }
                    if (tipo == 5) {
                        System.out.println("Digite o gênero e os tipos de roupa: ");
                        String roupa = scanner.nextLine();
                    }

                    System.out.print("Digite a quantidade que deseja doar: ");
                    double quantidade = scanner.nextDouble();

                    scanner.nextLine();  // Consumir a quebra de linha após o número

                    // Neste ponto, poderia ser implementado o tratamento da data
                    Date data = new Date();

                    gerenciador.adicionarDoacao(tipoStr, quantidade, data);
                    System.out.println("Doação registrada com sucesso!");
                    break;

                case 2:
                    double total = gerenciador.calcularTotalDoacoes();
                    System.out.println("Total de doações recebidas: ");
                    double totalAlimento = 0;
                    double totalMedicamento = 0;
                    double totalAgua = 0;
                    double totalRacao = 0;
                    double totalRoupa = 0;
                    double totalDinheiro = 0;
                    for (Doacao doacao : gerenciador.getDoacoes()) {
                        if (doacao.getTipo().equals("Alimentos")) {
                            totalAlimento += doacao.getQuantidade();
                        } else if (doacao.getTipo().equals("Medicamentos")) {
                            totalMedicamento += doacao.getQuantidade();
                        } else if (doacao.getTipo().equals("Água")) {
                            totalAgua += doacao.getQuantidade();
                        } else if (doacao.getTipo().equals("Ração")) {
                            totalRacao += doacao.getQuantidade();
                        } else if (doacao.getTipo().equals("Roupas")) {
                            totalRoupa += doacao.getQuantidade();
                        } else if (doacao.getTipo().equals("Dinheiro")) {
                            totalDinheiro += doacao.getQuantidade();
                        }
                    }
                    System.out.println("1. Alimentos: " + totalAlimento);
                    System.out.println("2. Medicamentos: " + totalMedicamento);
                    System.out.println("3. Água: " + totalAgua + " Litros");
                    System.out.println("4. Ração: " + totalRacao);
                    System.out.println("5. Roupas: " + totalRoupa);
                    System.out.println("6. Dinheiro: R$" + totalDinheiro);
                    break;

                case 3:
                    List<Doacao> doacoes = gerenciador.getDoacoes();
                    System.out.println("\n===== Lista de Doações =====");
                    for (Doacao doacao : doacoes) {
                    System.out.println("Tipo: " + doacao.getTipo());
                    System.out.println("Quantidade: " + doacao.getQuantidade());
                    System.out.println("Data: " + doacao.getData());
                    System.out.println("---------------------------"); }
                    break;

                case 4:
                    System.out.println("Até a próxima!");
                    System.exit(0);
                    break;

                default:
                    System.out.println("Opção inválida. Tente novamente.");
            }
        }
    }
}
# Classe GerenciadorDoacoes
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

public class GerenciadorDoacoes {
    private List<Doacao> doacoes;

    public GerenciadorDoacoes() {
        this.doacoes = new ArrayList<Doacao>();
    }

    public void adicionarDoacao(String tipo, double quantidade, Date data) {
        Doacao novaDoacao = new Doacao(tipo, quantidade, data);
        doacoes.add(novaDoacao);
    }

    public double calcularTotalDoacoes() {
        double totalAlimento = 0;
        double totalMedicamento = 0;
        double totalAgua = 0;
        double totalRacao = 0;
        double totalRoupa = 0;
        double totalDinheiro = 0;
        for (Doacao doacao : this.doacoes) {
            if (doacao.getTipo().equals("Alimentos")) {
                totalAlimento += doacao.getQuantidade();
            } else if (doacao.getTipo().equals("Medicamentos")) {
                totalMedicamento += doacao.getQuantidade();
            } else if (doacao.getTipo().equals("Água")) {
                totalAgua += doacao.getQuantidade();
            } else if (doacao.getTipo().equals("Ração")) {
                totalRacao += doacao.getQuantidade();
            } else if (doacao.getTipo().equals("Roupas")) {
                totalRoupa += doacao.getQuantidade();
            } else if (doacao.getTipo().equals("Dinheiro")) {
                totalDinheiro += doacao.getQuantidade();
            }
        }
         double total = totalAlimento + totalMedicamento + totalAgua + totalRacao + totalRoupa + totalDinheiro;
        return total;
        
    }

    public List<Doacao> getDoacoes() {
        return doacoes;
    }
}
# Classe Doacao
import java.util.Date;

public class Doacao {
    private String tipo;
    private double quantidade;
    private Date data;

    public Doacao(String tipo, double quantidade, Date data) {
        this.tipo = tipo;
        this.quantidade = quantidade;
        this.data = data;
    }

    // Getters
    public String getTipo() {
        return tipo;
    }

    public double getQuantidade() {
        return quantidade;
    }

    public Date getData() {
        return data;
    }
}
