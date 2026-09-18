
## Aula 4 — A Internet

### 1. Rede de redes e TCP/IP

- Interliga tecnologias distintas: Ethernet, Wi-Fi, redes celulares, satélites etc.
- **Abstração lógica comum**, sustentada por infraestrutura física e protocolos.
- **Sistemas autônomos:** redes participantes sob administração própria.
- **TCP/IP:** família de protocolos; **IP = L3**, **TCP = L4**.
- Outros: UDP, ICMP, ARP, DHCP, DNS, HTTP, BGP e OSPF.

### 2. Endereçamento IP

- **Endereço IP:** identificação lógica da interface na rede; base do roteamento.
- Máquina pode ter vários IPs e interfaces.
- Mudança de rede normalmente muda o IP.
- **NET-ID:** rede; **HOST-ID:** interface dentro dela.
- **DNS:** associa nomes, como `www.inf.ufpr.br`, a endereços.
- **Host:** origina/recebe comunicações.
- **Roteador:** encaminha pacotes entre redes.
- Hosts também podem conectar várias redes; a função distingue host de roteador.

### 3. IPv4 e IPv6

| Característica | IPv4 | IPv6 |
|---|---|---|
| Tamanho | 32 bits / 4 bytes | 128 bits / 16 bytes |
| Endereços teóricos | ≈ 4,3 bilhões | ≈ 3,4 × 10³⁸ |
| Representação | Decimal com pontos | Hexadecimal com dois-pontos |
| Exemplo | `200.17.212.86` | `2001:db8::1` |

- Octeto IPv4: **0–255**.
- `11001000.00010001.11010100.01010110` = `200.17.212.86`.
- IPv6 amplia o endereçamento; transição exige mudanças em redes e sistemas.
- NAT e endereços privados prolongam o IPv4; ambas as versões coexistem.
- **IPv5:** protocolo experimental de streaming, não sucessor geral do IPv4.

### 4. Classes IPv4 — históricas

| Classe | Bits iniciais | Primeiro octeto | Divisão histórica |
|---|---|---|---|
| A | `0` | 0–127 | Rede /8; 24 bits de host. |
| B | `10` | 128–191 | Rede /16; 16 bits de host. |
| C | `110` | 192–223 | Rede /24; 8 bits de host. |
| D | `1110` | 224–239 | Multicast. |
| E | `1111` | 240–255 | Reservada/experimental. |

- Intervalos incluem reservas; exemplo: **127.0.0.0/8 = loopback**.
- A: poucas redes grandes; B: intermediárias; C: muitas redes pequenas.
- **n bits → 2ⁿ combinações**. Bits de classe reduzem as combinações de NET-ID.
- Atual: **CIDR**, com prefixos flexíveis. Primeiro octeto sozinho não determina a máscara.

### 5. Destinatários e endereços especiais

- **Unicast:** um → um.
- **Broadcast:** um → todos no domínio local; solicitação ARP e algumas mensagens DHCP.
- **Multicast:** um → grupo; exemplo: IPTV.
- Multicast IPv4: **224.0.0.0–239.255.255.255**.
- Sub-redes IPv4 tradicionais: **HOST-ID zerado = rede; todos os bits 1 = broadcast**.

| Rede `200.17.202.0/24` | Valores |
|---|---|
| Endereço da rede | `200.17.202.0` |
| Hosts utilizáveis | `200.17.202.1–200.17.202.254` |
| Broadcast | `200.17.202.255` |
| Quantidade | 256 endereços; 254 para hosts. |

- **127.0.0.1 — loopback:** própria máquina; nome usual: `localhost`.
- Testa serviços locais; não sai pelo cabo/Wi-Fi nem atravessa switches/roteadores.

### 6. Ordem dos bytes

- **Big endian:** byte mais significativo primeiro.
- **Little endian:** byte menos significativo primeiro.

| Valor `0x12345678` | Ordem |
|---|---|
| Big endian | `12 34 56 78` |
| Little endian | `78 56 34 12` |

- Campos numéricos multibyte tradicionais: **ordem de rede = big endian**.
- Máquinas little endian, como x86, convertem quando necessário.
- Muda a ordem dos **bytes**, não inverte todos os bits.

### 7. Backbones

- Interligam redes; transportam grandes volumes de tráfego.
- Escalas: institucional, regional, nacional ou internacional.
- Recursos: equipamentos robustos, fibras, redundância e enlaces de alta capacidade.
- Exemplos: **Rede Ipê/RNP**, **COPEL**, backbone da **UFPR**.

## Dúvidas discutidas — complemento

| Conceito | Papel |
|---|---|
| **MAC** | Interface destinatária no enlace; endereço do quadro. |
| **IP** | Origem/destino lógico e roteamento; endereço do pacote. |
| **ARP** | Descobre MAC pelo IPv4 do próximo destino local. |
| **TCP** | Fluxo completo e ordenado para a aplicação; confirma e retransmite; pode informar falha. |

- Servidor distante: **IP destino = servidor; MAC destino inicial = roteador**.
- Entre redes, o roteador substitui o encapsulamento de enlace.
- Em casa: notebook e roteador têm IPs privados; roteador também tem IP na interface do provedor.
- **NAT IPv4 do exemplo:** traduz origem privada para pública; registra comunicação para entregar a resposta.

| Pacote com NAT | IP origem | IP destino |
|---|---|---|
| Antes | Privado do notebook | Servidor final |
| Depois | Público usado na tradução | Servidor final |

- Nem todo roteador faz NAT; sem tradução, IPs normalmente permanecem no percurso.
- Provedor também pode fazer NAT: IP externo doméstico nem sempre é público.
- **VLAN:** separação lógica de LANs.
- Tag de **4 bytes** pode identificar a VLAN; quadro sem tag também pode pertencer a uma VLAN.
