*Anti-Padrao*

    class CarrinhoDeComprasAntiPadrao {
        private double total;

        public void adicionarItem(double preco) {
            this.total += preco;
        }

        public void finalizarCompra(String tipoPagamento) {
            if (tipoPagamento.equals("PIX")) {
                System.out.println("Gerando QR Code... Valor: " + total);
                System.out.println("Aguardando confirmação do Banco Central...");
            } 
            else if (tipoPagamento.equals("CARTAO")) {
                System.out.println("Conectando com a operadora de cartão...");
                System.out.println("Cobrando R$ " + total + " no crédito.");
            } 
            else if (tipoPagamento.equals("BOLETO")) {
                System.out.println("Gerando boleto para o valor de " + total);
            }
            else {
                System.out.println("Erro: Método de pagamento inválido.");
            }
        }
    }

    public class MainAntiPadrao {
        public static void main(String[] args) {
            CarrinhoDeComprasAntiPadrao carrinho = new CarrinhoDeComprasAntiPadrao  ();
            carrinho.adicionarItem(50.0);
            carrinho.finalizarCompra("PIX");
        }
    }

*Padrão*

    interface EstrategiaPagamento {
        void pagar(double valor);
    }

    class PagamentoCartao implements EstrategiaPagamento {
        @Override
        public void pagar(double valor) {
            System.out.println("Pago R$ " + valor + " no Cartão (Crédito/Débito).");
        }
    }

    class PagamentoPix implements EstrategiaPagamento {
        @Override
        public void pagar(double valor) {
            System.out.println("Gerando QR Code... Pago R$ " + valor + " via Pix.");
        }
    }
    class CarrinhoDeCompras {
        private double total;

        public void adicionarItem(double preco) {
            this.total += preco;
        }

        public void finalizarCompra(EstrategiaPagamento metodo) {
            metodo.pagar(total);
        }
    }
    public class CafeteriaApp {
        public static void main(String[] args) {
            CarrinhoDeCompras meuCafe = new CarrinhoDeCompras();
            meuCafe.adicionarItem(15.50); // Um Cappuccino
            meuCafe.adicionarItem(8.00);  // Um Pão de Queijo

            // O cliente escolhe Pix
            meuCafe.finalizarCompra(new PagamentoPix());

            // Se o cliente mudasse de ideia e quisesse Cartão:
            // meuCafe.finalizarCompra(new PagamentoCartao());
        }
    }