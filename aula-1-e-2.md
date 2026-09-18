# Redes de Computadores — Resumo das Aulas 1 e 2

> Baseado nos slides do Prof. Giovanni Venâncio (UFPR), com esclarecimentos sobre quadros e TLS.

## Aula 1 — Introdução às Redes de Computadores

### 1. Origem e digitalização

- **Rede de computadores:** dispositivos conectados para trocar informações e compartilhar recursos.
- Surgiu da união de **telecomunicações** (comunicação a distância por sinais) com **computação digital**.
- Evolução: telégrafo → telefone → interligação de computadores → Internet.
- Voz, texto, imagens e vídeos são representados por **bits**, transmitidos por sinais elétricos, luminosos ou de rádio.
- A digitalização permite **compressão**, **criptografia**, **detecção/correção de erros** e otimização da comunicação.

### 2. Protocolos e padrões

- **Protocolo:** regras de comunicação; define formato das mensagens (**sintaxe**), significado (**semântica**) e ordem/momento das ações (**sincronização**).
- **Padrão:** especificação formal publicada para permitir implementações compatíveis.
- Redes proprietárias causavam **vendor lock-in**: dependência de um fabricante.
- Padrões abertos favorecem **interoperabilidade**, concorrência e redução de custos. Exemplo: Ethernet.
- **ISO:** organização responsável pelo modelo OSI.
- **IETF:** desenvolve e padroniza protocolos da Internet.
- **RFC:** documento técnico público e numerado; nem toda RFC é um padrão.

### 3. Internet e camadas

- **ARPANET:** precursora da Internet; adotou TCP/IP em 1983.
- **Internet:** interligação de redes que usam a família de protocolos TCP/IP.
- As **camadas** dividem a comunicação em responsabilidades menores, facilitando desenvolvimento, manutenção e substituição de tecnologias.
- Cada camada **usa serviços da inferior** e **oferece serviços à superior**.

### 4. Tipos de redes

| Tipo | Abrangência | Exemplo |
|---|---|---|
| **PAN** — pessoal | Dispositivos próximos | Celular e fone Bluetooth |
| **LAN** — local | Casa, escritório ou laboratório | Rede do DINF |
| **MAN** — metropolitana | Cidade ou região metropolitana | Interligação de unidades na cidade |
| **WAN** — longa distância | Cidades, países ou continentes | Redes de operadoras |

- O **roteador de borda** conecta a LAN a redes externas.
- Cobertura e administração ajudam na classificação; uma WAN também pode ser privada.
- **Broadcast:** envio a todos de um domínio de broadcast, não à Internet inteira.
- **Enlace ponto a ponto:** conecta dois participantes.

### 5. Comutação de circuitos e pacotes

| Circuitos | Pacotes |
|---|---|
| Estabelece um circuito antes da comunicação. | Divide os dados em unidades transmitidas pela rede. |
| Reserva capacidade durante toda a sessão. | Compartilha capacidade entre comunicações. |
| Pode desperdiçar capacidade durante a ociosidade. | Aproveita bem tráfego intermitente. |
| Exemplo: telefonia tradicional. | Exemplo: Internet. |

- Na comutação de pacotes, podem ocorrer **filas, perdas e chegada fora de ordem**.
- Pacotes podem seguir caminhos diferentes; a recuperação de perdas depende dos protocolos utilizados.

## Aula 2 — O Modelo ISO/OSI

### 1. As sete camadas

- **OSI — Open Systems Interconnection:** modelo de referência de sete camadas, publicado em 1984.
- As camadas são divisões lógicas de funções, não necessariamente programas separados.

| Nº | Camada | Responsabilidade principal |
|---:|---|---|
| 7 | **Aplicação** | Protocolos dos serviços usados pelas aplicações. |
| 6 | **Apresentação** | Representação, conversão, compressão e criptografia dos dados. |
| 5 | **Sessão** | Organização do diálogo e pontos de sincronização. |
| 4 | **Transporte** | Comunicação de ponta a ponta entre processos. |
| 3 | **Rede** | Endereçamento, encaminhamento e roteamento. |
| 2 | **Enlace** | Quadros, comunicação local e acesso ao meio. |
| 1 | **Física** | Transmissão dos bits por sinais. |

### 2. Física

- Define sinais, temporização, meios, conectores e interfaces.
- **Cobre:** sinais elétricos; **fibra:** luz; **Wi-Fi:** rádio.
- Não interpreta o conteúdo dos bits.
- **MHz:** frequência; **Mbps/Gbps:** taxa de bits. São grandezas diferentes.
- Categoria do cabo, distância e tecnologia influenciam a taxa suportada.

### 3. Enlace e quadros

- **Enlace = link:** comunicação local entre participantes de um enlace.
- **Quadro (frame):** unidade de dados da camada de enlace.
- Exemplo simplificado de um quadro Ethernet:

| Cabeçalho | Dados | FCS |
|---|---|---|
| MAC de destino, MAC de origem e tipo | Por exemplo, um pacote IP | Detecção de erros |

- **MAC — Medium Access Control:** controle de acesso ao meio; endereços MAC identificam interfaces na rede local.
- Pode haver controle de fluxo, detecção de erros e retransmissão, dependendo do protocolo. **Detectar um erro não garante a entrega.**
- Ethernet com switches e enlaces full-duplex elimina colisões tradicionais; Wi-Fi compartilha o meio de rádio.
- Para alcançar outra rede, o quadro normalmente é dirigido ao **MAC do próximo roteador**.
- Ao rotear, o roteador retira o pacote do quadro e cria um novo encapsulamento de enlace na saída. Um switch comum não troca os MACs a cada passagem.

### 4. Rede

- Permite comunicar entre redes; seu principal protocolo na Internet é o **IP**.
- **Roteamento:** determina caminhos; **encaminhamento:** envia o pacote ao próximo salto usando essas informações.
- O melhor caminho depende da métrica ou política adotada.
- O IP não garante, sozinho, entrega, ordem ou retransmissão.

### 5. Transporte

- Comunicação **de ponta a ponta entre processos**; portas ajudam a identificar serviços e processos.
- **TCP:** fluxo de bytes confiável e ordenado, com confirmações e retransmissões.
- **Controle de fluxo:** respeita a capacidade do receptor.
- **Controle de congestionamento:** adapta o envio às condições da rede.
- **UDP:** datagramas sem garantia de entrega ou ordem e sem retransmissão automática pelo protocolo.
- Diferença central: **enlace atua localmente; transporte atua entre as extremidades**.

### 6. Sessão, apresentação e aplicação

- **Sessão:** organiza o diálogo; checkpoints permitem retomar operações de um ponto registrado.
- **Apresentação:** define a representação de caracteres, números e estruturas; pode comprimir e criptografar. ASN.1 é uma notação citada nos slides.
- No TCP/IP, sessão e apresentação não são camadas separadas: suas funções geralmente ficam nas aplicações ou bibliotecas.
- **Aplicação:** define o que comunicar e delega a transmissão às camadas inferiores.
- Navegador é um programa; HTTP é um protocolo utilizado por ele.

| Protocolo de aplicação | Uso |
|---|---|
| HTTP | Web e APIs |
| FTP / SCP | Transferência de arquivos |
| SMTP | Envio de e-mails |
| DNS | Consulta de nomes e registros, incluindo endereços IP |
| SNMP | Gerência de rede |
| Telnet / SSH | Terminal remoto; SSH oferece proteção criptográfica |

### 7. TLS

- **TLS — Transport Layer Security:** protege a comunicação com **confidencialidade, integridade e autenticação**.
- **HTTPS:** HTTP protegido por TLS.
- No caso clássico: HTTP usa TLS, que usa TCP.
- TLS não substitui TCP: suas funções costumam ser agrupadas na aplicação no modelo TCP/IP.

### 8. OSI versus TCP/IP

| Modelo OSI | TCP/IP — quatro camadas dos slides |
|---|---|
| Aplicação + Apresentação + Sessão | Aplicação |
| Transporte | Transporte |
| Rede | Rede / Internet |
| Enlace + Física | Enlace / Acesso à rede |

- **OSI:** modelo de referência; **TCP/IP:** arquitetura e família de protocolos utilizadas na Internet.
- Implementação típica: HTTP na aplicação; TCP/IP no sistema operacional; enlace no driver e placa; física no hardware.

### 9. Encapsulamento

- **PDU — Protocol Data Unit:** unidade de dados de um protocolo.
- **Encapsulamento:** acrescentar informações de controle aos dados da camada superior.
- **Desencapsulamento:** interpretar/remover essas informações e entregar o conteúdo à camada superior.

| Camada / protocolo | Unidade | Composição simplificada |
|---|---|---|
| Aplicação | Mensagem | Dados da aplicação |
| Transporte / TCP | Segmento | Cabeçalho TCP + dados |
| Rede / IP | Pacote | Cabeçalho IP + segmento |
| Enlace / Ethernet | Quadro | Cabeçalho Ethernet + pacote + FCS |
| Física | Bits em sinais | Representação para transmissão |

- **Envio:** dados → segmento → pacote → quadro → sinais.
- **Recepção:** caminho inverso.
- Protocolos da mesma camada comunicam-se logicamente; os dados passam efetivamente pelas camadas inferiores e pelo meio físico.
- Uma mensagem pode ser dividida em vários segmentos, pacotes e quadros.

## Para memorizar

- **Física:** sinais; **enlace:** comunicação local; **rede:** caminhos; **transporte:** ponta a ponta.
- **MAC:** identificação no enlace; **IP:** endereço lógico na rede; **porta:** serviço/processo.
- **Quadro:** enlace; **pacote:** IP; **segmento:** TCP.
- **TCP:** entrega confiável e ordenada; **TLS:** proteção criptográfica.
- **Circuitos:** reserva de capacidade; **pacotes:** compartilhamento da capacidade.
