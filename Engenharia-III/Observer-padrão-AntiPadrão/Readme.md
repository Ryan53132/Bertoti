*Anti-padrão*
'''

class EmailService {
    public void enviarEmailConfirmacao(String mensagem) {
        System.out.println(mensagem);
    }
}

class LogService {
    public void gerarLogNoSistema(String info) {
        System.out.println(info);
    }
}


class Estoque {
    private int quantidade;
    private EmailService emailService = new EmailService();
    private LogService logService = new LogService();

    public void setQuantidade(int novaQuantidade) {
        this.quantidade = novaQuantidade;
        // O "Sujeito" chama manualmente cada dependência específica
        emailService.enviarEmail("Estoque alterado para: " + novaQuantidade);
        logService.registrarLog("Mudança no estoque detectada.");
    }
}
'''
*Padrão*
'''
import java.util.ArrayList;
import java.util.List;

interface Observer {
    void update(int quantidade);
}

class EmailAlert implements Observer {
    public void update(int q) { System.out.println("Email: Estoque é " + q); }
}

class Logger implements Observer {
    public void update(int q) { System.out.println("Log: Registrado " + q); }
}

class EstoqueSubject {
    private List<Observer> observers = new ArrayList<>();
    private int quantidade;

    public void registrar(Observer o) { observers.add(o); }
    
    public void setQuantidade(int novaQuantidade) {
        this.quantidade = novaQuantidade;
        notificarTodos();
    }

    private void notificarTodos() {
        for (Observer o : observers) {
            o.update(quantidade);
        }
    }
}
'''