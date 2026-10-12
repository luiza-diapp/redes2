
Aula 1 — Introdução às redes

- Redes conectam dispositivos para trocar dados e compartilhar recursos.
- Protocolos definem regras; padrões permitem compatibilidade.
- Circuitos reservam capacidade; pacotes compartilham a rede.
- Palavras-chave: protocolos, padrões, Internet, PAN, LAN, MAN, WAN, comutação.

Aula 2 — Modelo OSI

- Sete camadas: física, enlace, rede, transporte, sessão, apresentação e aplicação.
- MAC = enlace; IP = rede; portas = transporte.
- Encapsulamento: dados → segmento → pacote → quadro → sinais.
- Palavras-chave: OSI, TCP/IP, encapsulamento, TCP, UDP, TLS.

Aula 3 — Ethernet

- Tecnologia de rede local cabeada; utiliza quadros e endereços MAC.
- Switch: aprende pelo MAC de origem e encaminha pelo destino.
- CRC detecta erros; full-duplex permite transmitir e receber simultaneamente.
- Palavras-chave: Ethernet, IEEE 802.3, switch, tabela MAC, flooding, CSMA/CD, FCS.

Aula 4 — Internet

- Internet é uma rede de redes interligadas por roteadores.
- IPv4 tem 32 bits; IPv6 tem 128 bits.
- Unicast: um destino; broadcast: todos no domínio; multicast: grupo.
- Palavras-chave: IP, NET-ID, HOST-ID, DNS, backbone, loopback, NAT, big endian.

Aula 5 — ARP

- Descobre o MAC associado a um IPv4 local.
- Request normalmente é broadcast; Reply normalmente é unicast.
- Destino remoto: procura o MAC do gateway.
- Palavras-chave: ARP Request, ARP Reply, cache ARP, gateway.
- Diferença: cache ARP = IP → MAC; tabela do switch = MAC → porta.

Aula 6 — Roteamento IP

- Roteamento determina caminhos; encaminhamento envia cada pacote.
- IP não garante entrega nem ordem; confiabilidade pode ser fornecida pelo TCP.
- Sem NAT, IPs de origem/destino permanecem; MACs mudam entre enlaces.
- Palavras-chave: tabela de roteamento, próximo salto, rota padrão, DHCP, OSPF, RIP, BGP.

Aula 7 — Sub-redes

- Divide um bloco IP em redes menores, usando bits de host.
- Máscara separa rede e host: IP AND máscara = endereço da rede.
- Total de endereços: 2ʰ; hosts utilizáveis nas sub-redes tradicionais: 2ʰ − 2.
- Palavras-chave: máscara, prefixo, subnetting, broadcast, Proxy ARP.

Aula 8 — CIDR

- Permite blocos de tamanhos variados, sem depender das classes.
- Prefixo maior = bloco menor.
- Agregação resume rotas; encaminhamento escolhe o prefixo correspondente mais específico.
- Palavras-chave: CIDR, VLSM, sumarização, longest prefix match, IANA, LACNIC.

Aula 9 — IP: cabeçalho e fragmentação

- IP oferece serviço best effort, sem garantia de entrega.
- Cabeçalho IPv4: 20–60 bytes; IHL conta unidades de 4 bytes.
- Fragmentação depende da MTU; offset conta unidades de 8 bytes.
- Palavras-chave: datagrama, IHL, MTU, DF, MF, offset, DSCP, ECN.

Aula 10 — IP: continuação

- Fragmentos são remontados no destino; offsets referem-se ao payload original.
- TTL diminui a cada roteador e limita loops.
- Checksum IPv4 cobre somente o cabeçalho e é atualizado a cada salto.
- Palavras-chave: remontagem, refragmentação, TTL, checksum, protocolo, opções, padding.

Aula 11 — ICMP

- Envia mensagens de erro e controle; não torna o IP confiável.
- Ping testa conectividade e mede RTT: Request = tipo 8; Reply = tipo 0.
- Traceroute usa TTL crescente; tipo 11 = Time Exceeded; tipo 3 = Destination Unreachable.
- Palavras-chave: ICMP, ping, traceroute, RTT, hop, TTL, tipo, código.
- Para memorizar: nesse traceroute, a tentativa vai em UDP e a resposta de diagnóstico volta em ICMP, ambos dentro de IP.
