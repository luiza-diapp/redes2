# AULA 10 — O Protocolo IP (pt. 2)

## Exemplo com ajuste: 2800 bytes, MTU 600

- 600 − 20 = 580, **não é múltiplo de 8** → ajusta para **576**
- Payload original = 2780 → 5 fragmentos

| Fragmento | Total | Payload | Offset | MF |
|---|---|---|---|---|
| 1–4 | 596 | 576 | 0 / 576 / 1152 / 1728 | 1 |
| 5 | 496 | 476 | 2304 | 0 |

- O último fragmento **cresce** (460 → 476): recebe os 4 bytes descartados de cada um dos anteriores

## Onde o pacote é remontado?

- **Sempre no host de destino**, nunca num roteador intermediário
- Porque: o próximo enlace pode exigir fragmentação de novo; os fragmentos podem seguir **caminhos diferentes**; e remontar exigiria o roteador manter buffer e estado

## Fragmentando fragmentos

- O IP permite refragmentar um fragmento
- Exemplo: 3400 B → MTU 1500 → depois MTU 1000 (payload 980 → **976**)

| Fragmento | Payload | Offset | MF |
|---|---|---|---|
| 1.1 | 976 | 0 | 1 |
| 1.2 | 504 | 976 | 1 |
| 2.1 | 976 | 1480 | 1 |
| 2.2 | 504 | 2456 | 1 |
| 3.1 | 420 | 2960 | 0 |

- Offsets continuam medidos sobre o payload **original** (2456 = 1480 + 976)
- Fragmento 3 já cabia no MTU → não foi refragmentado
- Só o **último de todos** tem MF = 0; todos carregam o mesmo identificador

## Resumo da fragmentação

- Quem fragmenta e remonta é o próprio **IP**
- A cada transmissão, o IP compara tamanho do pacote × MTU do enlace
- Pode ocorrer no **host de origem** ou em **roteador intermediário**
- **Deve ser evitada**: degrada desempenho e cria fragilidade — perdeu um fragmento, reenvia tudo

## TTL — Time to Live

- Motivação: tabelas de roteamento inconsistentes podem gerar **loops**
- **O nome é ruim: TTL não conta tempo, conta saltos (hops)**
- Inicializado pela implementação do IP no S.O.; valores comuns **64 ou 128**
- Cada roteador faz TTL = TTL − 1, **na entrada** do pacote
- TTL = 0 → descarta

## Campo Protocolo

- O IP não gera pacotes espontaneamente — sempre carrega dados de alguém
- Diz ao destino **como interpretar o payload**
- **ICMP = 1 · TCP = 6 · UDP = 17**
- Números atribuídos pela **IANA**

## Checksum

- Mais simples e frágil que o da Ethernet, porque **Ethernet é hardware e IP é software** — é mais fácil atacar software
- Calculado **só sobre o header**, não sobre o payload
- Algoritmo:
  1. Header como palavras de **16 bits**
  2. Soma em **complemento de 1**, com **end-around carry** (o "vai 1" volta e soma no bit menos significativo)
  3. Tira o **complemento** → esse é o checksum
- No destino: mesma soma **incluindo o checksum**; complemento **= 0** → OK, **≠ 0** → descarta
- Exemplos com palavras de 4 bits:
  - `0110 0001` → 0110 + 0001 = 0111 → checksum `1000`; destino: 0110 + 0001 + 1000 = 1111 → 0000 ✓
  - `1101 0101` → 1101 + 0101 = 10010 → carry → 0011 → checksum `1100`; destino: 11110 → 1111 → 0000 ✓
  - Com erro (`1101 0001 1100`): soma 11010 → 1011 → complemento **0100** → erro ✗
- **Recalculado a cada salto**, porque o TTL muda → impacto no desempenho
  - Otimização em hardware: como se sabe o campo que mudou, a operação (−1) e o checksum anterior, atualiza-se incrementalmente
- O mesmo "checksum da Internet" é usado por **ICMP, UDP e TCP**

## Endereços de origem e destino

- Definem remetente e destinatário da comunicação

## Opcionais

- Tamanho variável; antes eram **ignorados**, hoje os pacotes são **descartados**
- Motivo: **segurança** — *record route* e *timestamp* revelam a topologia da rede ao atacante; somam-se injeção de código, desalinhamento de pacotes, buffer overflow
- Sobrevivem em **redes privadas**: laboratórios, redes internas, muitas nem conectadas à Internet → *TCP/IP é mais que Internet*
- Principais:
  - **Source Route** (roteamento na origem): o pacote sai com a rota completa
    - **Strict**: ordem exata; nó indisponível → descarta
    - **Loose**: passa pelos nós indicados, por qualquer caminho válido
  - **Record Route**: roteadores gravam no pacote a rota percorrida
  - **Timestamp**: gravam endereço **e** instante do processamento (precisão de ms)
  - **Security**: UNCLASSIFIED, CONFIDENTIAL, SECRET, TOP SECRET
  - **Router Alert**: pede processamento mais cuidadoso

## Padding

- "Enchimento": o header tem que ser múltiplo de **32 bits**
- Como os opcionais têm tamanho arbitrário, completa-se com bits **zero**

## Payload

- Carrega a informação útil: o segmento da camada de transporte (TCP, UDP) ou dados de camadas superiores

---

# Números para decorar

- Header sem opcionais: **20 bytes** → IHL = **5** · máximo **60 bytes** → IHL = 15
- Opcionais: até **40 bytes** · MTU Ethernet: **1500** · Datagrama máximo: **64 KB**
- Offset em palavras de **8 bytes** · IHL em palavras de **4 bytes** · Header múltiplo de **32 bits**
- TTL inicial: **64 ou 128** · Protocolos: ICMP 1, TCP 6, UDP 17
- DSCP: **6 bits** · ECN: **2 bits**

# Pegadinhas de prova

- IHL conta palavras de 4 bytes; offset conta palavras de 8 bytes — **não confundir as unidades**
- Offset no campo = offset em bytes **÷ 8**
- Se (MTU − 20) não for múltiplo de 8, **arredonde para baixo**; o excedente sobra para o último fragmento
- Na refragmentação, offsets são sempre relativos ao **payload original**
- MF = 1 mesmo no último pedaço de um fragmento intermediário
- Cabeçalho **inclui** os opcionais e o padding
- TTL conta hops, não segundos
- Checksum cobre só o header, e é recalculado em todo roteador