# Fonte de Alimentação Linear de 12 V DC

Projeto académico de uma fonte de alimentação linear, desenvolvido em KiCad no âmbito do TP1 de Sistemas Embebidos, ano letivo 2026/2027.

## Estado do projeto

O desenho da PCB e a visualização 3D foram apresentados pelo autor como concluídos. Esta versão do repositório é de documentação do projeto CAD: não constitui uma versão validada para fabrico ou utilização.

- PCB: 90 × 60 mm, duas camadas de cobre.
- Montagem mista: componentes THT e SMD.
- Saída nominal de projeto: 12 V DC.
- Fabrico, montagem e ensaios: não documentados.
- Resultados finais de ERC e DRC: não disponibilizados neste pacote.

## Objetivo

Desenvolver o esquema elétrico e uma placa de circuito impresso para uma fonte regulada de 12 V DC, aplicando retificação em ponte, filtragem capacitiva e regulação linear com LM7812.

## Funcionamento

Percurso funcional previsto:

```text
Entrada AC isolada → proteção → ponte retificadora → filtragem
                                                   ↓
                                        regulação LM7812
                                                   ↓
                                     comando ON/OFF → saída
```

Quatro díodos 1N4007 realizam a retificação. Um condensador eletrolítico de 470 µF participa na filtragem, e o projeto inclui dois condensadores cerâmicos de 100 nF. O LM7812 fornece a regulação nominal de 12 V. Um LED com resistência em série indica o estado da saída. A ligação efetiva do fusível, interruptor e indicador deve ser confirmada no esquema final.

## Características

| Parâmetro | Descrição |
|---|---|
| Topologia | Fonte linear com ponte retificadora |
| Saída nominal | 12 V DC |
| Corrente contínua de saída | Por validar |
| Gama admissível de entrada | Por validar |
| Regulador | LM7812, TO-220 vertical |
| PCB | 90 × 60 mm, duas camadas |
| Entrada | Jack; referência selecionada 4300.0104 |
| Saída | Phoenix Contact GMSTBA, 1×02, P7,62 mm, horizontal |
| Comando | Interruptor deslizante SPDT PCM12 |
| Fixação | Quatro furos de canto não metalizados |
| Ferramenta de desenvolvimento | KiCad; versão não registada |

## Componentes e footprints

| Referência | Qtd. | Componente | Footprint atribuído / identificado |
|---|---:|---|---|
| D1–D4 | 4 | 1N4007 | `Diode_THT:D_DO-41_SOD81_P7.62mm_Horizontal` |
| C1 | 1 | 470 µF; tensão nominal a rever | `Capacitor_THT:CP_Radial_D6.3mm_P2.50mm` |
| C3, C4 | 2 | 100 nF, cerâmico | `Capacitor_SMD:C_1206_3216Metric` |
| IC2 | 1 | LM7812 | `Package_TO_SOT_THT:TO-220-3_Vertical` |
| R1 | 1 | 4,7 kΩ | `Resistor_SMD:R_0603_1608Metric` |
| D5 | 1 | LED | `LED_SMD:LED_0805_2012Metric` |
| J1 | 1 | Jack 4300.0104 | `Samacsys:43000104` |
| J2 | 1 | Phoenix Contact GMSTBA | GMSTBA 2,5/2-G-7,62; confirmar nome integral no projeto |
| SW1 | 1 | Interruptor SPDT | `Button_Switch_SMD:SW_SPDT_PCM12` |
| F1 | 1 | Fusível e suporte 5 × 20 mm | Suporte Bulgin FX0457; confirmar nome integral |
| H1 | 1 | Dissipador SK104, 25,4 mm | `Samacsys:SK104254STCTO220` |

A BOM fornecida é preliminar e foi transcrita da lista apresentada, não exportada dos ficheiros CAD. Referências comerciais, tolerâncias, potências, calibre do fusível e modelos 3D devem ser confirmados antes de encomendar componentes.

## Mecânica

Os centros dos furos foram propostos a 5 mm das bordas. Para o contorno apresentado, de (94,30; 59,31) mm a (184,30; 119,31) mm:

| Furo | X (mm) | Y (mm) |
|---|---:|---:|
| Superior esquerdo | 99,30 | 64,31 |
| Superior direito | 179,30 | 64,31 |
| Inferior esquerdo | 99,30 | 114,31 |
| Inferior direito | 179,30 | 114,31 |

Estas coordenadas descrevem a proposta de posicionamento; confirmar no ficheiro PCB final. Para parafusos M3 foi proposto o footprint não metalizado `MountingHole:MountingHole_3.2mm_M3`.

## Requisitos do trabalho

O enunciado exige duas camadas de cobre, planos de massa em TOP e BOT com clearance de 0,5 mm, identificação em serigrafia e furos não metalizados nos cantos. A lista de entregáveis inclui esquema PDF, visualização 3D, BOM e ficheiros Gerber com furação metalizada e não metalizada.

A implementação destes requisitos deve ser verificada no projeto final. O enunciado designa o encapsulamento dos díodos como SOD68; o footprint selecionado usa a designação DO-41/SOD81. Esta diferença deve ser esclarecida antes do fabrico.

## Segurança e pontos críticos

- Alimentar apenas por uma fonte AC de baixa tensão isolada da rede. Não ligar diretamente a 230 V.
- A serigrafia apresentada indica entrada de 15–25 V AC, mas essa gama não está validada.
- A BOM apresentada inclui C1 de 470 µF / 25 V. Não considerar esta tensão nominal adequada para toda a gama inscrita na serigrafia.
- Rever a tensão máxima após retificação, incluindo tolerância e funcionamento sem carga, antes de escolher C1 e o regulador.
- Confirmar os limites do fabricante e da referência exata do LM7812. Limites absolutos não são condições normais de operação.
- A corrente de saída depende da tensão de entrada, ondulação, retificador, fusível, pistas e dissipação térmica.
- Confirmar o contacto térmico e a montagem do dissipador; o modelo 3D não valida o desempenho térmico.
- Corrigir a serigrafia para corresponder às condições efetivamente validadas.

## Organização

```text
README.md
.gitignore
bom/
  bom_preliminar.csv
docs/
  VALIDACAO.md
  PUBLICACAO.md
  images/             # acrescentar imagens reais
hardware/             # acrescentar projeto KiCad real
fabrication/
  gerbers/            # acrescentar apenas exportações revistas
  drill/              # acrescentar furação PTH e NPTH
```

Não foram criados ficheiros CAD, imagens, Gerbers ou relatórios de ensaio fictícios. As pastas técnicas destinam-se a receber os ficheiros reais do autor.

## Abrir o projeto

Depois de adicionar os ficheiros originais, abrir o `.kicad_pro` no KiCad e confirmar as tabelas de bibliotecas. Incluir símbolos, footprints e modelos 3D personalizados necessários. Usar caminhos relativos ao projeto sempre que possível e verificar ERC e DRC antes de exportar ficheiros de fabrico.

## Contexto académico

- Curso: Licenciatura em Engenharia Eletrotécnica e das Telecomunicações.
- Unidade curricular: Sistemas Embebidos.
- Trabalho: TP1 — Projeto de PCBs com KiCad.
- Ano letivo: 2026/2027.

## Autoria

O identificador associado ao projeto é `Kayaboook`, conforme o endereço inscrito no código da PCB. Os nomes completos dos autores não foram confirmados neste pacote. A autoria e a autorização dos restantes elementos do grupo devem ser revistas antes da publicação.

## Licença

Não foi atribuída uma licença neste pacote. A disponibilização pública não concede, por si só, uma licença de reutilização. Os autores devem selecionar uma licença adequada e respeitar as licenças das bibliotecas e modelos de terceiros.
