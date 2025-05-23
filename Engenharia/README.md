1) A engenharia de software é intangivel sendo muito dificil para ser realizado

2) A engenhria de software necessita planejamento, nâo só programaçâo, necessita ver se, com o tempo ele poderá mudar, se ele ira crescer e/ou se tera que abdicar de alguma linguagem mais facil pra que rode melhor

3) usar uma liguagem de dificil entendimento para ter melhor rendimento no software ou usar uma linguagem facil para melhor dessenvolvimento,fazer um codigo mais abrangente mas mais lento ou codigo mais focado mas menos abrangemte,um codigo com muita seguranca mas dificil acesso ou codigo sem muita seguranca mas de facil acesso

4) e nessesario apresentar algo funcional do que partes de um codigo, faz que o cliente entenda para onde o projeto esta caminhando.

5) ```
   public class Player {
    String nome,nick;
    int kda;

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public String getNick() {
        return nick;
    }

    public void setNick(String nick) {
        this.nick = nick;
    }

    public int getKda() {
        return kda;
    }

    public void setKda(int kda) {
        this.kda = kda;
    }

    public Player(String nome, String nick, int kda) {
        this.nome = nome;
        this.nick = nick;
        this.kda = kda;
    }
    }
```
```
    public class Servidor {
        private List<Player> player = new LinkedList<Player>();
        public void addPlayer (Player player){
            this.player.add(player);
        }

        public Player buscarNick(String nick) {
                    for(Player player:player) {
                            if(player.getNick().equals(nick)) return player;
                    }
                    return null;
            }

            public List<Player> buscarNome(String nome){
                    List<Player> encontrados = new LinkedList<Player>();
                    for(Player player: player) {
                            if(player.getNome().equals(nome)) encontrados.add(player);
                    }
                    return encontrados;
            }
            public List<Player> buscarKda(int kda){
                    List<Player> encontrados = new LinkedList<Player>();
                    for(Player player: player) {
                            if(player.getKda() > kda) encontrados.add(player);
                    }
                    return encontrados;
            }
            public List<Player> getPlayers(){//met verb minus
                    return this.player;
            }
    }
```
```
    public class ServidorTest {
    
    public ServidorTest() {
    }

    @Test
    public void testSomeMethod() {
                Servidor vava = new Servidor();
		vava.addPlayer(new Player("Polo", "ryan",9));
		vava.addPlayer(new Player("Link", "kayan",19));
                vava.addPlayer(new Player("Dogoodvibes", "taylor",10));
		
		assertEquals(vava.getPlayers().size(), 3);
		
		Player p = vava.buscarNick("kayan");
		
		assertEquals(p.getNome(), "Link");
    }
    
    } 
```
