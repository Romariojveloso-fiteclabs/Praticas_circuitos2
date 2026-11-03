# Cola de apresentação — Prática 4

Acompanhe a numeração do [PDF da apresentação](Apresentação_-_Romario_Jonas.pdf). Destaque as mudanças de ganho e de frequência de corte; use as tabelas como apoio.

## Slide 1 — Filtro RC Passa-Baixa e Efeito de Carga

“Vou apresentar um filtro RC passa-baixa em três condições: sem carga, com carga direta e com uma carga isolada por buffer.”

## Slide 2 — Sumário

“Começo pela modelagem e pelo projeto, mostro as simulações e depois comparo as previsões com as medições de bancada.”

## Slide 3 — Contexto da prática

“A questão central é como uma carga modifica o comportamento de um filtro passivo e como um seguidor de tensão pode reduzir essa influência.”

**Aponte:** ganho em baixas frequências e frequência de corte são as grandezas principais.

## Slide 4 — Objetivos

“Vou obter as três funções de transferência, projetar o filtro para 50 Hz e verificar como a carga altera o ganho e o corte.”

## Slide 5 — Metodologia de validação

“A análise segue três etapas: equações e cálculo simbólico, simulação no LTspice e medições de entrada e saída em bancada.”

**Lembrete:** calcular $|H|=V_o/V_i$ em cada frequência, porque a entrada varia durante a varredura.

## Slide 6 — Três configurações do filtro RC

“No circuito 1, a saída está sobre o capacitor. No circuito 2, a carga fica em paralelo com ele. No circuito 3, o buffer fica entre o filtro e a carga.”

**Aponte nos diagramas:** o elemento alterado em cada etapa e a posição da saída.

## Slide 7 — Circuito 1: modelagem sem carga

“Uso $Z_C=1/(sC)$ e a lei das correntes: $(V_i-V_o)/R=sCV_o$. Isolando a razão entre saída e entrada:”

$$
H_1(s)=\frac{1}{1+sRC},\qquad K_1=1,\qquad f_{c1}=\frac{1}{2\pi RC}.
$$

“O polo é negativo, $p=-1/(RC)$, e o circuito é um passa-baixa de primeira ordem.”

**Fonte não ideal:** uma resistência série $R_s$ soma-se a $R$ quando a referência é a tensão ideal do gerador. Na bancada, $V_i$ é medido na entrada do filtro.

## Slide 8 — Projeto para frequência de corte de 50 Hz

“Com $C=100\,nF$ e $f_c=50\,Hz$, o resistor calculado é 31,83 kΩ. Escolhendo o valor comercial de 33 kΩ, o corte passa a 48,23 Hz.”

**Valores essenciais:** $H_1(s)=1/(1+0{,}0033s)$, ganho DC unitário e constante de tempo de **3,3 ms**.

## Slide 9 — Circuito 2: efeito da carga resistiva

“Agora a corrente do resistor se divide entre o capacitor e a carga: $(V_i-V_o)/R=sCV_o+V_o/R_L$.”

$$
H_2(s)=\frac{R_L}{R+R_L+sCRR_L}
=\frac{K_2}{1+s(R\parallel R_L)C},\qquad K_2=\frac{R_L}{R+R_L}.
$$

“No projeto com R = 33 kΩ e carga de 22 kΩ, o ganho cai para **0,4**, ou **−7,96 dB**, e o corte sobe para **120,57 Hz**. A resistência equivalente menor reduz a constante de tempo.”

## Slide 10 — Circuito 3: isolamento da carga com buffer

“No modelo ideal, a entrada do ampop não consome corrente. A realimentação faz a saída acompanhar a tensão do capacitor, e o ampop fornece a corrente da carga.”

$$
H_3(s)=H_1(s)=\frac{1}{1+sRC}.
$$

**Resposta do roteiro:** ganho DC volta a **1** e o corte nominal a **48,23 Hz**. A carga desaparece da função de transferência ideal.

## Slide 11 — Resposta nominal em frequência

“Os diagramas mostram o efeito de carga: o patamar de passagem diminui e o corte se desloca. As curvas sem carga e com buffer ideal coincidem.”

**Aponte:** queda de **20 dB por década**, fase de **0° a −90°** e ganho inicial de **0 dB** ou **−7,96 dB**, conforme a configuração.

## Slide 12 — Como identificar a frequência de corte

“O corte ocorre quando a magnitude cai para $K/\sqrt{2}$, isto é, 3 dB abaixo do patamar de passagem.”

- Sem carga ou com buffer ideal: ganho no corte **0,707**.
- Com carga nominal: ganho no corte **0,283**, correspondente a **−10,97 dB absolutos**.

**Lembrete:** usar entrada e saída na mesma convenção, como tensão pico a pico. A função de transferência se refere à entrada efetivamente medida no filtro.

## Slide 13 — Validação no LTspice: três configurações

“As simulações reproduzem o projeto nominal com R = 33 kΩ, C = 100 nF e carga de 22 kΩ.”

**Configuração:** fonte AC unitária, varredura de **0,01 a 100.000 Hz**, 20 pontos por década e alimentação de **±10 V** no buffer.

## Slide 14 — Validação no LTspice: diagramas de Bode

“As capturas mostram o patamar unitário sem carga, a atenuação com carga direta e a recuperação com o buffer.”

**Lembrete:** são simulações do projeto nominal; a comparação dessas imagens é qualitativa.

## Slide 15 — Montagens e componentes medidos

“Os componentes da bancada diferem dos valores do projeto. Por isso, recalculo o modelo para cada conjunto medido.”

**Destaques:** resistores de filtro próximos de **22 kΩ**, capacitores de **103,80 a 110,90 nF** e cargas próximas de **32 kΩ**. As fotografias ilustram as três topologias.

## Slide 16 — Amplitudes medidas nas três configurações

“A varredura vai de 0,02 a 20 vezes o corte registrado. As tabelas trazem as tensões pico a pico de entrada e saída, convertidas para volts.”

**Valores registrados:** **67 Hz** sem carga, **121 Hz** com carga direta e **69 Hz** com buffer. Não é necessário ler todas as linhas.

## Slide 17 — Funções de transferência com componentes medidos

“Substituindo os componentes aferidos nas expressões gerais, obtenho as previsões ajustadas à bancada.”

| Circuito | Ganho DC teórico | Corte teórico |
| --- | --- | --- |
| Sem carga | 1 | 70,20 Hz |
| Carga direta | 0,59472 | 109,58 Hz |
| Buffer | 1 | 68,83 Hz |

“As constantes de tempo são, respectivamente, **2,2671**, **1,4524** e **2,3123 ms**. A diferença entre os cortes dos circuitos 1 e 3 acompanha seus componentes medidos.”

## Slide 18 — Comparação em bancada: filtro sem carga

“A linha usa os componentes medidos; os pontos usam $V_o/V_i$. A 1 Hz, o ganho medido foi $469{,}1/483{,}2\approx0{,}971$.”

**Compare:** corte teórico de **70,20 Hz** e registro de **67 Hz**; diferença de **4,56%**.

## Slide 19 — Comparação em bancada: carga direta

“A carga reduz o patamar de passagem. A medição em baixa frequência dá $0{,}460/1{,}140\approx0{,}404$, enquanto o modelo com os componentes aferidos prevê 0,595.”

“Para esse patamar medido, o nível de corte é aproximadamente **0,285**. Em **121 Hz**, a razão medida é **0,288**, próxima desse nível.”

**Lembrete:** o corte teórico ajustado é **109,58 Hz**; o desvio de ganho permanece visível e será discutido.

## Slide 20 — Comparação em bancada: isolamento com buffer

“Com o buffer, o ganho em baixa frequência volta para perto da unidade: $480/500=0{,}960$.”

**Compare:** corte teórico de **68,83 Hz** e registro de **69 Hz**; diferença de **0,25%**. O comportamento se aproxima daquele sem carga.

## Slide 21 — Síntese dos resultados e limites da comparação

“As tendências do efeito de carga e da recuperação pelo buffer aparecem nas medições. O maior desvio está no ganho do circuito 2: **32,15%** em relação ao modelo ajustado.”

**Se perguntarem a causa:** conferir componentes, conexões e referência da tensão de entrada. Os dados não permitem atribuir todo o desvio a uma única causa ou apenas à tolerância.

**Se perguntarem sobre ganho acima de 1 em um ponto:** é uma razão entre leituras experimentais; o modelo do filtro passivo continua prevendo ganho máximo unitário.

## Slide 22 — Conclusões

“A carga altera o divisor de tensão e a resistência vista pelo capacitor, reduzindo o ganho e deslocando o corte. O buffer isola os estágios e recupera a resposta próxima da condição sem carga.”

**Fechamento:** o resultado depende da carga e das condições reais de medição, além dos componentes do filtro.

## Slide 23 — Referências bibliográficas

“Estas são as bases de análise de circuitos, o roteiro da disciplina e as ferramentas utilizadas.”

## Slide 24 — Obrigado

“Obrigado pela atenção. Fico à disposição para as perguntas.”

## Consulta rápida — Atividades do roteiro

| Atividade | Slides |
| --- | --- |
| Equações, função de transferência, ganho e corte sem carga | 7 |
| Projeto de 50 Hz com capacitor de 100 nF e resistor comercial | 8 |
| Equações, função de transferência e efeito da carga | 9 |
| Modelo do ampop, função de transferência e restauração pelo buffer | 10 |
| Diagramas de Bode e comparação das configurações | 11–12 |
| Representação e análise AC no LTspice | 13–14 |
| Valores reais dos componentes | 15 |
| Tabelas de tensões e varredura em frequência | 16 |
| Recálculo das funções com os componentes medidos | 17 |
| Sobreposição em escala log-log e comparação dos ganhos e cortes | 18–21 |
