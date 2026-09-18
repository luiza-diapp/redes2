# Redes de Computadores — Aulas 3 e 4

> Base: **O Padrão Ethernet** e **A Internet**, Prof. Giovanni Venâncio (UFPR). Inclui as dúvidas discutidas.

## Aula 3 — O Padrão Ethernet

### 1. Conceito e evolução

- **Ethernet:** família de tecnologias para LANs cabeadas; padrão **IEEE 802.3**.
- Atua em **L2 (enlace)** e define aspectos de **L1 (física)**.
- L2: quadros, MACs, acesso ao meio e detecção de erros.
- L1: meios, conexões, sinais e transmissão dos bits.
- Velocidades: 10 Mbps → 100 Mbps → 1 Gbps → 10 Gbps → taxas superiores.
- Meio: cobre ou fibra, conforme a variante.
- Vantagens: baixo custo, interoperabilidade e configuração simples.
- **NIC — Network Interface Card:** interface/placa de rede.

### 2. Ethernet antiga e CSMA/CD

- **Barramento:** máquinas compartilham o mesmo cabo.
- Todos recebem o sinal; interfaces normalmente aceitam quadros para si ou grupos pertinentes.
- Transmissões simultâneas podem causar **colisão**.
- **CSMA/CD:** escuta do meio, acesso compartilhado e detecção de colisões.
- Processo: escutar → transmitir se livre → detectar colisão → interromper → esperar tempo aleatório → tentar novamente.
- **1-persistente:** transmite assim que o meio fica livre; ainda há risco de colisão.
- Meio compartilhado ≠ todo quadro ser broadcast.

### 3. Ethernet moderna e switches

- Dispositivos normalmente têm enlaces dedicados ao switch.
- **Full-duplex:** envio e recepção simultâneos; sem colisões tradicionais nem CSMA/CD.
- **Tabela MAC:** associa endereços às portas.
- **Aprende pela origem; encaminha pelo destino.**

| Destino | Ação do switch |
|---|---|
| Conhecido em outra porta | Envia só nessa porta. |
| Conhecido na porta de entrada | Não envia para outras portas. |
| Unicast desconhecido | Flooding nas demais portas da VLAN. |
| Broadcast | Replica nas demais portas da VLAN. |

- **Flooding:** replica o quadro; mantém o MAC de destino original.
- Aprendizado: observa tráfego recebido; dispensa resposta especial.

### 4. Endereço MAC

- Identifica uma **interface no enlace**, não o computador inteiro.
- **6 bytes = 48 bits**.
- Hexadecimal: `00:1A:2B:3C:4D:5E`; cada par representa 1 byte.
- Atribuição tradicional: IEEE fornece **OUI de 3 bytes** à organização; ela define os 3 bytes finais por interface.
- Parte final: 24 bits → aproximadamente **16,7 milhões de combinações** por bloco.
- MAC de fábrica pode diferir do usado: software permite configurar ou aleatorizar.

### 5. Quadro Ethernet

- **Quadro/frame:** unidade de dados de L2; transporta protocolos como IP ou ARP.
- Estrutura estudada **sem tag VLAN**:

| Campo | Tamanho | Função |
|---|---:|---|
| Preâmbulo | 7 bytes | Sincronizar receptor. |
| SFD | 1 byte | Marcar início do quadro. |
| MAC destino | 6 bytes | Destinatário no enlace. |
| MAC origem | 6 bytes | Interface remetente. |
| Tipo/EtherType | 2 bytes | Identificar protocolo transportado. |
| Dados + padding | 46–1500 bytes | Conteúdo e preenchimento. |
| FCS | 4 bytes | Detectar erros. |

- **Padding:** completa conteúdos menores que 46 bytes.
- **1500 bytes:** limite usual do payload/MTU, não do quadro.
- Quadro: **64–1518 bytes**, do MAC destino ao FCS; exclui preâmbulo e SFD.
- Tag **802.1Q:** +4 bytes → máximo usual de **1522 bytes**.
- Correção dos slides: **MAC destino vem antes do MAC origem**.

### 6. CRC, FCS e encapsulamento

- **CRC:** algoritmo de detecção de corrupção dos bits.
- **FCS:** guarda o cálculo sobre cabeçalho, dados e padding.
- Erro detectado → descarte. CRC não corrige nem criptografa.
- **Encapsulamento:** dados da camada superior dentro da unidade inferior, com controle adicional.
- Envio: dados → segmento TCP → pacote IP → quadro Ethernet → sinais.
- **Desencapsulamento:** processo inverso no destino.

### 7. Redes comuns e industriais

- Sem colisões ainda há risco de **filas, congestionamento, atrasos e perdas**.
- Ethernet comum: sem garantias rígidas de prazo.
- Redes industriais: podem exigir prazo máximo de entrega.
- **Token Ring — IEEE 802.5:** só transmite quem tem token; evita colisões, mas exige esperar a vez.
- **Token Bus — IEEE 802.4:** outra tecnologia histórica.
- **Ethernet Industrial/TSN:** mecanismos para requisitos industriais e temporais.
- Cabos resistentes: robustez física. Garantias temporais também exigem protocolos e configuração.
