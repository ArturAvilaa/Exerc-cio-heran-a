#exercicio1

abstract class Progressao {
    protected long atual;

    public Progressao(long inicio) {
        this.atual = inicio;
    }
    public abstract long proximo();

    public void reiniciar() {
        atual = inicio();
    }
    protected abstract long inicio();
}
class ProgressaoAritmetica extends Progressao {
    private final long passo;

    public ProgressaoAritmetica(long inicio, long passo) {
        super(inicio);
        this.passo = passo;
    }
    @Override
    public long proximo() {
        long proximoValor = atual;
        atual += passo;
        return proximoValor;
    }
    @Override
    protected long inicio() {
        return 0;
    }
}
class ProgressaoGeometrica extends Progressao {
    private final long razao;

    public ProgressaoGeometrica(long inicio, long razao) {
        super(inicio);
        this.razao = razao;
    }
    @Override
    public long proximo() {
        long proximoValor = atual;
        atual *= razao;
        return proximoValor;
    }
    @Override
    protected long inicio() {
        return 1;
    }
}
class ProgressaoFibonacci extends Progressao {
    private long anterior;
    private long proximo;
    public ProgressaoFibonacci() {
        super(0);
        this.anterior = 0;
        this.proximo = 1;
    }
    @Override
    public long proximo() {
        long proximoValor = atual;
        atual = proximo;
        proximo += anterior;
        anterior = atual - anterior;
        return proximoValor;
    }

    @Override
    protected long inicio() {
        return 0;
    }
}
public class Main {
  
public static void main(String[] args) {
        Progressao aritmetica = new ProgressaoAritmetica(2, 3);
        Progressao geometrica = new ProgressaoGeometrica(2, 3);
        Progressao fibonacci = new ProgressaoFibonacci();

        // Testando as progressões
        System.out.println("Progressão Aritmética:");
        for (int i = 0; i < 11; i++) {
            System.out.println(aritmetica.proximo());
        }
        aritmetica.reiniciar();

        System.out.println("Progressão Geométrica:");
        for (int i = 0; i < 11; i++) {
            System.out.println(geometrica.proximo());
        }
        geometrica.reiniciar();

        System.out.println("Sequência de Fibonacci:");
        for (int i = 0; i <11; i++) {
            System.out.println(fibonacci.proximo());
        }
    }
}

#exercicio2

abstract class RetanguloDecorator {
    protected String texto;

    public RetanguloDecorator(String texto) {
        this.texto = texto;
    }

    public abstract void desenhar();
}

class RetanguloBordasArredondadas extends RetanguloDecorator {
    public RetanguloBordasArredondadas(String texto) {
        super(texto);
    }

    @Override
    public void desenhar() {
        System.out.println("╭───────────────╮");
        System.out.println("│               │");
        System.out.println("│   " + texto + "   │");
        System.out.println("│               │");
        System.out.println("╰───────────────╯");
    }
}

class RetanguloLinhasDuplas extends RetanguloDecorator {
    public RetanguloLinhasDuplas(String texto) {
        super(texto);
    }

    @Override
    public void desenhar() {
        System.out.println("╔═══════════════╗");
        System.out.println("║               ║");
        System.out.println("║   " + texto + "   ║");
        System.out.println("║               ║");
        System.out.println("╚═══════════════╝");
    }
}

class RetanguloASCIIArt extends RetanguloDecorator {
    public RetanguloASCIIArt(String texto) {
        super(texto);
    }

    @Override
    public void desenhar() {
        System.out.println("   /¯¯¯¯¯¯¯¯¯¯¯¯¯\\");
        System.out.println("  |               |");
        System.out.println("  |   " + texto + "   |");
        System.out.println("  |               |");
        System.out.println("   \\_____________/");
    }
}

class RetanguloColorido extends RetanguloDecorator {
    public RetanguloColorido(String texto) {
        super(texto);
    }

    @Override
    public void desenhar() {
        System.out.println("\u001B[44m\u001B[30m███\u001B[0m");
        System.out.println("\u001B[44m\u001B[30m█\u001B[0m " + texto + " \u001B[44m\u001B[30m█\u001B[0m");
        System.out.println("\u001B[44m\u001B[30m███\u001B[0m");
    }
}

public class Main {
    public static void main(String[] args) {
        RetanguloDecorator retangulo1 = new RetanguloBordasArredondadas("Retângulo com bordas arredondadas");
        RetanguloDecorator retangulo2 = new RetanguloLinhasDuplas("Retângulo com linhas duplas");
        RetanguloDecorator retangulo3 = new RetanguloASCIIArt("Retângulo com ASCII art");
        RetanguloDecorator retangulo4 = new RetanguloColorido("Retângulo colorido");

        retangulo1.desenhar();
        System.out.println();
        retangulo2.desenhar();
        System.out.println();
        retangulo3.desenhar();
        System.out.println();
        retangulo4.desenhar();
    }
}
