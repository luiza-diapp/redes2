# Aula 11 — Protocolo ICMP

## 1. O que é ICMP

- **ICMP** = *Internet Control Message Protocol*.
- Atua na **camada de rede**.
- É usado para:
  - reportar erros no envio de pacotes IP;
  - enviar mensagens de controle.
- O ICMP **não torna o IP confiável**.
- A própria mensagem ICMP é transportada dentro de um pacote IP, então ela também pode ser perdida.
- Não são geradas mensagens de erro ICMP em resposta a outras mensagens de erro ICMP.

## 2. Formato da mensagem ICMP

- **Tipo (8 bits):** identifica o tipo de mensagem.
- **Código (8 bits):** detalha o motivo dentro daquele tipo.
- **Checksum (16 bits):** detecta erros na mensagem ICMP.
- **Payload:** informações específicas da mensagem.

Em mensagens de erro, o payload inclui informações do pacote IP original para ajudar no diagnóstico.

## 3. Tipos importantes

### Tipo 8 — Echo Request

- É a requisição enviada pelo comando `ping`.
- Pergunta, de forma simplificada: **“você está aí?”**

### Tipo 0 — Echo Reply

- É a resposta ao Echo Request.
- Indica que o destino respondeu ao `ping`.

```text
Origem  -- Echo Request (Tipo 8) -->  Destino
Origem  <-- Echo Reply (Tipo 0) ---  Destino
```

### Tipo 3 — Destination Unreachable

Indica que o pacote não pôde ser entregue.

Códigos principais:

- **0:** Network Unreachable — rede inatingível.
- **1:** Host Unreachable — host inatingível.
- **2:** Protocol Unreachable — protocolo não suportado.
- **3:** Port Unreachable — não existe processo associado à porta.
- **4:** Fragmentation Needed — pacote precisa ser fragmentado, mas a flag **Don't Fragment** está ativa.

### Tipo 11 — Time Exceeded

- Cada roteador diminui o **TTL** em 1.
- Quando `TTL = 0`:
  - o pacote é descartado;
  - o roteador envia uma mensagem ICMP **Time Exceeded**.

### Tipo 4 — Source Quench

- Relacionado ao congestionamento.
- Indicava que a origem deveria reduzir a taxa de envio.
- Na prática, o controle de congestionamento é feito pelo **TCP**.

### Tipo 12 — Parameter Problem

- Usado para problemas não representados por outras mensagens ICMP.
- Exemplos:
  - cabeçalho IP corrompido;
  - opções IP inválidas.

## 4. Ping

O comando:

```bash
ping 8.8.8.8
```

usa:

- **Echo Request (Tipo 8)**;
- **Echo Reply (Tipo 0)**.

Permite verificar:

- conectividade até a camada de rede;
- funcionamento do roteamento;
- **RTT (Round-Trip Time)**;
- perda de pacotes.

Campos comuns:

- `icmp_seq`: número de sequência.
- `ttl`: TTL restante na resposta.
- `time`: tempo de ida e volta do pacote.

> Um `ping` responder não garante que protocolos de transporte ou aplicações estejam funcionando.

## 5. Porta

- O **IP** identifica a máquina.
- A **porta** identifica o processo ou serviço dentro da máquina.

Exemplo:

```text
IP: 10.0.0.5
Porta: 9999
```

Se o host existe, mas não há nenhum processo usando a porta `9999`, pode ser retornado:

```text
ICMP Tipo 3
Código 3
Port Unreachable
```

## 6. Hop

- **Hop** = salto entre roteadores no caminho até o destino.
- Cada roteador atravessado corresponde a um hop.

Exemplo:

```text
PC → R1 → R2 → R3 → Servidor
      1     2     3      4 hops
```

## 7. Traceroute

O `traceroute` descobre os roteadores no caminho até o destino.

Funcionamento:

1. Envia pacote com `TTL = 1`.
2. O primeiro roteador decrementa para `0`.
3. Ele descarta o pacote e responde com **ICMP Tipo 11**.
4. Depois é enviado outro pacote com `TTL = 2`.
5. O processo continua até chegar ao destino.

```text
TTL 1 → descobre o 1º roteador
TTL 2 → descobre o 2º roteador
TTL 3 → descobre o 3º roteador
...
```

- A implementação mostrada na aula envia **3 pacotes UDP por rodada**.
- Isso permite observar:
  - variação de latência;
  - perda de pacotes;
  - múltiplas rotas;
  - balanceamento de carga.

### `* * *` no traceroute

- Significa que não houve resposta para aquelas tentativas.
- Não significa necessariamente que o roteador esteja com defeito.
- ICMP pode estar bloqueado ou ter baixa prioridade.

## 8. Ping x Traceroute

- O **traceroute** observa o caminho de **ida**.
- O TTL observado no **ping** corresponde ao caminho de **volta**.
- Os caminhos podem ser diferentes devido a **rotas assimétricas**.

## 9. Record Route

- É uma opção do cabeçalho IP.
- Cada roteador registra seu endereço IP no pacote.
- Como o espaço de opções do cabeçalho é limitado, consegue registrar apenas poucos saltos.
- O `traceroute` não possui essa mesma limitação.

## 10. Congestionamento

- Acontece quando os pacotes chegam aos roteadores mais rápido do que eles conseguem processar.
- Consequência:
  - filas aumentam;
  - pacotes são descartados;
  - retransmissões podem aumentar ainda mais o tráfego.

## Resumo para prova

- **ICMP:** mensagens de erro e controle da camada de rede.
- **Tipo 8:** Echo Request.
- **Tipo 0:** Echo Reply.
- **Tipo 3:** Destination Unreachable.
- **Tipo 11:** Time Exceeded.
- **Ping:** testa conectividade e mede RTT.
- **TTL:** diminui 1 em cada roteador.
- **Traceroute:** usa TTL crescente para descobrir os hops.
- **Porta:** identifica o processo/serviço dentro de um host.
- **Hop:** cada salto entre roteadores.
- `* * *` no traceroute = ausência de resposta, não necessariamente falha.
---
- CMP auxilia o IP com mensagens de erro e controle; ele não torna IP confiável.
- ICMP é transportado dentro de IP, portanto uma mensagem ICMP também pode ser perdida.
- O cabeçalho básico possui Tipo + Código + Checksum + Payload.
- Ping = Echo Request tipo 8 + Echo Reply tipo 0.
- Ping testa conectividade da camada de rede e mede RTT, mas não prova que TCP ou uma aplicação estejam funcionando.
- Tipo 3 = Destination Unreachable, e o código explica por que o destino não pôde ser alcançado.
- TTL diminui a cada roteador; quando chega a zero, o pacote é descartado e surge ICMP Tipo 11 — Time Exceeded.
- Traceroute explora propositalmente o TTL: envia pacotes com TTL 1, depois 2, depois 3 etc., descobrindo os roteadores do caminho.
- `* * *`no traceroute significa ausência de resposta, não necessariamente roteador com defeito.
- Ping e traceroute podem mostrar caminhos diferentes porque a rota de ida pode ser diferente da rota de volta.
- ICMP também aparece relacionado a congestionamento (Source Quench) e erros de parâmetros do pacote (Parameter Problem).
