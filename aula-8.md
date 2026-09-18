# Aula 8 — Manipulação de Endereços IP (Parte 2)

## 1. Revisão de sub-redes

- `200.17.212.177/26` pertence à sub-rede `200.17.212.128/26`.
- Seu Host-ID é 49 e seu broadcast é `200.17.212.191`.
- `130.97.16.132/20` pertence à sub-rede `130.97.16.0/20`.
- Nesse exercício histórico, o `/20` divide o bloco classe B `/16` em 16 sub-redes.

## 2. Problema das classes

- As classes A, B e C ofereciam blocos de tamanhos fixos.
- Uma classe C podia ser pequena demais para uma organização.
- Uma classe B podia desperdiçar milhares de endereços.
- Esse desperdício contribuiu para a escassez de IPv4.
- IPv6, NAT e CIDR enfrentam diferentes aspectos desse problema.

## 3. CIDR

- **CIDR:** Classless Inter-Domain Routing.
- Elimina a dependência das classes A, B e C.
- Permite distribuir blocos de tamanhos diferentes.
- O prefixo `/n` informa quantos bits identificam a rede.
- Os bits restantes variam dentro do bloco.
- Exemplo: `/25` utiliza 25 bits de rede e deixa 7 bits restantes.

## 4. Tamanho dos blocos

- Total de endereços: `2^(32 − prefixo)`.
- Quanto maior o prefixo, menor o bloco.
- Quanto menor o prefixo, maior o bloco.
- Os prefixos IPv4 podem variar de `/0` a `/32`.
- Total de endereços não é necessariamente o total utilizável por hosts.

| Prefixo | Bits restantes | Total de endereços |
|---|---:|---:|
| `/27` | 5 | 32 |
| `/26` | 6 | 64 |
| `/25` | 7 | 128 |
| `/24` | 8 | 256 |
| `/23` | 9 | 512 |
| `/22` | 10 | 1.024 |
| `/21` | 11 | 2.048 |
| `/20` | 12 | 4.096 |

## 5. Distribuição hierárquica

- A IANA coordena globalmente os recursos de numeração IP.
- Os RIRs administram regiões.
- A LACNIC atende a América Latina e o Caribe.
- O NIC.br exerce o papel de registro nacional no Brasil.
- Provedores recebem blocos e distribuem partes menores aos clientes.
- Nem toda distribuição passa por todos esses níveis.

Exemplo didático de blocos encaixados, sem representar uma alocação real:

```text
Bloco maior:  200.0.0.0/7
Parte dele:  200.128.0.0/9
Provedor:    200.128.32.0/20
Cliente:     200.128.32.0/24
```

## 6. Divisão de blocos

- Para dividir um bloco, aumentamos o prefixo.
- Dividir um `/16` em quatro partes usa dois bits adicionais.
- Cada parte passa a ser `/18`.
- Quantidade de partes iguais: `2^(novo prefixo − prefixo original)`.

Divisão de `200.17.0.0/16`:

```text
200.17.0.0/18
200.17.64.0/18
200.17.128.0/18
200.17.192.0/18
```

- Cada `/18` contém `2^14 = 16.384` endereços.
- O bloco `200.17.64.0/18` pode ser dividido novamente em quatro `/20`:

```text
200.17.64.0/20
200.17.80.0/20
200.17.96.0/20
200.17.112.0/20
```

## 7. Agregação de rotas

- Representa várias redes menores por uma rota mais abrangente.
- Também chamada de sumarização ou supernetting.
- Para uma agregação exata, os blocos precisam preencher um intervalo contínuo e alinhado ao prefixo resultante.
- A rota agregada deve encaminhar corretamente para as redes representadas.
- As redes internas continuam existindo; o que se simplifica é sua representação nas tabelas.

Exemplo:

```text
200.17.200.0/24
200.17.201.0/24
200.17.202.0/24
200.17.203.0/24
```

As quatro redes podem ser representadas por:

```text
200.17.200.0/22
```

- O bloco agregado contém 1.024 endereços.
- Seu intervalo vai de `200.17.200.0` a `200.17.203.255`.
- Uma entrada pode substituir quatro onde a agregação for apropriada.

## 8. Longest Prefix Match

- Um destino pode corresponder a várias rotas.
- O roteador escolhe o maior prefixo entre as rotas que correspondem ao destino.
- Essa é a rota mais específica.
- Uma rota com prefixo maior só participa da escolha se contiver o destino.

Exemplo:

```text
Destino: 200.17.212.177

Rotas:
200.17.0.0/16
200.17.212.0/24

Escolhida:
200.17.212.0/24
```

- Ambas contêm o destino, mas `/24` é mais específico.
- A rota padrão `0.0.0.0/0` corresponde a qualquer IPv4.
- Ela é usada quando não existe uma rota correspondente mais específica.

## 9. CIDR e VLSM

- **VLSM:** permite sub-redes com máscaras de tamanhos diferentes dentro de uma organização.
- **CIDR:** permite endereçamento sem classes e agregação de rotas entre redes.
- Ambos utilizam prefixos de tamanho variável, mas têm focos diferentes.

## O que você precisa guardar

- CIDR substitui a dependência das classes fixas.
- O prefixo define o tamanho do bloco.
- Dividir um bloco aumenta o prefixo.
- Agregar blocos produz um prefixo menor e mais abrangente.
- Longest prefix match seleciona a rota correspondente mais específica.
- CIDR melhora a distribuição dos IPv4 e permite reduzir tabelas de roteamento.