# Cola de apresentação — Prática 3

Acompanhe a numeração do [PDF da apresentação](Apresentação_-_Romario_Jonas.pdf). Use as falas como lembretes; destaque o comportamento dos circuitos sem ler todas as tabelas.

## Slide 1 — Filtro Ativo Passa-Baixa de Segunda Ordem

“Vou apresentar a análise de dois filtros ativos de segunda ordem, comparando a resposta em frequência e a resposta ao degrau.”

## Slide 2 — Sumário

“Começo pelo circuito e pela modelagem, apresento as previsões teóricas e depois comparo com a simulação e a bancada.”

## Slide 3 — Contexto da prática

“A pergunta central é como a troca de dois resistores modifica o ganho e o amortecimento. Vou observar tanto sinais senoidais quanto a aplicação de um degrau.”

## Slide 4 — Objetivos

“O objetivo é obter a função de transferência, encontrar os polos e usar esse modelo para explicar os gráficos de Bode e os transitórios.”

## Slide 5 — Metodologia de validação

“A análise foi organizada em três etapas: cálculo simbólico, simulação no LTspice e medições em bancada.”

**Lembrete:** ganho de magnitude é a razão entre as amplitudes de saída e entrada; o intervalo entre 10% e 90% é $t_r=t_{90}-t_{10}$.

## Slide 6 — Circuito ativo e configurações estudadas

“A topologia permanece a mesma. A mudança está na troca dos valores de $R_1$ e $R_3$.”

- **Circuito 1:** $R_1=47\,k\Omega$ e $R_3=470\,k\Omega$.
- **Circuito 2:** valores invertidos.
- **Comuns:** $R_2=470\,k\Omega$, $C_1=100\,nF$ e $C_2=10\,nF$.

## Slide 7 — Modelagem no domínio de Laplace

“No modelo ideal, não entra corrente nos terminais do ampop. Com realimentação negativa, o terminal inversor fica em terra virtual. Aplico a lei das correntes e isolo $V_o/V_i$.”

**Aponte:** as duas equações nodais à esquerda e a função de transferência à direita. O ganho em corrente contínua é $H(0)=-R_2/R_1$.

## Slide 8 — Funções de transferência e polos

“Substituindo os componentes do primeiro circuito, obtenho a função numérica pedida no roteiro:”

$$
H_1(s)=\frac{-470000}{10{,}3823s^2+2650{,}8s+47000}.
$$

- **Polos do circuito 1:** $-19{,}17$ e $-236{,}15\,s^{-1}$; reais e negativos, com resposta sobreamortecida.
- **Polos do circuito 2:** $-127{,}66\pm j170{,}21\,s^{-1}$; complexos, com oscilação amortecida.

“Ambos são estáveis. O ganho DC passa de −10 para −1; o sinal negativo indica inversão.”

## Slide 9 — Resposta teórica em frequência

“Para obter o Bode, substituo $s=j2\pi f$, calculo $20\log_{10}|H|$ e a fase.”

**Aponte nos gráficos:**

- Circuito 1: magnitude inicial de **20 dB** e queda sem pico.
- Circuito 2: magnitude inicial de **0 dB** e pico suave próximo de **17,9 Hz**.
- Em altas frequências: queda de **40 dB por década**. A fase aparece de **180° a 0°**, ramo equivalente a −180° até −360°.

## Slide 10 — Do degrau à resposta no tempo

“Um degrau de 0,8 V corresponde a $V_i(s)=0{,}8/s$. Multiplico por $H_1(s)$ e aplico a inversa de Laplace:”

$$
v_{o1}(t)\approx-8+8{,}7068e^{-19{,}1698t}-0{,}7068e^{-236{,}1494t},\qquad t\geq0.
$$

“As exponenciais desaparecem com o tempo. Pelo teorema do valor final, $v_o(\infty)=A\,H(0)$: **−8 V** no circuito 1 e **−5 V** no circuito 2.”

**Lembrete:** $t$ está em segundos; o teorema é aplicável porque os polos de $sV_o(s)$ têm parte real negativa.

## Slide 11 — Resposta teórica ao degrau

“Aqui visualizamos essas expressões. O primeiro circuito chega ao valor final sem oscilar; o segundo apresenta sobressinal e depois se acomoda.”

**Aponte:** o circuito 1 está representado de **0 a 500 ms**, ou **0 a 0,5 s**, como solicitado. O circuito 2 mostra os primeiros 60 ms.

## Slide 12 — Níveis de 10% e 90% da resposta

“Como o valor final é negativo, os níveis de 10% e 90% também são negativos. Resolvo a expressão temporal para encontrar o primeiro instante de cada cruzamento.”

| Circuito | Níveis de 10% / 90% | $t_{10}$ | $t_{90}$ | $t_r$ |
| --- | --- | --- | --- | --- |
| 1 | −0,8 / −7,2 V | 9,35 ms | 124,53 ms | 115,18 ms |
| 2 | −0,5 / −4,5 V | 2,33 ms | 11,05 ms | 8,71 ms |

“O circuito 2 faz essa transição mais rapidamente.” **São valores teóricos**, com arredondamento ao final dos cálculos.

## Slide 13 — Validação no LTspice: circuitos

“Reproduzi as duas configurações para comparar com as previsões do modelo.”

**Aponte:** alimentação de **±10 V**, entrada AC unitária e varredura de **0,01 a 100.000 Hz**. Nos transitórios, os degraus são de **0,8 V** e **5 V**.

## Slide 14 — Validação no LTspice: resposta em frequência

“As simulações reproduzem a característica passa-baixa e a diferença entre as configurações: queda gradual no primeiro circuito e pequeno pico no segundo.”

**Lembrete:** a comparação dessas capturas é qualitativa; não apresentar um erro numérico de simulação que não foi calculado.

## Slide 15 — Montagem e conferência dos componentes

“Os valores reais dos componentes diferem dos nominais. Essas tolerâncias podem deslocar o ganho e os polos.”

**Exemplos:** $C_1=109{,}9\,nF$ e $C_2=11{,}42\,nF$. A identificação dos resistores na tabela corresponde ao **circuito 2**.

## Slide 16 — Amplitudes medidas em bancada

“Estas tabelas mostram a atenuação da saída com o aumento da frequência. A entrada também variou, então preciso considerar o ganho $V_o/V_i$ em cada ponto.”

**Destaques:** entrada de **78–155 mV** no circuito 1 e **4,7–5,1 V** no circuito 2. Não é necessário ler todas as linhas.

## Slide 17 — Formas de onda transitórias registradas

“As capturas mostram a diferença prevista: resposta monótona no primeiro circuito e oscilação amortecida no segundo.”

**Aponte:** cursores em **−7,2 V / 160 ms** e **−4,5 V / 13,4 ms**. São leituras das capturas; para obter tempos a partir do degrau, é preciso conferir a referência temporal. Não usá-las isoladamente para calcular $t_r$.

## Slide 18 — Comparação entre teoria e experimento

“A linha representa o modelo nominal e os pontos representam os ganhos medidos. Dividir a saída pela entrada permite comparar pontos obtidos com excitações diferentes.”

**Exemplo rápido:** no circuito 1, em 0,6 Hz, $|H|=0{,}750/0{,}078\approx9{,}62$.

## Slide 19 — Discussão dos resultados e limites dos registros

“O corte registrado do circuito 1 foi **4,3 Hz**, diante de **3,03 Hz** teóricos: desvio de **41,9%**. No circuito 2, o pico registrado foi **17,5 Hz**, diante de **17,92 Hz**: desvio de **2,3%**.”

**Lembretes:** corte e pico são grandezas diferentes. A variação da entrada exige analisar o ganho normalizado. As tolerâncias e as leituras podem contribuir para os desvios, mas não permitem isolar uma única causa. Sem pares experimentais de 10% e 90%, não informar $t_r$ medido.

## Slide 20 — Conclusões

“A troca dos resistores reduziu o ganho DC e mudou o amortecimento. A posição dos polos explica tanto o Bode quanto o transitório: resposta mais lenta e monótona no primeiro circuito, mais rápida e oscilatória no segundo.”

## Slide 21 — Referências bibliográficas

“Estas são as bases teóricas, os materiais da disciplina e as ferramentas utilizadas na análise.”

## Slide 22 — Obrigado

“Obrigado pela atenção. Fico à disposição para as perguntas.”

## Consulta rápida — Perguntas do roteiro

| Pergunta | Onde responder |
| --- | --- |
| 1. Função de transferência numérica | Slide 8 |
| 2. Polos da função de transferência | Slide 8 |
| 3. Bode de magnitude e fase | Slide 9 |
| 4. Resposta ao degrau de 0,8 V | Slide 10 |
| 5. Valor de convergência | Slide 10: **−8 V** |
| 6. Gráfico entre 0 e 0,5 s | Slide 11, à esquerda |
| 7. Tempos de 10% e 90% | Slide 12: **9,35 ms e 124,53 ms** |
