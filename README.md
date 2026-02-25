DPA Framework — Digital Power Asymmetry
📊 Structural Power Diagnostics for Digital Markets

O DPA Framework (Digital Power Asymmetry) é um modelo analítico proprietário desenvolvido para mensurar poder estrutural em mercados digitais por meio da integração de:

Participação de Atenção

Eficiência de Monetização

Assimetria Estrutural

Concentração Competitiva

O projeto consolida essas dimensões no Digital Power Index (DPI) — um índice sintético de dominância estrutural.

🎯 Objetivo do Projeto

Responder às seguintes questões estratégicas:

Quem detém poder estrutural no mercado digital?

A dominância decorre de escala ou eficiência?

Existe desalinhamento entre atenção e captura de valor?

O mercado está se consolidando ou redistribuindo poder?

O modelo foi implementado em Power BI como um dashboard executivo estruturado em cinco camadas analíticas.

🧠 Estrutura Analítica

O framework é organizado em 5 dimensões:

1️⃣ Estrutura de Mercado

Mede concentração e distribuição de atenção e receita.

HHI_A (Concentração de Atenção)

HHI_R (Concentração de Receita)

Gap de Concentração

2️⃣ Dinâmica Temporal

Avalia evolução do poder competitivo ao longo do tempo.

Trajetória do DPI

Evolução do Power_Gap

Mudança na concentração (HHI)

3️⃣ Sensibilidade Estrutural

Testa robustez do modelo.

Relação entre Share_A e DPI

Elasticidade implícita do poder

Eficiência de monetização (RAM)

4️⃣ Síntese Estratégica

Classificação competitiva consolidada:

Dominante Estrutural

Eficiente em Nicho

Submonetizada

Vulnerável

5️⃣ Metodologia e Framework

Formalização conceitual do modelo e premissas analíticas.

📐 Metodologia
🔷 1. Share_A

Participação relativa de atenção capturada por cada plataforma.

🔷 2. Share_R

Participação relativa de receita no mercado.

🔷 3. RAM (Revenue Attention Multiplier)
RAM=ShareRShareA
RAM=
Share
A
	​

Share
R
	​

Interpretação:

RAM > 1 → Super monetização relativa

RAM < 1 → Sub monetização estrutural

🔷 4. Power_Gap
Power_Gap=ShareR−ShareA
Power_Gap=Share
R
	​

−Share
A
	​
Mede desalinhamento estrutural entre escala e captura de valor.

🔷 5. HHI (Herfindahl-Hirschman Index)
HHI=∑si2
HHI=∑s
i
2
	​
Aplicado tanto à atenção quanto à receita para medir concentração competitiva.

🔷 6. Digital Power Index (DPI)

O DPI é um índice composto que integra:

Escala (Share_A)

Eficiência (RAM)

Assimetria (Power_Gap)

Estrutura de mercado (HHI)

As métricas são normalizadas para permitir integração comparativa.

🏗 Arquitetura do Modelo

A lógica estrutural segue:

ATENÇÃO → EFICIÊNCIA → ASSIMETRIA → PODER ESTRUTURAL

A atenção define escala.

A eficiência determina capacidade de captura.

A assimetria revela distorções estruturais.

O DPI consolida dominância relativa.

📊 Estrutura do Dashboard

O projeto é dividido em 5 páginas:

Página 1 — Visão Geral Estrutural

Fotografia da distribuição de poder no mercado.

Página 2 — Dinâmica Temporal

Evolução da dominância e concentração.

Página 3 — Análise de Sensibilidade

Elasticidade estrutural e robustez competitiva.

Página 4 — Síntese Estratégica

Classificação e posicionamento competitivo.

Página 5 — Metodologia

Formalização do framework.

🧩 Classificação Estratégica

Baseada em regras quantitativas:

Critério	Resultado
Alta escala + Alta eficiência	Dominante Estrutural
Alta eficiência + Baixa escala	Eficiente em Nicho
Alta escala + Baixa eficiência	Submonetizada
Baixa escala + Baixa eficiência	Vulnerável

⚙️ Implementação Técnica

Ferramenta:

Power BI Desktop

Elementos utilizados:

Medidas DAX

Normalização de métricas

Classificação condicional

Formatação executiva

Sem uso de:

Scripts externos

Visuals customizados

Componentes não nativos

⚙️ Implementação Técnica Detalhada

🔹 1. Medidas DAX

O modelo é estruturado integralmente em medidas DAX (Data Analysis Expressions), garantindo cálculo dinâmico e comportamento relativo ao contexto de filtro.

📌 Share_A
Share_A =
DIVIDE(
    SUM(Tabela[Atencao]),
    CALCULATE(SUM(Tabela[Atencao]), ALL(Tabela[Plataforma]))
)
📌 Share_R
Share_R =
DIVIDE(
    SUM(Tabela[Receita]),
    CALCULATE(SUM(Tabela[Receita]), ALL(Tabela[Plataforma]))
)
📌 RAM (Revenue Attention Multiplier)
RAM =
DIVIDE([Share_R], [Share_A])

Interpretação:

1 → Monetização acima da proporção de atenção

< 1 → Sub monetização estrutural

📌 Power_Gap
Power_Gap =
[Share_R] - [Share_A]
📌 HHI (Herfindahl-Hirschman Index)
HHI_A =
SUMX(
    VALUES(Tabela[Plataforma]),
    [Share_A] * [Share_A]
)
HHI_R =
SUMX(
    VALUES(Tabela[Plataforma]),
    [Share_R] * [Share_R]
)
📌 DPI (Digital Power Index)

Exemplo de estrutura simplificada:

DPI_Score =
VAR Escala = [Share_A_Normalizado]
VAR Eficiencia = [RAM_Normalizado]
VAR Assimetria = [Power_Gap_Normalizado]
RETURN
(0.4 * Escala) +
(0.4 * Eficiencia) +
(0.2 * Assimetria)

Os pesos podem ser ajustados conforme o racional analítico.

📐 2. Normalização de Métricas

Como as variáveis possuem escalas distintas, o modelo aplica normalização Min-Max:

Share_A_Normalizado =
VAR MinValor = CALCULATE(MIN([Share_A]), ALL(Tabela[Plataforma]))
VAR MaxValor = CALCULATE(MAX([Share_A]), ALL(Tabela[Plataforma]))
RETURN
DIVIDE(
    [Share_A] - MinValor,
    MaxValor - MinValor
)

A mesma lógica é aplicada a:

RAM

Power_Gap

Objetivo:
Garantir comparabilidade entre dimensões heterogêneas.

🏷 3. Classificação Condicional

Para tradução executiva dos dados numéricos, foram criadas categorias estratégicas via DAX.

📌 Escala
Escala =
SWITCH(
    TRUE(),
    [Share_A] >= 0.30, "Alta",
    [Share_A] >= 0.15, "Média",
    "Baixa"
)
📌 Eficiência
Eficiencia =
SWITCH(
    TRUE(),
    [RAM] > 1.05, "Alta",
    [RAM] >= 0.95, "Média",
    "Baixa"
)
📌 Status Competitivo
Status Competitivo =
SWITCH(
    TRUE(),
    [Escala] = "Alta" && [Eficiencia] = "Alta", "Dominante Estrutural",
    [Eficiencia] = "Alta" && [Escala] = "Baixa", "Eficiente em Nicho",
    [Escala] = "Alta" && [Eficiencia] = "Baixa", "Submonetizada",
    "Vulnerável"
)

Isso permite transformar métricas técnicas em leitura estratégica decisória.

🎨 4. Formatação Executiva

O dashboard foi projetado com padrão institucional e estratégico:

Diretrizes visuais:

Fundo escuro institucional (#0B1220)

Azul elétrico para liderança estrutural

Vermelho discreto para vulnerabilidade

Cinza grafite para elementos neutros

Sem gridlines pesadas

Sem 3D ou efeitos decorativos

Regras aplicadas:

Destaque visual para top performers

Cores condicionais baseadas em status competitivo

Hierarquia forte de títulos e subtítulos

Rodapés técnicos explicativos em cada visual

🧠 Diferencial Técnico

O projeto combina:

✔ Modelagem econômica
✔ Normalização estatística
✔ Classificação estratégica
✔ Visualização executiva

📌 Premissas Analíticas

Poder estrutural é relativo e comparativo.

Escala isolada não garante dominância.

Eficiência de monetização é vetor central de vantagem competitiva.

Concentração de mercado influencia sustentabilidade do poder.

🚀 Possíveis Extensões

Integração com dados financeiros reais

Inclusão de custo de aquisição (CAC)

Simulação de redistribuição de atenção

Modelagem preditiva de mudança estrutural

Expansão para outros setores digitais

📜 Licença

Uso acadêmico e analítico.
Framework proprietário DPA™ — Digital Power Asymmetry.

👤 Autor

[Seu Nome Aqui]

Especialização em:

Estrutura de mercado

Economia digital

Modelagem competitiva

Business Intelligence estratégico

🧠 Diferencial do Projeto

Este não é um dashboard operacional.

É um modelo de leitura estrutural de poder competitivo.

Ele traduz:

Dados → Estrutura → Assimetria → Dominância → Estratégia
