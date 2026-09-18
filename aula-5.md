# Aula 5 — O Protocolo ARP

## 1. Recursos e serviços de rede

- **Compartilhamento:** permite dividir arquivos, serviços e equipamentos.
- **Multicast:** envia dados a um grupo, replicando pacotes onde os caminhos se dividem.
- **CDN:** distribui conteúdo em servidores próximos dos usuários.
- **Nuvem:** oferece processamento e armazenamento sob demanda.

## 2. Para que serve o ARP?

- Descobre o **MAC associado a um IPv4 na rede local**.
- O IP identifica logicamente uma interface e permite o roteamento.
- O MAC permite entregar o quadro no enlace local.
- O MAC não é calculado a partir do IP: a associação é descoberta.

## 3. Funcionamento

- O computador consulta seu **cache ARP**.
- Se não encontrar a associação, envia um **ARP Request**:
  - Pergunta: “Quem tem este IP?”
  - Normalmente usa broadcast: `FF:FF:FF:FF:FF:FF`.
- O dispositivo procurado envia um **ARP Reply**:
  - Responde: “Esse IP é meu; este é meu MAC.”
  - Normalmente usa unicast para responder ao solicitante.
- O solicitante guarda a associação e envia o quadro de dados.

## 4. Cache ARP

- Armazena associações **IPv4 → MAC** temporariamente.
- Evita repetir a descoberta para cada envio.
- As entradas dinâmicas expiram e podem ser renovadas.
- O comando `arp -a` permite consultar associações armazenadas.

## 5. Destino local ou remoto

- **Mesma rede:** procura o MAC do destinatário.
- **Outra rede:** procura o MAC do gateway local.
- O gateway encaminha o pacote em direção à rede de destino.
- O broadcast ARP não atravessa roteadores.
- Sem NAT, os IPs de origem e destino permanecem; os endereços de enlace mudam entre os enlaces.

## 6. Encapsulamento e campos

- ARP é transportado diretamente no quadro Ethernet, sem cabeçalho IP.
- **EtherType `0x0806`:** identifica ARP no quadro.
- Principais campos da mensagem ARP:
  - Tipo de hardware: Ethernet = `1`.
  - Tipo de protocolo: IPv4 = `0x0800`.
  - Tamanho do MAC: `6 bytes`.
  - Tamanho do IPv4: `4 bytes`.
  - Operação: Request = `1`; Reply = `2`.
  - MAC e IP do remetente.
  - MAC e IP do alvo.
- No Request, o MAC do alvo ainda é desconhecido e normalmente aparece zerado.
- Esse campo zerado não é o MAC de destino do quadro, que é broadcast.

## 7. Não confundir

- **Cache ARP:** associa IP a MAC.
- **Tabela do switch:** associa MAC à porta de saída do switch.
- **DNS:** associa nomes a endereços e outros registros.
- **ARP:** descobre o MAC do próximo salto local; não o de qualquer computador na Internet.