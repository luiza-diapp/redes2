# Aula 6 — Introdução ao Roteamento IP

## 1. ARP, RARP e DHCP

- **ARP:** descobre o MAC associado a um IPv4 local.
- **RARP:** permitia obter o próprio IP a partir do MAC, consultando um servidor.
- RARP era usado na inicialização de máquinas sem disco.
- É obsoleto; foi sucedido por BOOTP e DHCP.
- **DHCP:** fornece automaticamente IP, máscara, gateway e servidores DNS.

## 2. Roteamento e encaminhamento

- **Roteamento:** determina caminhos e constrói informações de rotas.
- **Encaminhamento:** consulta a tabela para decidir por onde enviar cada pacote.
- IP atua na camada de rede (L3).
- OSPF, RIP e BGP são exemplos de protocolos de roteamento.

## 3. Características do IP

- **Não confiável:** não garante entrega, ordem ou ausência de duplicação.
- Não confirma cada entrega nem retransmite dados perdidos por conta própria.
- **Não orientado à conexão:** não estabelece uma sessão antes do envio.
- Cada pacote é encaminhado individualmente; pacotes podem seguir caminhos diferentes.
- A confiabilidade fica nas pontas, por meio do TCP ou da aplicação.
- TCP oferece entrega confiável e ordenada enquanto a conexão funciona.

## 4. Três casos de comunicação

- **Mesmo computador:** usa comunicação local, como `127.0.0.1`; não sai pela placa de rede.
- **Mesma rede:** envia diretamente ao destino, usando seu MAC.
- **Outra rede:** envia ao próximo roteador, usando o MAC dele.
- Nos slides, os dois primeiros casos são diretos; o terceiro é indireto.

## 5. IP, MAC e próximo salto

- O IP de destino identifica o destinatário final.
- O MAC de destino identifica quem recebe o quadro no enlace atual.
- A tabela de roteamento escolhe o próximo salto e a interface de saída.
- ARP descobre o MAC desse próximo salto, quando necessário.

### Exemplo: A envia para C em outra rede, sem NAT

| Informação | A envia ao roteador | Roteador envia a C |
|---|---|---|
| IP de origem | IP de A | IP de A |
| IP de destino | IP de C | IP de C |
| MAC de origem | MAC de A | MAC da interface de saída do roteador |
| MAC de destino | MAC da interface do roteador na rede de A | MAC de C |

- Os IPs de origem e destino permanecem.
- O roteador monta um novo quadro com os MACs do enlace seguinte.
## 6. Tabela de roteamento

- Associa redes de destino a próximos saltos e interfaces.
- Usa prefixos para representar redes, evitando uma entrada por computador.
- A rota com o prefixo correspondente mais específico é preferida.
- **Rota padrão:** usada quando não existe uma rota mais específica.
- Cada roteador decide apenas o próximo passo, usando sua própria tabela.
- Ida e volta podem seguir caminhos diferentes.
- Podem existir múltiplos caminhos e loops de encaminhamento.

## 7. Comandos e campos importantes

- `ip route show`: consulta a tabela de roteamento.
- `default`: rota padrão.
- `via`: endereço do próximo salto.
- `dev`: interface de saída.
- `scope link`: destino diretamente alcançável no enlace.
- `src`: IP de origem preferido para a rota.
- `proto dhcp`: rota configurada via DHCP.
- `metric`: preferência entre rotas comparáveis; menor valor costuma ser preferido.
- `tcpdump`: observa pacotes em uma interface.
- `nc`: envia dados ou espera conexões.
- `lo`: interface virtual de loopback.

## O essencial

- **Tabela de roteamento:** escolhe para onde enviar.
- **ARP:** descobre o MAC do próximo destinatário local.
- **Ethernet:** entrega o quadro nesse enlace.
- **IP:** permite alcançar o destino através das redes.
- **TCP:** controla a entrega confiável e ordenada nas pontas.