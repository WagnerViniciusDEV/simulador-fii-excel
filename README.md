# Simulador de FIIs no Excel

Projeto do desafio da DIO. A planilha estima o patrimônio acumulado e os dividendos mensais ao final de um prazo e distribui o aporte por tipo de fundo conforme o perfil escolhido.

## Como usar

Na aba **Simulador**, informe o salário fictício em B3, o aporte em B5, o prazo em anos em B6 e as taxas mensais de acumulação e dividendos em B7 e B8. Digite a taxa com o símbolo de porcentagem, por exemplo, `0,5%`. Selecione o perfil em B9. A sugestão em B4 corresponde a 30% do salário. O aporte usado na simulação é o valor de B5.

O patrimônio e os dividendos aparecem em B10:B11. As linhas 15 a 19 comparam 2, 5, 10, 20 e 30 anos. As linhas 21 a 27 mostram a divisão do aporte e os totais.

## Fórmulas e intervalos nomeados

| Nome | Referência |
| --- | --- |
| `Salario_Mensal` | Simulador!B3 |
| `Aporte_Mensal` | Simulador!B5 |
| `Prazo_Anos` | Simulador!B6 |
| `Taxa_Acumulacao` | Simulador!B7 |
| `Taxa_Dividendos` | Simulador!B8 |
| `Perfil_Investidor` | Simulador!B9 |
| `Patrimonio_estimado` | Simulador!B10 |
| `Dividendos_mensais_estimados` | Simulador!B11 |
| `lista_perfis` | Apoio!E3:E5 |

- **Sugestão de aporte:** `=Salario_Mensal*30%`.
- **Patrimônio:** `=VF(Taxa_Acumulacao;Prazo_Anos*12;-Aporte_Mensal;0;0)`. A taxa é mensal e o prazo é convertido em meses. O aporte negativo representa uma saída de caixa. O primeiro zero indica capital inicial zero. O segundo coloca os aportes no fim de cada mês.
- **Dividendos mensais estimados:** `=Patrimonio_estimado*Taxa_Dividendos`. O cálculo estima a renda de um mês sobre o saldo no fim do prazo. Cada cenário aplica a mesma lógica ao prazo da sua linha.
- **Divisão do aporte:** em B21, `=PROCV(Perfil_Investidor&"|"&A21;Apoio!$A$3:$D$20;4;FALSO)`. Por exemplo, a chave `Moderado|Papel` identifica a combinação de perfil e tipo. O PROCV busca a chave na primeira coluna da tabela e retorna o percentual da quarta coluna. `FALSO` exige correspondência exata. Em C21, `=Aporte_Mensal*B21` converte esse percentual em reais. A lista suspensa de B9 usa `lista_perfis`.

## Hipóteses

Os percentuais por perfil vêm dos exemplos didáticos do Guia de Projeto DIO Excel FIIs. A simulação usa valores fictícios, taxas e aportes constantes, capitalização mensal e capital inicial zero. Custos, impostos e inflação ficam fora do cálculo. Os valores servem para praticar Excel e ilustrar o modelo.

## Testes e capturas

As fórmulas foram recalculadas em um ambiente compatível com XLSX. Com salário de R$ 2.000, aporte de R$ 200, prazo de 5 anos e ambas as taxas em 0,5% ao mês, a sugestão ficou em R$ 600, o patrimônio em R$ 13.954,01 e os dividendos em R$ 69,77. O cenário de 5 anos coincidiu com o resultado principal.

| Perfil | Aporte em Papel | Total percentual | Total distribuído |
| --- | ---: | ---: | ---: |
| Conservador | R$ 80,00 | 100% | R$ 200,00 |
| Moderado | R$ 50,00 | 100% | R$ 200,00 |
| Arrojado | R$ 30,00 | 100% | R$ 200,00 |

Com taxa de acumulação zero, o patrimônio calculado foi R$ 12.000,00. A versão entregue abre com taxa de acumulação de 0,5% e perfil Moderado. As imagens mostram os resultados no Excel. A lista suspensa de B9 foi testada no Excel com os três perfis.

- [Captura do perfil Conservador](imagens/perfil_conservador.png)
- [Captura do perfil Moderado](imagens/perfil_moderado.png)
