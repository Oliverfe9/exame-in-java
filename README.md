# exame-in-java

package Exame;
 import javax.swing.JOptionPane;

import javax.swing.JOptionPane;

public class Exame {
    private final String nomePaciente;
    private final String tipoSanguineo;
    private final int anoNascimento;

    public Exame(String nomePaciente, String tipoSanguineo, int anoNascimento) {
        this.nomePaciente = nomePaciente;
        this.tipoSanguineo = tipoSanguineo;
        this.anoNascimento = anoNascimento;
    }

    public String getNomePaciente() {
        return nomePaciente;
    }

    public String getTipoSanguineo() {
        return tipoSanguineo;
    }

    public int getIdade() {
        int anoAtual = java.time.Year.now().getValue();
        return anoAtual - anoNascimento;
    }

    public void classificarResultado() {
        // Implementação da classificação de resultado geral
    }

    public void mostrarResultado() {
        String message = "Exame para: " + getNomePaciente() + "\n"
                + "Tipo Sanguíneo: " + getTipoSanguineo() + "\n"
                + "Idade: " + getIdade() + " anos\n";
        
        JOptionPane.showMessageDialog(null, message);
        classificarResultado();
    }

    public static void main(String[] args) {
        Exame exame = cadastrarExame();
        exame.mostrarResultado();
    }

    public static Exame cadastrarExame() {
        String nome = JOptionPane.showInputDialog("Informe o nome do paciente:");
        String tipoSanguineo = JOptionPane.showInputDialog("Informe o tipo sanguíneo:");
        int anoNascimento = Integer.parseInt(JOptionPane.showInputDialog("Informe o ano de nascimento:"));

        String tipoExame = JOptionPane.showInputDialog("Informe o tipo de exame (G - Glicemia, C - Colesterol, T - Triglicerídeos):");

        if (tipoExame.equalsIgnoreCase("G")) {
            int quantidadeGlicose = (int) Double.parseDouble(JOptionPane.showInputDialog("Informe a quantidade de glicose por mg/l:"));
            return new Glicemia(nome, tipoSanguineo, anoNascimento, (int) quantidadeGlicose);
        } else if (tipoExame.equalsIgnoreCase("C")) {
            int quantidadeLDL = (int) Double.parseDouble(JOptionPane.showInputDialog("Informe a quantidade de LDL por mg/l:"));
            int quantidadeHDL = (int) Double.parseDouble(JOptionPane.showInputDialog("Informe a quantidade de HDL por mg/l:"));
            String risco = JOptionPane.showInputDialog("Informe o risco do paciente (B - baixo, M - medio, A - alto):");
            return new Colesterol(nome, tipoSanguineo, anoNascimento, quantidadeLDL, quantidadeHDL, risco);
        } else if (tipoExame.equalsIgnoreCase("T")) {
          double quantidadeTriglicerideo = Double.parseDouble(JOptionPane.showInputDialog("Informe a quantidade de triglicerídeo por mg/l:"));
            return new Triglicerideos(nome, tipoSanguineo, anoNascimento, (int) quantidadeTriglicerideo);
        } else {
            JOptionPane.showMessageDialog(null, "Tipo de exame inválido.");
            return null;
        }
    }
}
