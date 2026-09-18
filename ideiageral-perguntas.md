# Aula 1

## O que você precisa guardar desta aula

As ideias centrais da aula estão organizadas nos pontos abaixo para facilitar a sua revisão:

* **Convergência Tecnológica:** As redes surgiram da união entre telecomunicações e computação digital.
* **Digitalização Universal:** Voz, texto, imagem e vídeo podem ser representados por bits.
* **Protocolos:** Regras fundamentais que determinam como a comunicação acontece entre os dispositivos.
* **Padrões:** Normas que permitem que equipamentos de fabricantes diferentes sejam compatíveis entre si.
* **Modularidade (Camadas):** A comunicação é dividida em camadas para reduzir a complexidade do sistema.
* **Escala de Redes:** **LAN** (*Local Area Network*) é uma rede local; **WAN** (*Wide Area Network*) cobre distâncias maiores e geograficamente dispersas.
* **Fronteira de Rede:** O **roteador de borda** conecta uma LAN a outras redes externas.
* **Modelo de Comutação da Internet:** A Internet utiliza principalmente a **comutação de pacotes**.
* **Comutação de Circuitos:** Modelo em que os recursos de rede ficam totalmente reservados durante toda a sessão (ex: telefonia tradicional).
* **Definição da Internet:** A Internet é uma imensa interligação de redes independentes que utilizam protocolos compatíveis.


## Perguntas rápidas para conferir se entendeu

1. Por que computadores antigos de fabricantes diferentes não conseguiam se comunicar? usavam diferentes padroes e protocolos de comunicacao
2. Qual é a diferença entre um protocolo e um padrão? protocolo é uma regra que determina a comunicacao entre dispositivos. padrão são normas que permitem que comunicacao acontececa entre disponsitivos de diferetnes fabricantes 
3. Por que dividir a comunicação em camadas? Dividir a comunicação em camadas reduz a complexidade ao separar um problema grande em partes menores e independentes. Isso facilita a organização e a manutenção, permitindo atualizar ou consertar uma parte da rede sem precisar alterar o sistema inteiro.
4. Qual equipamento normalmente marca a fronteira entre uma LAN e uma WAN? roteador de borda
5. Qual é a diferença principal entre comutação de circuitos e de pacotes? a comutacao de circutos primeiro ouve o caminho ate o destino e bloqueia ele para qualquer outro tipo de comunicacao durante sua transmissao, a comunicacao de pacotes nao pega a rede para si e pode tomar diferentes caminhos ao longo do caminho e é divida em pacotes que nao necessariamente chegam em ordem. 
6. Por que a comutação de pacotes aproveita melhor a infraestrutura?orque ela permite que vários usuários compartilhem a mesma infraestrutura ao mesmo tempo, utilizando os recursos da rede apenas no momento em que há dados sendo transmitidos (evitando o desperdício de espaço ocioso), além de permitir o roteamento dinâmico pelos melhores caminhos disponíveis.
7. O que significa dizer que a Internet é uma “rede de redes”?Significa que a Internet não é uma rede única, mas sim a união de milhares de redes menores e independentes. Elas se conectam e trocam dados entre si porque todas seguem os mesmos protocolos de comunicação.

# Aula 2 
## O essencial 

* O modelo OSI divide a comunicação em sete camadas.
* Cada camada resolve uma parte específica do problema.
* A camada física transmite bits por sinais.
* O enlace organiza a comunicação local em quadros.
* A rede usa endereçamento e roteamento para alcançar outras redes.
* O transporte realiza a comunicação de ponta a ponta entre aplicações.
* Sessão e apresentação possuem funções que, no TCP/IP, geralmente ficam na aplicação.
* A aplicação determina o que precisa ser comunicado.
* A Internet utiliza a família TCP/IP, enquanto o OSI funciona principalmente como modelo de referência.
* Os dados sofrem encapsulamento na origem e desencapsulamento no destino.
* A sequência mais importante é:
  `Dados → Segmento → Pacote → Quadro → Bits`


## Perguntas para conferir seu entendimento

1. Por que é vantajoso dividir a comunicação em camadas?
2. Qual é a diferença entre camada física e camada de enlace?
A camada física transmite os bits brutos transformando-os em sinais físicos (como eletricidade ou luz) pelo meio de transmissão. A camada de enlace organiza esses bits em quadros para gerenciar a comunicação local entre dispositivos vizinhos.
3. Qual é a diferença entre enlace e transporte em relação à confiabilidade?
A camada de enlace lida com a confiabilidade e entrega dos dados apenas localmente (entre dispositivos conectados na mesma rede ou salto direto). Já a camada de transporte garante a confiabilidade de ponta a ponta (end-to-end), assegurando que a mensagem inteira chegue corretamente do aplicativo na origem até o aplicativo no destino, mesmo que passem por várias redes diferentes no meio do caminho.

4. Qual camada escolhe o caminho até outra rede?
5. Por que a camada de sessão não foi mantida separadamente no TCP/IP?
6. Qual é a diferença entre HTTP e um navegador?
navegador é a ferramenta que o usuário utilizar para acessar paginas web; http é o protocolo que o navegador usa para conversar com o servidor. 
7. O que acontece durante o encapsulamento?
8. Qual é a diferença entre segmento, pacote e quadro?
9. Onde HTTP, TCP, IP e Ethernet são aproximadamente implementados?
10. O OSI é a arquitetura efetivamente utilizada pela Internet ou um modelo de referência?

# Aula 3 — O Padrão Ethernet

## O que você precisa guardar desta aula

- **Ethernet:** família de tecnologias para redes locais; padrão IEEE 802.3.
- **Camadas:** atua no enlace (L2) e define aspectos físicos (L1).
- **Barramento:** na Ethernet antiga, máquinas compartilhavam o cabo e podiam ocorrer colisões.
- **CSMA/CD:** escuta o meio, detecta colisões e permite novas tentativas após espera aleatória.
- **Switches:** interligam dispositivos e encaminham quadros conforme a tabela MAC.
- **Aprendizado:** o switch aprende pelo MAC de origem e encaminha pelo MAC de destino.
- **Flooding:** destino desconhecido provoca replicação nas demais portas da VLAN.
- **Endereço MAC:** identifica uma interface no enlace; possui 6 bytes ou 48 bits.
- **Quadro Ethernet:** contém MACs, tipo, dados e FCS; preâmbulo e SFD precedem o quadro.
- **Payload:** normalmente transporta um pacote IP; limite usual de 1500 bytes.
- **Padding:** preenchimento para atingir o tamanho mínimo.
- **CRC/FCS:** detectam erros; não corrigem nem criptografam os dados.
- **Full-duplex:** permite enviar e receber simultaneamente, sem colisões tradicionais.
- **Prazos:** eliminar colisões não elimina filas, atrasos ou perdas.
- **Redes industriais:** podem exigir garantias temporais; utilizam mecanismos como TSN.

## Perguntas para conferir seu entendimento

1. O que é Ethernet e em quais camadas ela atua?
2. Por que ocorriam colisões na Ethernet em barramento?
3. Como funciona o CSMA/CD?
4. O que mudou com switches e enlaces full-duplex?
5. Como o switch aprende qual MAC está acessível por cada porta?
6. O que acontece quando o MAC de destino é conhecido? E quando é desconhecido?
7. Qual é a diferença entre flooding e um quadro broadcast?
8. Quem atribui o MAC e quantos bits ele possui?
9. Quais são os campos da transmissão Ethernet e suas funções?
10. Qual é a diferença entre payload e tamanho total do quadro?
11. Para que serve o padding?
12. Qual é a diferença entre CRC e FCS? Eles garantem a entrega?
13. Por que uma Ethernet sem colisões ainda pode apresentar atrasos?
14. Como a passagem de token controla quem pode transmitir?

# Aula 4 — A Internet

## O que você precisa guardar desta aula

- **Internet:** interligação de redes físicas diferentes por protocolos compatíveis.
- **TCP/IP:** família de protocolos; IP atua na rede (L3), TCP no transporte (L4).
- **Sistemas autônomos:** redes participantes sob administração própria.
- **Endereço IP:** identificação lógica de uma interface; base do roteamento.
- **NET-ID e HOST-ID:** identificam a rede e a interface dentro dela.
- **DNS:** associa nomes simbólicos a endereços e outros registros.
- **IPv4:** 32 bits; quatro octetos decimais entre 0 e 255.
- **IPv6:** 128 bits; espaço de endereçamento muito maior.
- **Classes históricas:** A, B e C dividiam rede e host em tamanhos fixos; D identifica multicast; E é reservada/experimental.
- **CIDR:** permite prefixos flexíveis; substituiu o endereçamento baseado em classes.
- **Destinatários:** unicast é um para um; broadcast, um para todos no domínio local; multicast, um para um grupo.
- **Endereços especiais:** em sub-redes tradicionais, HOST-ID zerado identifica a rede; todos os bits em 1 identificam o broadcast.
- **Loopback:** `127.0.0.1` representa a própria máquina; não sai pela rede física.
- **Ordem de rede:** campos numéricos multibyte tradicionais utilizam big endian.
- **Backbones:** infraestruturas de alta capacidade que interligam redes.

## Perguntas para conferir seu entendimento

1. Por que a Internet é chamada de “rede de redes”?
2. Como TCP/IP permite comunicar entre tecnologias físicas diferentes?
3. Qual é a diferença entre endereço MAC, endereço IP e nome DNS?
4. O que um endereço IP identifica? Uma máquina pode ter vários IPs?
5. Para que servem NET-ID e HOST-ID?
6. Quantos bits possuem IPv4 e IPv6?
7. Por que o IPv6 foi desenvolvido e por que a transição é complexa?
8. Como as classes A, B e C dividiam rede e host?
9. Por que não devemos determinar a máscara atual apenas pela classe histórica?
10. Qual é a diferença entre unicast, broadcast e multicast?
11. Na rede `200.17.202.0/24`, quais são o endereço da rede, o broadcast e o intervalo de hosts?
12. Quantos endereços totais e quantos endereços utilizáveis existem nessa rede?
13. Para que serve `127.0.0.1`? Seus dados passam pelo switch?
14. Qual é a diferença entre big endian e little endian?
15. O que é um backbone e por que ele precisa de capacidade e redundância?

# Aula 5 — O Protocolo ARP

## O essencial

- **Compartilhamento:** redes permitem compartilhar recursos e reduzir custos.
- **Multicast:** entrega dados a um grupo.
- **CDN:** aproxima conteúdo dos usuários; **nuvem:** oferece recursos sob demanda.
- **ARP:** descobre o MAC associado a um IPv4 local; não calcula um pelo outro.
- **IP e MAC:** IP orienta o roteamento; MAC permite a entrega local.
- **Request (1):** pergunta pelo MAC, normalmente em broadcast (`FF:FF:FF:FF:FF:FF`).
- **Reply (2):** informa o MAC, normalmente em unicast ao solicitante.
- **Cache ARP:** guarda associações IP → MAC temporariamente; consultável com `arp -a`.
- **Destino local:** procura o MAC do destinatário. **Remoto:** procura o MAC do gateway.
- **Próximo salto:** cada roteador encaminha o pacote pelo enlace seguinte.
- **Encapsulamento:** ARP vai diretamente no quadro Ethernet, não dentro de IP.
- **EtherType:** `0x0806` indica ARP; `0x0800`, IPv4.
- **Campos ARP:** tipos, tamanhos, operação e endereços MAC/IP do remetente e do alvo.
- **Tabelas:** ARP associa IP → MAC; switch associa MAC → porta física.

## Perguntas para conferir seu entendimento

1. Quais vantagens o compartilhamento de recursos traz para uma rede?
  Reduz custos, diminui a duplicação de infraestrutura e facilita a manutenção, permitindo que vários usuários acessem o mesmo hardware (processamento e memória), softwares e arquivos remotamente.

2. Como multicast evita enviar uma cópia independente para cada destinatário? Em vez de a origem enviar múltiplos pacotes duplicados, ela envia apenas uma cópia. A própria rede (os roteadores/switches) se encarrega de replicar o pacote nos pontos onde os caminhos se dividem para alcançar os interessados.

3. Para que serve uma CDN? O que a nuvem oferece sob demanda?
CDN (Content Delivery Network): Distribui servidores geograficamente para entregar conteúdos aos usuários a partir do ponto mais próximo, reduzindo a latência e aliviando a origem. Nuvem: Oferece processamento, armazenamento e redes de forma elástica e paga conforme o uso, sem necessidade de infraestrutura local.

4. Por que conhecer o IP não basta para montar um quadro Ethernet destinado a outro computador? O IP identifica o destino final na camada de rede, mas a placa de rede precisa do endereço físico (MAC) para entregar o quadro diretamente no enlace local (camada de enlace).

5. Para que serve o ARP? É possível calcular o MAC a partir do IP?

6. Qual é a diferença entre ARP Request e ARP Reply?

7. Por que o Request normalmente usa broadcast? Qual MAC representa esse broadcast?

8. Quem deve responder à pergunta “Quem tem este IP?”?
Apenas a máquina (host ou roteador) que possui o endereço IP solicitado.

9. O Reply normalmente é enviado a todos ou apenas ao solicitante?

10. O que o cache ARP armazena? Por que suas entradas são temporárias? Armazena: Mapeamentos do tipo IPv4 → MAC. Motivo de ser temporário: Interfaces e IPs podem mudar com o tempo. Se fosse permanente, o cache guardaria informações desatualizadas, impedindo a comunicação.

11. Se a associação já estiver no cache, é necessário enviar outro Request? N

12. Qual é a diferença entre o cache ARP e a tabela de encaminhamento do switch?

13. Se o destino estiver na mesma rede, qual MAC o computador procura?

14. Se o destino estiver em outra rede, qual MAC o computador procura? Por quê? 

15. Sem NAT, ao enviar para outra rede, o IP de destino é o do servidor remoto ou o do gateway? O IP de destino é o do servidor remoto (o destino final). O que muda para o Gateway no nível do enlaçe é o MAC de destino, não o IP.

16. Uma mensagem ARP fica dentro de um pacote IP ou diretamente no quadro Ethernet? 

17. Qual é a diferença entre o EtherType do quadro e o campo de tipo de protocolo dentro da mensagem ARP?

18. Quais endereços aparecem em uma mensagem ARP? O que indicam os códigos de operação `1` e `2`?


# Aula 6 — Introdução ao Roteamento IP

## O que você precisa guardar desta aula

- **ARP:** descobre o MAC associado a um IPv4 local.
- **RARP:** obtinha o próprio IP a partir do MAC; usado em máquinas sem disco, hoje obsoleto.
- **DHCP:** fornece automaticamente IP e outras configurações de rede.
- **IP:** atua na camada de rede (L3) e permite o encaminhamento de pacotes.
- **Roteamento:** determina caminhos; protocolos como OSPF, RIP e BGP ajudam a construir as tabelas.
- **Encaminhamento:** consulta a tabela para decidir por onde enviar cada pacote.
- **Não confiável:** IP não garante entrega nem ordem e não retransmite dados perdidos.
- **Sem conexão:** IP não estabelece uma sessão; pacotes são encaminhados individualmente.
- **Confiabilidade nas pontas:** TCP ou a aplicação controlam perdas, duplicações e ordem.
- **Roteamento hierárquico:** rotas usam prefixos de redes, evitando uma entrada por computador.
- **Mesmo computador:** comunicação local por loopback; não sai pela placa de rede.
- **Mesma rede:** entrega direta, usando o MAC do destinatário.
- **Outra rede:** entrega ao gateway, usando o MAC da interface local dele.
- **IP e MAC:** IP identifica o destino final; MAC identifica quem recebe o quadro no enlace atual.
- **Sem NAT:** os IPs de origem e destino permanecem; novos quadros são montados entre enlaces.
- **Próximo salto:** cada roteador escolhe apenas o próximo passo com sua tabela local.
- **Rota padrão:** usada quando nenhuma rota mais específica corresponde ao destino.
- **Caminhos:** ida e volta podem ser diferentes; múltiplos caminhos e loops são possíveis.
- **Comandos:** `ip route show` consulta rotas; `tcpdump` observa pacotes; `nc` envia ou recebe dados.

## Perguntas para conferir seu entendimento
 1. Qual é a diferença entre ARP, RARP e DHCP?
* **ARP:** Descobre o **MAC** a partir de um IP conhecido.
* **RARP:** Descobre o **IP** a partir de um MAC conhecido (tecnologia antiga que descobria apenas o IP).
* **DHCP:** Configura automaticamente o **IP, máscara de rede, gateway e servidor DNS** de forma completa.



 2. Como uma máquina sem IP configurado conseguia fazer uma requisição RARP?
A máquina enviava um quadro Ethernet usando seu próprio **MAC como origem** e o endereço de broadcast (`FF:FF:FF:FF:FF:FF`) como destino. O servidor RARP recebia esse pacote, consultava sua tabela interna e respondia enviando o IP correspondente diretamente para aquele MAC.



 3. Qual é a diferença entre roteamento e encaminhamento?
* **Roteamento:** É o **planejamento** (o processo de construir a tabela/mapa com os melhores caminhos na rede).
* **Encaminhamento:** É a **ação local** (o ato de pegar um pacote na interface de entrada e movê-lo para a interface de saída correta).



 4. O que significa dizer que IP é não confiável e não orientado à conexão?
* **Não confiável:** O protocolo não garante que o pacote vai chegar ao destino, nem que chegará sem erros ou sem duplicatas.
* **Não orientado à conexão:** Envia os pacotes diretamente, sem antes avisar, negociar ou estabelecer uma sessão prévia com o receptor.



 5. Por que pacotes podem chegar fora de ordem? Quem controla essa situação?
* **Por quê:** Os pacotes são tratados de forma independente e podem seguir caminhos/rotas diferentes ou enfrentar atrasos variáveis na rede.
* **Quem controla:** As camadas superiores do destinatário, principalmente o protocolo **TCP**.



 6. Como o prefixo permite identificar a rede de destino?
O prefixo/máscara de rede (ex: `/24`) divide o endereço IP em duas partes: os bits iniciais identificam a **rede**, enquanto os bits finais identificam o **host** (dispositivo específico) dentro dessa rede.



 7. Quais são os três casos de comunicação apresentados na aula?
1. **Host para Host:** Comunicação direta entre computadores na mesma rede local.
2. **Host para Roteador:** Quando um computador envia um pacote para o gateway para acessar outra rede.
3. **Roteador para Roteador:** Encaminhamento intermediário entre roteadores ao longo do caminho até a rede final.



 8. Ao acessar `localhost:3000`, os dados passam pelo roteador?
**Não.** O endereço `localhost` (`127.0.0.1`) é processado internamente na interface de *loopback* do próprio sistema operacional, sem sequer sair da placa de rede.



 9. Qual MAC é usado para enviar a um destino local? E a um destino remoto?
* **Destino local:** O MAC da **própria máquina de destino**.
* **Destino remoto:** O MAC do **Roteador/Gateway** da rede local.



 10. Sem NAT, quais endereços permanecem e quais mudam entre enlaces?
* **Permanecem iguais:** Os endereços **IP** de origem e de destino.
* **Mudam a cada enlace:** Os endereços **MAC** de origem e de destino.



 11. O que uma tabela de roteamento informa? Para que serve a rota padrão?
* **Tabela de roteamento:** Mapeia redes de destino aos seus respectivos próximos saltos (*gateways*) ou interfaces de saída.
* **Rota Padrão (`0.0.0.0/0`):** Serve como destino coringa para enviar qualquer tráfego que não coincida com nenhuma rota específica da tabela (a saída para a internet).



 12. Cada roteador escolhe o caminho inteiro ou apenas o próximo salto?
Cada roteador escolhe **apenas o próximo salto** (*hop-by-hop*), delegando a decisão do restante do trajeto aos roteadores seguintes.



 13. Por que os caminhos de ida e volta podem ser diferentes? O que é um loop?
* **Caminhos diferentes (Assimetria):** Porque as tabelas de roteamento dos dispositivos de ida e de volta são independentes e podem calcular as melhores rotas usando critérios diferentes.
* **Loop:** Ocorre quando erros de configuração ou sincronização fazem com que um pacote fique circulando infinitamente entre os mesmos roteadores sem nunca chegar ao destino.

14. Como as tabelas são preenchidas e qual é o papel dos protocolos de roteamento?
* **Preenchimento:** Pode ser feito de forma **estática** (configurado manualmente pelo administrador) ou **dinâmica** (atualizado por software).
* **Papel dos protocolos (ex: OSPF, BGP):** Trocar informações automaticamente entre os roteadores para descobrir redes, recalcular caminhos em caso de falhas e manter as tabelas atualizadas.



# Aula 7 — Manipulação de Endereços IP (Parte 1)

## O que você precisa guardar desta aula

- **Problema inicial:** uma organização pode ter várias redes físicas, mas querer utilizar um único bloco de endereços IP.
- **Economia de endereços:** dividir um bloco evita solicitar um bloco público diferente para cada rede física - **Tabelas de roteamento** 
- **Proxy:** entidade intermediária que recebe uma comunicação e a encaminha ao destino.
- **Proxy ARP:** permite que computadores em redes físicas diferentes se comportem como se estivessem na mesma rede IP.
- **Resposta do Proxy ARP:** o roteador responde à consulta ARP em nome do destino, informando seu próprio MAC.
- **Limitações do Proxy ARP:** exige controle dos endereços, pode causar conflitos e não é muito escalável.
- **Sub-redes:** dividem um bloco IP em redes menores, normalmente conectadas por roteadores.
- **Roteamento interno:** computadores de sub-redes diferentes enviam os pacotes ao gateway.
- **Máscara de sub-rede:** indica quais bits pertencem à rede e quais pertencem ao host.
- **Bits da máscara:** `1` representa rede; `0` representa host.
- **Empréstimo de bits:** bits que identificavam hosts passam a identificar sub-redes.
- **Quantidade de sub-redes:** com `n` bits adicionais, podem ser criadas `2ⁿ` sub-redes.
- **Capacidade da sub-rede:** com `h` bits de host, existem `2ʰ` endereços no total.
- **Endereços tradicionais:** o primeiro identifica a sub-rede; o último é o broadcast.
- **Prefixos:** `/24` equivale a `255.255.255.0`; `/26` equivale a `255.255.255.192`.
- **Exemplo da aula:** dividir um `/24` em `/26` utiliza dois bits adicionais e produz quatro sub-redes.
- **Exemplo de IP:** `192.39.100.86/26` pertence à sub-rede `192.39.100.64/26`.
- **Host-ID do exemplo:** `86 − 64 = 22`; portanto, é o host 22 dessa sub-rede.
- **Broadcast do exemplo:** a sub-rede `192.39.100.64/26` possui broadcast `192.39.100.127`.
- **Cálculo da rede:** o endereço da sub-rede é obtido realizando `IP AND máscara`.
- **Limitação:** Proxy ARP e sub-redes não criam novos IPv4; ajudam a aproveitar melhor um bloco existente.
- **Uso atual:** as classes são históricas; atualmente, as redes são definidas por prefixos CIDR.

## Perguntas para conferir seu entendimento

1. Qual problema o Proxy ARP e as sub-redes procuram resolver?

2. Por que solicitar um bloco para cada rede física pode causar desperdício?

3. O que é uma entidade proxy?

4. Como o Proxy ARP permite a comunicação entre duas redes físicas?

5. Por que o computador recebe o MAC do roteador quando pergunta pelo IP do destino?

6. No Proxy ARP, qual é o IP de destino do pacote enviado ao roteador?

7. Quais são as principais limitações do Proxy ARP?

8. Qual é a diferença entre Proxy ARP e sub-redes?

9. Para que serve uma máscara de sub-rede?

10. O que representam os bits `1` e `0` da máscara?

11. O que significa “emprestar bits do HOST-ID”?

12. Quantas sub-redes podem ser criadas com dois, três ou quatro bits adicionais?

13. Por que criar mais sub-redes reduz a quantidade de hosts em cada uma?

14. Quantos endereços totais e utilizáveis existem em uma sub-rede `/26`?

15. Quais são as quatro sub-redes obtidas ao dividir `192.39.100.0/24` em `/26`?

16. A qual sub-rede pertence o IP `192.39.100.86/26`?

17. Quais são o endereço da rede, o intervalo utilizável e o broadcast dessa sub-rede?

18. Como o operador AND entre o IP e a máscara encontra o endereço da rede?

19. Proxy ARP e sub-redes aumentam a quantidade total de endereços IPv4?

20. Por que atualmente usamos CIDR em vez das classes A, B e C?