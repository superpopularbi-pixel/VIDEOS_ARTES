═══════════════════════════════════════════════════════════════════════════════
                    DOCUMENTAÇÃO DO RELATÓRIO
                    MELHORES DO ANO 2026 INTERNO
═══════════════════════════════════════════════════════════════════════════════

═══════════════════════════════════════════════════════════════════════════════
1. INTRODUÇÃO AO RELATÓRIO
═══════════════════════════════════════════════════════════════════════════════

O Dashboard "MELHORES DO ANO 2026 INTERNO" é um relatório analítico desenvolvido
no Power BI para reconhecimento e premiação dos melhores colaboradores e filiais
do ano. O modelo foi construído com a cultura pt-BR e está em modo de importação 
(Import).

OBJETIVO DO RELATÓRIO:
---------------------
O relatório tem como objetivo principal:

• Promover engajamento e competitividade saudável entre colaboradores
• Reconhecer e premiar os melhores desempenhos em múltiplas categorias
• Estabelecer um sistema de pontuação justo e transparente
• Acompanhar indicadores-chave de performance (KPIs)
• Identificar destaques mensais em diferentes áreas de atuação
• Fornecer insights sobre crescimento de vendas e tendências

CATEGORIAS DE PREMIAÇÃO:
-----------------------
O relatório contempla as seguintes categorias de premiação:

1. **Farmácia Destaque**: Ranking de filiais com base em pontuação geral
2. **Top Faturamento**: Melhores vendedores (Balconistas e Farmacêuticos)
3. **Top Indústrias**: Parceiros que mais venderam produtos de fabricantes específicos
4. **Top Marcas Próprias**: Vendedores com maior faturamento em marcas próprias
5. **Top Folguista (Multiplas Filiais)**: Encarregados Externos atuando em várias filiais
6. **Top Promotor de Vendas**: Melhores promotoras de vendas
7. **Top Atendente**: Ranking de atendentes por pontuação
8. **Top Auxiliar**: Ranking de auxiliares por pontuação
9. **Top Parceiro da Semana**: Destaque semanal

SISTEMA DE PONTUAÇÃO:
--------------------
O sistema utiliza um modelo de pontos baseado em 8 indicadores principais:

1. **Faturamento** (70-120 pontos)
2. **Delivery** (70-120 pontos)
3. **PBM - Programa de Benefício de Medicamentos** (até 100 pontos)
4. **Fidelidade** (75-100 pontos)
5. **Inventário** (0-100 pontos)
6. **Validade** (0-100 pontos)
7. **CMV - Custo de Mercadoria Vendida** (0-100 pontos)
8. **Ticket Médio** (-∞ a 200 pontos)

Pontos adicionais:
• **Marcas Próprias**: 1 ponto por cada R$ 100,00 em vendas
• **Harmo**: Pontos por participação em programa específico

ESTRUTURA DO MODELO:
-------------------
O modelo de dados é composto por 41 tabelas:

• **Tabelas Fato (f_*)**:
  - f_venda: Transações de vendas (29 colunas)
  - f_MetaMensalFilial: Metas mensais por filial (18 colunas)
  - f_PBM_interno: Controle interno de PBM (9 colunas)
  - f_Fidelidade: Dados do programa de fidelidade (13 colunas)
  - f_PBM: Programa de Benefício de Medicamentos (13 colunas)
  - f_Fidelidades: Fidelidade consolidada (10 colunas)
  - f_fidelidadeFinal: Versão final de fidelidade (8 colunas)
  - f_Entregas: Dados de entregas (6 colunas)

• **Tabelas Dimensão (d_*)**:
  - d_Calendario: Dimensão temporal (11 colunas + 1 hierarquia)
  - d_Filial: Cadastro de filiais (8 colunas)
  - d_FuncionarioCargo: Função dos colaboradores (4 colunas)
  - d_Classe_Filiais: Classificação de filiais (4 colunas)
  - d_ProdutosMarcasProprias: Produtos de marca própria (3 colunas)
  - d_MetavsReal_Consolidado: Comparativo meta x realizado (11 colunas)
  - d_fabricanteTopIndustria: Fabricantes do Top Indústrias (1 coluna)

• **Tabelas de Rankings (Top_*)**:
  - Top_Farmacia_Destaque: Destaques de farmácias (10 colunas)
  - Top_Industrias: Ranking de indústrias parceiras (29 colunas)
  - Top_Atendente: Ranking de atendentes (9 colunas)
  - Top_Auxiliar: Ranking de auxiliares (12 colunas)
  - Top_AuxiliarConsolidado: Consolidado de auxiliares (8 colunas)
  - Top_Jogando_ADM: ADMs em jogo (5 colunas)
  - Top_Parceiro_Semana: Parceiro da semana (7 colunas)
  - Top_Atendente_Quebra: Quebras de atendentes (5 colunas)
  - Top Folguista: Vendedores múltiplas filiais (4 colunas + 1 medida)
  - Top Promotora de Vendas: Promotoras (3 colunas)

• **Tabelas Auxiliares**:
  - _Medida: Centraliza todas as medidas DAX (102 medidas)
  - UltimaAtualizacao: Data/hora da última atualização (1 coluna)
  - DateTableTemplate: Templates de calendário automático

INDICADORES PRINCIPAIS:
----------------------
• Pontuação Geral (Soma de 8 indicadores)
• Faturamento e Metas
• Delivery e Entregas
• PBM (Programa de Benefício de Medicamentos)
• Fidelidade de Clientes
• Controle de Inventário
• Gestão de Validades
• CMV (Custo de Mercadoria Vendida)
• Ticket Médio (TKM)
• Marcas Próprias
• Programa Harmo

Data de Última Modificação do Modelo: 18/08/2025
Data de Última Modificação da Estrutura: 20/01/2026


═══════════════════════════════════════════════════════════════════════════════
2. DOCUMENTAÇÃO DETALHADA DAS MEDIDAS DAX
═══════════════════════════════════════════════════════════════════════════════

───────────────────────────────────────────────────────────────────────────────
CATEGORIA: SISTEMA DE PONTUAÇÃO - INDICADORES MENSAIS
───────────────────────────────────────────────────────────────────────────────

1. PontosFaturamento_Mes
────────────────────────
DESCRIÇÃO: Soma os pontos de faturamento agrupados por mês.
FÓRMULA DAX:
    SUMX(VALUES(d_Calendario[AnoMês]), [PontosFaturamento])

FORMATO: Número decimal
OBSERVAÇÕES: Utiliza SUMX para iterar sobre cada mês e somar os pontos 
individuais de faturamento. Essencial para consolidação mensal.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


2. Pontos_Delivery_Mes
──────────────────────
DESCRIÇÃO: Soma os pontos de delivery agrupados por mês.
FÓRMULA DAX:
    SUMX(VALUES(d_Calendario[AnoMês]), [Pontos_Delivery])

FORMATO: Número decimal
OBSERVAÇÕES: Consolida mensalmente os pontos de entregas/delivery.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


3. Pontos PBM Mês
─────────────────
DESCRIÇÃO: Soma os pontos de PBM por mês, apenas se forem positivos.
FÓRMULA DAX:
    IF([Pontos_PBM] > 0, SUMX(VALUES(d_Calendario[AnoMês]), [Pontos_PBM]))

FORMATO: Número decimal
OBSERVAÇÕES: Verifica se há pontos positivos antes de somar. Evita 
contabilização de valores negativos.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


4. PontosFidelidade_Mes
───────────────────────
DESCRIÇÃO: Soma os pontos de fidelidade agrupados por mês.
FÓRMULA DAX:
    SUMX(VALUES(d_Calendario[AnoMês]), [PontosFidelidade])

FORMATO: Número decimal
OBSERVAÇÕES: Consolidação mensal dos pontos de fidelidade.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


5. PontosInventario_Mes
───────────────────────
DESCRIÇÃO: Soma os pontos de inventário agrupados por mês.
FÓRMULA DAX:
    SUMX(VALUES(d_Calendario[AnoMês]), [Pontos_Inventario])

FORMATO: Número inteiro
OBSERVAÇÕES: Pontuação relacionada à gestão de inventário.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


6. Pontos Validade Mês
──────────────────────
DESCRIÇÃO: Soma os pontos de validade agrupados por mês.
FÓRMULA DAX:
    SUMX(VALUES(d_Calendario[AnoMês]), [Pontos_Validade])

FORMATO: Número inteiro
OBSERVAÇÕES: Pontuação de controle de produtos próximos ao vencimento.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


7. Ponto_CMV_Mes
────────────────
DESCRIÇÃO: Soma os pontos de CMV agrupados por mês.
FÓRMULA DAX:
    SUMX(VALUES(d_Calendario[AnoMês]), [Pontos_CMV])

FORMATO: Número inteiro
OBSERVAÇÕES: Pontuação do Custo de Mercadoria Vendida.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


8. Pontos Ticketmedio Mês
─────────────────────────
DESCRIÇÃO: Soma os pontos de ticket médio agrupados por mês.
FÓRMULA DAX:
    SUMX(VALUES(d_Calendario[AnoMês]), [Pontos_TicketMedio])

FORMATO: Número decimal
OBSERVAÇÕES: Consolida mensalmente os pontos de ticket médio.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


9. Ponto_Total_Mes
──────────────────
DESCRIÇÃO: Calcula o total de pontos do Super Gerente por mês.
FÓRMULA DAX:
    SUMX(VALUES(d_Calendario[Date].[Mês]), [Pontos_Totais_SuperGerente])

FORMATO: Número decimal
OBSERVAÇÕES: Soma total de todos os indicadores para ranking de filiais.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


10. Pontos_MarcasProprias_Mes
─────────────────────────────
DESCRIÇÃO: Soma os pontos de marcas próprias agrupados por mês.
FÓRMULA DAX:
    SUMX(VALUES(d_Calendario[Date].[Mês]),[Pontos_Marcas_Proprias])

FORMATO: Número decimal
OBSERVAÇÕES: Pontuação adicional por vendas de marcas próprias.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: CÁLCULO DE PONTOS POR INDICADOR
───────────────────────────────────────────────────────────────────────────────

11. PontosFaturamento
─────────────────────
DESCRIÇÃO: Calcula pontos baseados no % de atingimento da meta de faturamento.
FÓRMULA DAX:
    VAR MetaLoja = MAX(f_MetaMensalFilial[Meta faturamento])
    VAR Realizado = SUM(f_venda[valortotal])
    VAR Percentual = DIVIDE(Realizado, MetaLoja, 0) * 100
    RETURN
        IF(
            Percentual >= 70,
            MIN(Percentual, 120),
            0
        )

FORMATO: Número decimal
OBSERVAÇÕES: 
- Mínimo de 70% da meta para pontuar
- Máximo de 120 pontos
- Linear entre 70% e 120%
ÚLTIMA MODIFICAÇÃO: 05/01/2026


12. Pontos_Delivery
───────────────────
DESCRIÇÃO: Calcula pontos de delivery com tratamento especial para filiais sem entregas.
FÓRMULA DAX:
    VAR MetaLoja = SUM ( f_MetaMensalFilial[Meta Delivery] )
    VAR Realizado = [delivery]
    VAR Percentual = DIVIDE ( Realizado, MetaLoja, 0 ) * 100
    VAR Media = CALCULATE (
        AVERAGE ( f_venda[valortotal] ),
        f_venda[tipo_registro] = "Entrega",
        ALL ( f_venda )
    )
    VAR PossuiEntrega = 
        NOT ISBLANK(
            CALCULATE(
                COUNTROWS(f_venda),
                f_venda[tipo_registro] = "Entrega"
            )
        )
    RETURN
        IF (
            NOT PossuiEntrega, 
            Media,
            IF (
                Percentual >= 70,
                MIN ( Percentual, 120 ),
                0
            )
        )

FORMATO: Número decimal
OBSERVAÇÕES:
- Filiais sem delivery recebem média geral (não penalizadas)
- Mínimo 70% da meta para pontuar
- Máximo 120 pontos
ÚLTIMA MODIFICAÇÃO: 20/01/2026


13. Pontos_PBM
──────────────
DESCRIÇÃO: Calcula pontos de PBM com penalização abaixo de 80%.
FÓRMULA DAX:
    VAR result1 = IF(ISBLANK(SUMX(VALUES(d_Calendario[Date]),[PBM])), 0, [PBM])
    VAR Resultado_PBM_pct = result1 * 100
    RETURN
        IF(
            Resultado_PBM_pct >= 80,
            Resultado_PBM_pct,
            (Resultado_PBM_pct- 80) * 10
        )

FORMATO: Número decimal
OBSERVAÇÕES:
- Acima de 80%: pontos = percentual
- Abaixo de 80%: penalização de 10x a diferença
- Exemplo: 75% → (75-80)*10 = -50 pontos
ÚLTIMA MODIFICAÇÃO: 07/01/2026


14. PontosFidelidade
────────────────────
DESCRIÇÃO: Calcula pontos de fidelidade com penalização abaixo de 75%.
FÓRMULA DAX:
    VAR Resultado = [calculo_fidelidad] * 100
    RETURN
        IF(
            Resultado >= 75,
            MIN(Resultado, 100),
            (Resultado - 75) * 10
        )

FORMATO: Número decimal
OBSERVAÇÕES:
- Entre 75% e 100%: pontos = percentual (máx 100)
- Abaixo de 75%: penalização de 10x a diferença
ÚLTIMA MODIFICAÇÃO: 05/01/2026


15. Pontos_Inventario
─────────────────────
DESCRIÇÃO: Pontuação por faixas de percentual de inventário.
FÓRMULA DAX:
    VAR Resultado = AVERAGE(f_MetaMensalFilial[Inventario_realizado])
    RETURN
        SWITCH(
            TRUE(),
            ISBLANK(Resultado) || resultado = 0,0,
            Resultado <= 0.002, 100,
            Resultado <= 0.0029, 70,
            Resultado <= 0.004, 30,
            Resultado > 0.004, (0.004 - Resultado) * 1000000
        )

FORMATO: Número decimal
OBSERVAÇÕES:
- 0,00% a 0,20%: 100 pontos
- 0,20% a 0,29%: 70 pontos
- 0,30% a 0,40%: 30 pontos
- Acima de 0,40%: penalização
ÚLTIMA MODIFICAÇÃO: 03/01/2026


16. Pontos_Validade
───────────────────
DESCRIÇÃO: Pontuação por faixas de percentual de validade.
FÓRMULA DAX:
    VAR Resultado = SUM(f_MetaMensalFilial[Validade_realizado])
    RETURN
        SWITCH(
            TRUE(),
            ISBLANK(Resultado), 0,
            Resultado <= 0.001, 100,
            Resultado <= 0.0019, 70,
            Resultado <= 0.0025, 30,
            Resultado > 0.0025, (0.0025 - Resultado) * 1000000
        )

FORMATO: Número decimal
OBSERVAÇÕES:
- 0,00% a 0,10%: 100 pontos
- 0,10% a 0,19%: 70 pontos
- 0,20% a 0,25%: 30 pontos
- Acima de 0,25%: penalização
ÚLTIMA MODIFICAÇÃO: 03/01/2026


17. Pontos_CMV
──────────────
DESCRIÇÃO: Pontuação baseada no CMV vs meta.
FÓRMULA DAX:
    VAR MetaLoja = MAX(f_MetaMensalFilial[CMV])
    VAR Realizado = [cmv]
    VAR Relacao = DIVIDE(Realizado, MetaLoja)
    RETURN
    IF(
        Relacao <= 0.97,
        100,
        IF(
            Relacao > 1,
            0,
            50
        )
    )

FORMATO: Número inteiro
OBSERVAÇÕES:
- Até 97% da meta: 100 pontos (excelente)
- Entre 97% e 100%: 50 pontos (ok)
- Acima de 100%: 0 pontos (ruim)
ÚLTIMA MODIFICAÇÃO: 03/01/2026


18. Pontos_TicketMedio
──────────────────────
DESCRIÇÃO: Pontuação de ticket médio com bônus acima de meta.
FÓRMULA DAX:
    VAR MetaLoja = MAX(f_MetaMensalFilial[Ticket Medio])
    VAR Realizado = [tktmedio]
    VAR Percentual = DIVIDE(Realizado - MetaLoja, MetaLoja, 0) * 100
    RETURN
    IF(
        Percentual > 10,
        200,
        IF(
            Percentual >= 0,
            100,
            Percentual * 10
        )
    )

FORMATO: Número decimal
OBSERVAÇÕES:
- Acima de 10% da meta: 200 pontos
- Atingiu a meta (0% a 10%): 100 pontos
- Abaixo da meta: penalização (percentual * 10)
ÚLTIMA MODIFICAÇÃO: 03/01/2026


19. Pontos_Marcas_Proprias
──────────────────────────
DESCRIÇÃO: 1 ponto por cada R$ 100 em vendas de marcas próprias.
FÓRMULA DAX:
    VAR FaturamentoTotal = 
        CALCULATE(
            SUM(f_venda[valortotal]),
            FILTER(
                f_venda,
                f_venda[embalagem] IN SELECTCOLUMNS(d_ProdutosMarcasProprias, "Embalagem", [Embalagem])
                    || f_venda[nome_fabricante] = "VITA PREMIUM"
            )
        )
    VAR Pontos = DIVIDE(FaturamentoTotal, 100, 0)
    RETURN
    ROUND(Pontos, 0)

FORMATO: Número decimal
OBSERVAÇÕES: Inclui produtos da tabela d_ProdutosMarcasProprias e 
fabricante VITA PREMIUM.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: TOTALIZADORES DE PONTOS
───────────────────────────────────────────────────────────────────────────────

20. Pontos_Totais_SuperGerente
──────────────────────────────
DESCRIÇÃO: Soma total dos 8 indicadores principais.
FÓRMULA DAX:
    [Pontos PBM Mês] +
    [Pontos Validade Mês] +
    [PontosInventario_Mes] +
    [PontosFidelidade_Mes] +
    [PontosFaturamento_Mes] +
    [Pontos_Delivery_Mes] +
    [Ponto_CMV_Mes] +
    [Pontos Ticketmedio Mês]

FORMATO: Número decimal
OBSERVAÇÕES: Base para ranking de filiais (Farmácia Destaque).
ÚLTIMA MODIFICAÇÃO: 20/01/2026


21. Pontos_Totais Farmacia destaque
───────────────────────────────────
DESCRIÇÃO: Total de pontos incluindo marcas próprias e Harmo.
FÓRMULA DAX:
    [Pontos PBM Mês] +
    [PontosFidelidade_Mes] +
    [Pontos_Marcas_Proprias]+
    [PontosInventario_Mes] +
    [Pontos Validade Mês] + 
    [PontosHarmo]

FORMATO: Número decimal
OBSERVAÇÕES: Versão com indicadores extras para ranking Farmácia Destaque.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


22. Pontos_Atendente_Final
──────────────────────────
DESCRIÇÃO: Pontos de atendente com dedução de quebras.
FÓRMULA DAX:
    [PontosFaturamento_Geral] - SUM('Top_Atendente_Quebra'[QUEBRA])

FORMATO: Número decimal
OBSERVAÇÕES: Desconta quebras do total de pontos por faturamento.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


23. Pontos_Quebra
─────────────────
DESCRIÇÃO: Pontos negativos por quebras.
FÓRMULA DAX:
    SUM(Top_Atendente[Quebra]) * -1

FORMATO: Número decimal
OBSERVAÇÕES: Multiplica por -1 para transformar em penalização.
ÚLTIMA MODIFICAÇÃO: 14/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: CÁLCULOS BASE DE INDICADORES
───────────────────────────────────────────────────────────────────────────────

24. cmv
───────
DESCRIÇÃO: Calcula o percentual de CMV.
FÓRMULA DAX:
    DIVIDE(
        SUM(f_venda[custo_medio]),
        SUM(f_venda[valortotal])
    )

FORMATO: Percentual
OBSERVAÇÕES: Custo de Mercadoria Vendida dividido pelo valor total.
ÚLTIMA MODIFICAÇÃO: 03/01/2026


25. calculo_fidelidad
─────────────────────
DESCRIÇÃO: Calcula o percentual de fidelidade.
FÓRMULA DAX:
    ABS(
        DIVIDE(
            SUMX(
                FILTER(
                    f_fidelidadeFinal,
                    f_fidelidadeFinal[Status] IN {"Não paasou", "Não Passou"}
                ),
                f_fidelidadeFinal[Valor]
            ),
            SUM(f_fidelidadeFinal[valor])
        )
        - 1
    )

FORMATO: Percentual
OBSERVAÇÕES: Calcula o complemento (1 - %) das vendas que NÃO passaram, 
resultando no % que PASSOU. ABS garante valor positivo.
ÚLTIMA MODIFICAÇÃO: 14/01/2026


26. calculoPBM
──────────────
DESCRIÇÃO: Calcula o percentual de PBM (método antigo).
FÓRMULA DAX:
    ABS(
        SUMX(
            FILTER(
                f_PBM,
                f_PBM[PASSOU_PROGRAMA] = "não passou"
                &&
                NOT CONTAINSSTRING(UPPER(f_PBM[nome_caderno]), "PRÉ")
            ),
            f_PBM[valortotal]
        )
        /
        SUMX(
            FILTER(
                f_PBM,
                NOT CONTAINSSTRING(UPPER(f_PBM[nome_caderno]), "PRÉ")
            ),
            f_PBM[valortotal]
        ) * 100
        - 100
    )
    /100

FORMATO: Percentual
OBSERVAÇÕES: Método usado até 31/12/2025. Exclui cadernos "PRÉ".
ÚLTIMA MODIFICAÇÃO: 03/01/2026


27. PBM_novo
────────────
DESCRIÇÃO: Calcula o percentual de PBM (novo método).
FÓRMULA DAX:
    VAR comPBM = CALCULATE(SUM(f_venda[valortotal]), 
                           f_venda[Passou pbm] = "Passou com PBM")
    VAR valortotal = CALCULATE(SUM(f_venda[valortotal]), 
                               f_venda[Passou pbm] <> BLANK())
    RETURN
    comPBM/valortotal

FORMATO: Percentual
OBSERVAÇÕES: Método usado a partir de 01/01/2026. Mais simples e direto.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


28. PBM
───────
DESCRIÇÃO: Medida unificada que escolhe automaticamente entre método antigo e novo.
FÓRMULA DAX:
    VAR DataCorte = DATE(2026, 1, 1)
    VAR MaxDateSelected = MAX(d_Calendario[date])
    
    RETURN
        IF (
            MaxDateSelected <= DataCorte,
            [calculoPBM],
            [PBM_novo]
        )

FORMATO: Percentual
OBSERVAÇÕES:
- Até 31/12/2025: usa calculoPBM
- A partir de 01/01/2026: usa PBM_novo
ÚLTIMA MODIFICAÇÃO: 14/01/2026


29. tktmedio
────────────
DESCRIÇÃO: Calcula o ticket médio (valor médio por venda).
FÓRMULA DAX:
    SUM(f_venda[valortotal])/DISTINCTCOUNT(f_venda[venda_id])

FORMATO: Moeda brasileira (R$)
OBSERVAÇÕES: Faturamento total dividido pelo número de cupons.
ÚLTIMA MODIFICAÇÃO: 04/01/2026


30. Inventario_Medio
────────────────────
DESCRIÇÃO: Média do inventário realizado.
FÓRMULA DAX:
    AVERAGE(f_MetaMensalFilial[Inventario_realizado])

FORMATO: Percentual
OBSERVAÇÕES: Utilizado para análises de inventário.
ÚLTIMA MODIFICAÇÃO: 04/01/2026


31. delivery
────────────
DESCRIÇÃO: Calcula o valor total de vendas por delivery.
FÓRMULA DAX:
    CALCULATE(SUM(f_venda[valortotal]), f_venda[tipo_registro] = "Entrega" )

FORMATO: Número decimal
OBSERVAÇÕES: Filtra apenas vendas do tipo "Entrega".
ÚLTIMA MODIFICAÇÃO: 20/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: RANKINGS
───────────────────────────────────────────────────────────────────────────────

32. RANK TOP AUXILIAR
─────────────────────
DESCRIÇÃO: Ranking de auxiliares por pontos totais.
FÓRMULA DAX:
    RANKX(ALL(Top_AuxiliarConsolidado[AUXILIAR], Top_AuxiliarConsolidado[Filial]), 
          CALCULATE(SUM(Top_AuxiliarConsolidado[Pontos Totais]), 
                    REMOVEFILTERS(Top_AuxiliarConsolidado[Filial], 
                                  Top_AuxiliarConsolidado[AnoMes])),
          ,DESC, Dense)

FORMATO: Número inteiro
OBSERVAÇÕES: Ranking denso (sem pulos) em ordem decrescente.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


33. Rank por Pontos Top Atendente
──────────────────────────────────
DESCRIÇÃO: Ranking de atendentes por pontos finais.
FÓRMULA DAX:
    RANKX(
        ALL('Top_Atendente'[USUARIO]),
        CALCULATE(
            SUM('Top_Atendente'[Ponto Final]),
            REMOVEFILTERS('Top_Atendente'[Mes])
        ),
        ,
        DESC,
        DENSE
    )

FORMATO: Número inteiro
OBSERVAÇÕES: Remove filtro de mês para ranking geral.
ÚLTIMA MODIFICAÇÃO: 15/12/2025


34. Rank por Pontos top Faturamento
────────────────────────────────────
DESCRIÇÃO: Ranking de vendedores por faturamento total.
FÓRMULA DAX:
    RANKX(
        FILTER(
            ALL('f_venda'[usuario], 'f_venda'[Cargo]),
            'f_venda'[Cargo] IN {"BALCONISTA", "FARMACÊUTICO"} &&
            NOT 'f_venda'[usuario] IN {"admin", "sistema"}
        ),
        CALCULATE(
            SUM('f_venda'[valortotal]), 
            'f_venda'[Cargo] IN {"BALCONISTA", "FARMACÊUTICO"},
            REMOVEFILTERS('f_venda'[filial])
        ),
        ,
        DESC,
        DENSE
    )

FORMATO: Número inteiro
OBSERVAÇÕES: Filtra apenas Balconistas e Farmacêuticos, exclui usuários 
sistema. Remove filtro de filial.
ÚLTIMA MODIFICAÇÃO: 02/01/2026


35. Rank por Pontos top Marcas Próprias
────────────────────────────────────────
DESCRIÇÃO: Ranking de vendedores por faturamento em marcas próprias.
FÓRMULA DAX:
    RANKX(
        FILTER(
            ALL('f_venda'[usuario], f_venda[CARGO], f_venda[filial]),
            NOT 'f_venda'[usuario] IN {"admin", "sistema"} && 
            f_venda[CARGO] IN {"BALCONISTA", "FARMACÊUTICO", "ENCARREGADO EXTERNO"}
        ),
        CALCULATE([Faturamento_MarcasProprias], REMOVEFILTERS(f_venda[Mes])),
        ,
        DESC,
        DENSE
    )

FORMATO: Número inteiro
OBSERVAÇÕES: Inclui também Encarregados Externos. Remove filtro de mês.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


36. Rank por Pontos top Industrias
───────────────────────────────────
DESCRIÇÃO: Ranking de vendedores por vendas de produtos de indústrias parceiras.
FÓRMULA DAX:
    RANKX(
        ALL('Top_Industrias'[usuario]),
        CALCULATE(
            SUM('Top_Industrias'[valortotal]),
            'd_Calendario'[Date] >= DATE(2025, 9, 1),
            REMOVEFILTERS('Top_Industrias'[filial]),
            REMOVEFILTERS('Top_Industrias'[Mes])
        ),
        ,
        DESC, 
        DENSE
    )

FORMATO: Número inteiro
OBSERVAÇÕES: Considera vendas a partir de 01/09/2025.
ÚLTIMA MODIFICAÇÃO: 02/01/2026


37. Rank Vendedores Multiplas Filiais
──────────────────────────────────────
DESCRIÇÃO: Ranking de folguistas (vendedores em múltiplas filiais).
FÓRMULA DAX:
    RANKX(
        ALL('Top Folguista'[usuario]),
        CALCULATE(
            SUM('Top Folguista'[Faturamento Folguista]),
            REMOVEFILTERS(f_venda[filial]) 
        ),
        , 
        DESC, 
        DENSE
    )

FORMATO: Número inteiro
OBSERVAÇÕES: Remove filtro de filial para consolidar vendas em todas as lojas.
ÚLTIMA MODIFICAÇÃO: 04/01/2026


38. Rank por Pontos top Promotor de Vendas
───────────────────────────────────────────
DESCRIÇÃO: Ranking de promotoras por faturamento em categorias específicas.
FÓRMULA DAX:
    RANKX(
        ALL('f_venda'[usuario]),
        CALCULATE(
            SUMX(FILTER(
            'f_venda',
            'f_venda'[Cargo] IN {"Promotora de Vendas"} &&
            NOT 'f_venda'[usuario] IN {"admin", "sistema"} &&
            'f_venda'[categoria] IN {"CONVENIENCIA", "PERFUMARIA", "SUPLEMENTO", "VAREJINHO"} &&
            f_venda[classe] <> "CAIXA 06 - NFE" && f_venda[classe] <> "CAIXA 07 - NFE" && 
            f_venda[classe] <> "CAIXA 08 - NFE" && f_venda[classe] <> "CAIXA 09 - NFE"), 
            SUM(f_venda[valortotal])),
            REMOVEFILTERS(f_venda[filial], f_venda[categoria])
        ),
        ,
        DESC,
        DENSE
    )

FORMATO: Número inteiro
OBSERVAÇÕES: Filtra categorias específicas e exclui caixas NFE.
ÚLTIMA MODIFICAÇÃO: 02/01/2026


39. RANK TOP PARCEIRO DA SEMANA
────────────────────────────────
DESCRIÇÃO: Ranking do parceiro da semana por pontuação.
FÓRMULA DAX:
    RANKX(ALL(Top_Parceiro_Semana[USUARIO], Top_Parceiro_Semana[FILIAL]), 
          CALCULATE(SUM(Top_Parceiro_Semana[PONTUAÇÃO]), 
                    REMOVEFILTERS(Top_Parceiro_Semana[MÊS])),
          ,DESC, Dense)

FORMATO: Número inteiro
OBSERVAÇÕES: Ranking semanal removendo filtro de mês.
ÚLTIMA MODIFICAÇÃO: 15/12/2025


40. Ranking_Filial
──────────────────
DESCRIÇÃO: Ranking de filiais por pontos totais.
FÓRMULA DAX:
    RANKX(
        FILTER(
            ALL(d_Filial[nome real]),
            NOT ISBLANK(d_Filial[nome real])
        ),
        CALCULATE([Ponto_Total_Mes], REMOVEFILTERS(d_Calendario[Date])),
        ,
        DESC,
        Dense
    )

FORMATO: Número inteiro
OBSERVAÇÕES: Exclui filiais em branco. Remove filtro de data.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


41. Ranking_Farmacia destaque
─────────────────────────────
DESCRIÇÃO: Ranking de farmácias destaque.
FÓRMULA DAX:
    RANKX(
        ALL(d_Filial[nome]),
        [Pontos_Totais Farmacia destaque]
        ,
        ,
        DESC,
        Dense
    )

FORMATO: Número inteiro
OBSERVAÇÕES: Usa pontuação com indicadores extras (marcas próprias + Harmo).
ÚLTIMA MODIFICAÇÃO: 20/01/2026


42. Ícone Ranking Top Auxiliar
──────────────────────────────
DESCRIÇÃO: Retorna emoji correspondente à posição no ranking.
FÓRMULA DAX:
    SWITCH( TRUE(), 
            [Rank por Pontos top Faturamento] = 1, "🏆" & [Rank por Pontos top Faturamento], 
            [Rank por Pontos top Faturamento] = 2, "🥈" & [Rank por Pontos top Faturamento], 
            [Rank por Pontos top Faturamento] = 3, "🥉" & [Rank por Pontos top Faturamento], 
            [Rank por Pontos top Faturamento] >= 4, "🏃‍♂️➡️" & [Rank por Pontos top Faturamento], 
            BLANK() )

FORMATO: Texto
OBSERVAÇÕES: 
- 1º lugar: 🏆
- 2º lugar: 🥈  
- 3º lugar: 🥉
- 4º+ lugar: 🏃‍♂️➡️
ÚLTIMA MODIFICAÇÃO: 03/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: FATURAMENTO E VENDAS
───────────────────────────────────────────────────────────────────────────────

43. Faturamento
───────────────
DESCRIÇÃO: Calcula o faturamento total.
FÓRMULA DAX:
    CALCULATE(SUM(f_venda[valortotal]))

FORMATO: Número decimal
OBSERVAÇÕES: Medida base de faturamento.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


44. Faturamento_TopFaturamento
──────────────────────────────
DESCRIÇÃO: Faturamento de Balconistas e Farmacêuticos.
FÓRMULA DAX:
    CALCULATE(
        SUM('f_venda'[valortotal]), 
        'd_FuncionarioCargo'[FUNÇÃO- MELHORES DO ANO] IN {"BALCONISTA", "FARMACÊUTICO"},
        REMOVEFILTERS('f_venda'[filial])
    )

FORMATO: Moeda brasileira (R$)
OBSERVAÇÕES: Remove filtro de filial para totalização geral.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


45. Faturamento_MarcasProprias
──────────────────────────────
DESCRIÇÃO: Faturamento de marcas próprias.
FÓRMULA DAX:
    CALCULATE(SUM('f_venda'[valortotal]),
              FILTER(f_venda,
                     'f_venda'[embalagem] IN VALUES('d_ProdutosMarcasProprias'[Embalagem]) && 
                     f_venda[CARGO] IN {"BALCONISTA", "FARMACÊUTICO", "ENCARREGADO EXTERNO"}))

FORMATO: Número decimal
OBSERVAÇÕES: Filtra produtos da tabela de marcas próprias e cargos específicos.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


46. Faturamento_Vendedores_MultiplasFiliais
───────────────────────────────────────────
DESCRIÇÃO: Faturamento de vendedores que atuam em múltiplas filiais.
FÓRMULA DAX:
    CALCULATE(
        SUM(f_venda[valortotal]),
        TREATAS(
            VALUES('Top Folguista'[usuario]),
            f_venda[usuario]
        )
    )

FORMATO: Número decimal
OBSERVAÇÕES: Usa TREATAS para filtrar vendedores da tabela Top Folguista.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


47. Faturamento_TopIndustria
────────────────────────────
DESCRIÇÃO: Faturamento de produtos de indústrias parceiras.
FÓRMULA DAX:
    CALCULATE(SUM(Top_Industrias[valortotal]))

FORMATO: Moeda brasileira (R$)
OBSERVAÇÕES: Soma valores da tabela Top_Industrias.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


48. PontosFaturamento_Geral
───────────────────────────
DESCRIÇÃO: Converte faturamento em pontos (1 ponto por R$ 100).
FÓRMULA DAX:
    INT( SUM( 'f_venda'[valortotal] ) / 100 )

FORMATO: Número inteiro
OBSERVAÇÕES: Arredonda para baixo (INT).
ÚLTIMA MODIFICAÇÃO: 05/01/2026


49. Media_Vendas
────────────────
DESCRIÇÃO: Média de vendas por dia.
FÓRMULA DAX:
    AVERAGEX(ALLSELECTED(d_Calendario[Dia]),[Faturamento])

FORMATO: Número decimal
OBSERVAÇÕES: Calcula média considerando apenas dias selecionados.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: MEDIDAS DO MÊS ANTERIOR
───────────────────────────────────────────────────────────────────────────────

50. Faturamento_MesAnterior
───────────────────────────
DESCRIÇÃO: Faturamento total do mês anterior.
FÓRMULA DAX:
    CALCULATE(SUM(f_venda[valortotal]), 
              d_Calendario[Mês Nº] = MONTH(TODAY() - 31))

FORMATO: Número decimal
OBSERVAÇÕES: Usa TODAY() - 31 para pegar o mês anterior.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


51. Faturamento_MesAnterior_AcummuladoporDia
────────────────────────────────────────────
DESCRIÇÃO: Faturamento do mês anterior acumulado até o dia equivalente ao atual.
FÓRMULA DAX:
    CALCULATE(SUM(f_venda[valortotal]), 
              DAY(UTCTODAY() - TIME(3,0,0)) >= d_Calendario[Dia] && 
              MONTH(TODAY()-31)  = d_Calendario[Mês Nº])

FORMATO: Número decimal
OBSERVAÇÕES: Permite comparação justa entre mês atual e anterior (mesmo dia).
ÚLTIMA MODIFICAÇÃO: 05/01/2026


52. Faturamento_EsseMes
───────────────────────
DESCRIÇÃO: Faturamento do mês atual.
FÓRMULA DAX:
    CALCULATE(SUM(f_venda[valortotal]), MONTH(TODAY())  = d_Calendario[Mês Nº])

FORMATO: Número decimal
OBSERVAÇÕES: Filtra apenas o mês atual.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


53. MetaFaturamento_MesPassado
──────────────────────────────
DESCRIÇÃO: Meta de faturamento do mês anterior.
FÓRMULA DAX:
    CALCULATE(SUM(f_MetaMensalFilial[Meta Faturamento]),
              MAX(d_Calendario[Mês Nº])-1 = d_Calendario[Mês Nº])

FORMATO: Número decimal
OBSERVAÇÕES: Pega a meta do mês anterior ao máximo selecionado.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


54. MetaTKM
───────────
DESCRIÇÃO: Meta de ticket médio do mês atual.
FÓRMULA DAX:
    CALCULATE(SUM(f_MetaMensalFilial[Ticket Medio]),
              MAX(d_Calendario[Mês Nº]) = d_Calendario[Mês Nº])

FORMATO: Número decimal
OBSERVAÇÕES: Filtra a meta do mês máximo selecionado.
ÚLTIMA MODIFICAÇÃO: 04/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: ANÁLISES E COMPARAÇÕES
───────────────────────────────────────────────────────────────────────────────

55. Faturamento_CumprimentoMeta%
────────────────────────────────
DESCRIÇÃO: Percentual de cumprimento da meta de faturamento do mês anterior.
FÓRMULA DAX:
    DIVIDE ( [Faturamento_MesAnterior], [MetaFaturamento_MesPassado], 0 )

FORMATO: Número decimal
OBSERVAÇÕES: Usado para identificar melhor filial do mês.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


56. MelhorFaturamento_CumprimentoMeta
─────────────────────────────────────
DESCRIÇÃO: Melhor percentual de cumprimento de meta entre filiais.
FÓRMULA DAX:
    MAXX (
        VALUES ( f_venda[filial] ),
        [Faturamento_CumprimentoMeta%]
    )

FORMATO: Percentual
OBSERVAÇÕES: Itera sobre filiais e retorna o maior percentual.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


57. MelhorFaturamento_Filial_MesPassado
────────────────────────────────────────
DESCRIÇÃO: Nome da filial com melhor cumprimento de meta.
FÓRMULA DAX:
    VAR TabelaFiliaisComPct =
        ADDCOLUMNS (
            VALUES ( d_Filial[nome real] ),
            "PctCumprimento", [MelhorFaturamento_CumprimentoMeta]
        )
    VAR Top1 =
        TOPN ( 1, TabelaFiliaisComPct, [PctCumprimento], DESC )
    RETURN
    CONCATENATEX ( Top1, d_Filial[nome real], ", " )

FORMATO: Texto
OBSERVAÇÕES: Cria tabela com percentuais e retorna o nome da TOP 1.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


58. Faturamento_MelhorFilial
────────────────────────────
DESCRIÇÃO: Faturamento da melhor filial do mês atual.
FÓRMULA DAX:
    VAR NomeFilial = [MelhorFaturamento_Filial_MesPassado]
    VAR NomeFilialParaFiltro =
        LOOKUPVALUE(
            d_Filial[nome],
            d_Filial[nome real],
            NomeFilial
        )
    RETURN
        CALCULATE(
            SUM( f_venda[valortotal] ),
            d_Filial[nome] = NomeFilialParaFiltro,
            d_Calendario[Mês Nº] = max(d_Calendario[Mês Nº]))

FORMATO: Número decimal
OBSERVAÇÕES: Usa LOOKUPVALUE para converter nome real em código de filial.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


59. MetaFaturamento_MelhorFilial
─────────────────────────────────
DESCRIÇÃO: Meta de faturamento da melhor filial.
FÓRMULA DAX:
    VAR NomeFilial = [MelhorFaturamento_Filial_MesPassado]
    VAR NomeFilialParaFiltro =
        LOOKUPVALUE(
            d_Filial[nome],
            d_Filial[nome real],
            NomeFilial
        )
    RETURN
        CALCULATE(
            SUM( f_MetaMensalFilial[Meta Faturamento] ),
            d_Filial[nome] = NomeFilialParaFiltro,
            d_Calendario[Mês Nº] = max(d_Calendario[Mês Nº]))

FORMATO: Número decimal
OBSERVAÇÕES: Mesma lógica da medida anterior para pegar a meta.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


60. Tkm Cumprimento Meta %
──────────────────────────
DESCRIÇÃO: Percentual de cumprimento da meta de ticket médio.
FÓRMULA DAX:
    DIVIDE ( [tktmedio], [MetaTKM], 0 )

FORMATO: Número decimal
OBSERVAÇÕES: Realizado dividido pela meta.
ÚLTIMA MODIFICAÇÃO: 04/01/2026


61. Melhor tkm Cumprimento Meta
────────────────────────────────
DESCRIÇÃO: Melhor percentual de TKM entre filiais.
FÓRMULA DAX:
    MAXX (
        VALUES ( f_venda[filial] ),
        [Tkm Cumprimento Meta %]
    )

FORMATO: Percentual
OBSERVAÇÕES: Retorna o maior percentual entre todas as filiais.
ÚLTIMA MODIFICAÇÃO: 04/01/2026


62. Melhor Tkm Filial Mês Passado
──────────────────────────────────
DESCRIÇÃO: Nome da filial com melhor TKM.
FÓRMULA DAX:
    VAR TabelaFiliaisComPct =
        ADDCOLUMNS (
            VALUES ( d_Filial[nome real] ),
            "PctCumprimento", [Melhor tkm Cumprimento Meta]
        )
    VAR Top1 =
        TOPN ( 1, TabelaFiliaisComPct, [PctCumprimento], DESC )
    RETURN
    CONCATENATEX ( Top1, d_Filial[nome real], ", " )

FORMATO: Texto
OBSERVAÇÕES: Similar ao padrão de melhor filial.
ÚLTIMA MODIFICAÇÃO: 04/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: CRESCIMENTO E TENDÊNCIAS
───────────────────────────────────────────────────────────────────────────────

63. CrescimentoAbsoluto
───────────────────────
DESCRIÇÃO: Diferença absoluta entre mês atual e anterior.
FÓRMULA DAX:
    [Faturamento_EsseMes]  - [Faturamento_MesAnterior_AcummuladoporDia]

FORMATO: Número decimal
OBSERVAÇÕES: Valor em R$ do crescimento.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


64. CrescimentoPercentual
─────────────────────────
DESCRIÇÃO: Percentual de crescimento em relação ao mês anterior.
FÓRMULA DAX:
    DIVIDE(
        [CrescimentoAbsoluto],
        [Faturamento_MesAnterior_AcummuladoporDia]
    )

FORMATO: Percentual
OBSERVAÇÕES: Crescimento absoluto dividido pela base.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


65. MaiorCrescimento_VMA
────────────────────────
DESCRIÇÃO: Maior crescimento absoluto entre todos os produtos.
FÓRMULA DAX:
    MAXX(
        ALL(f_venda[embalagem]),
        [CrescimentoAbsoluto]
    )

FORMATO: Número decimal
OBSERVAÇÕES: Itera sobre embalagens para encontrar o maior crescimento.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


66. MaiorCrescimento_VMA%
─────────────────────────
DESCRIÇÃO: Maior crescimento percentual entre produtos.
FÓRMULA DAX:
    MAXX(
        ALL(f_venda[embalagem]),
        DIVIDE([CrescimentoAbsoluto],[Faturamento_MesAnterior_AcummuladoporDia])
    )

FORMATO: Percentual
OBSERVAÇÕES: Versão percentual do maior crescimento.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


67. Produto_MaiorCrescimento
────────────────────────────
DESCRIÇÃO: Nome do produto com maior crescimento.
FÓRMULA DAX:
    VAR MaxGrowth = [MaiorCrescimento_VMA]
    RETURN
    CALCULATE(
        CONCATENATEX(
            FILTER(
                ALL(f_venda[embalagem]),
                [CrescimentoAbsoluto] = MaxGrowth
            ),
            f_venda[embalagem],
            ", "
        ),
        ALL(f_venda[embalagem])
    )

FORMATO: Texto
OBSERVAÇÕES: Filtra produtos com crescimento = máximo e retorna nome(s).
ÚLTIMA MODIFICAÇÃO: 05/01/2026


68. Medida
──────────
DESCRIÇÃO: Crescimento do produto com maior crescimento.
FÓRMULA DAX:
    CALCULATE([CrescimentoAbsoluto],
              FILTER(f_venda, f_venda[embalagem] = [Produto_MaiorCrescimento]))

FORMATO: Número decimal
OBSERVAÇÕES: Medida auxiliar para validação.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: DESTAQUES DO MÊS ANTERIOR
───────────────────────────────────────────────────────────────────────────────

69. Faturamento_Top_Fat_MesPassado
──────────────────────────────────
DESCRIÇÃO: Faturamento individual de vendedor do mês passado.
FÓRMULA DAX:
    CALCULATE(
        SUM('f_venda'[valortotal]), 
        'd_FuncionarioCargo'[FUNÇÃO- MELHORES DO ANO] IN {"BALCONISTA", "FARMACÊUTICO"},
        REMOVEFILTERS('f_venda'[filial]), 
        MONTH(TODAY()-31)  = d_Calendario[Mês Nº]
    )

FORMATO: Número decimal
OBSERVAÇÕES: Filtra mês anterior para ranking de destaques.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


70. MelhorFaturamento_Pessoa_MesPassado
────────────────────────────────────────
DESCRIÇÃO: Nome do vendedor com maior faturamento do mês passado.
FÓRMULA DAX:
    VAR TabelaFiliaisComPct =
        ADDCOLUMNS (
            VALUES ( f_venda[usuario] ),
            "PctCumprimento", [Faturamento_Top_Fat_MesPassado]
        )
    VAR Top1 =
        TOPN ( 1, TabelaFiliaisComPct, [PctCumprimento], DESC )
    RETURN
    CONCATENATEX ( Top1, f_venda[usuario], ", " )

FORMATO: Texto
OBSERVAÇÕES: Destaque mensal de Top Faturamento.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


71. Faturamento_TopIndustriaMesPassado
───────────────────────────────────────
DESCRIÇÃO: Faturamento de indústria do mês passado.
FÓRMULA DAX:
    CALCULATE(
        SUM('Top_Industrias'[valortotal]), 
        'd_FuncionarioCargo'[FUNÇÃO- MELHORES DO ANO] IN {"BALCONISTA", "FARMACÊUTICO"},
        REMOVEFILTERS('Top_Industrias'[filial]), 
        MONTH(TODAY()-31)  = d_Calendario[Mês Nº]
    )

FORMATO: Número decimal
OBSERVAÇÕES: Para destaque Top Indústrias.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


72. MelhorFaturamento_TopIndustria_MesPassado
──────────────────────────────────────────────
DESCRIÇÃO: Nome do vendedor destaque em indústrias do mês passado.
FÓRMULA DAX:
    VAR TabelaFiliaisComPct =
        ADDCOLUMNS (
            VALUES ( Top_Industrias[usuario] ),
            "PctCumprimento", [Faturamento_TopIndustriaMesPassado]
        )
    VAR Top1 =
        TOPN ( 1, TabelaFiliaisComPct, [PctCumprimento], DESC )
    RETURN
    CONCATENATEX ( Top1, Top_Industrias[usuario], ", " )

FORMATO: Texto
OBSERVAÇÕES: Destaque mensal Top Indústrias.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


73. Faturamento_TopFolguista_MesPassado
────────────────────────────────────────
DESCRIÇÃO: Faturamento de folguista do mês passado.
FÓRMULA DAX:
    CALCULATE(
        SUM('f_venda'[valortotal]), 
        'd_FuncionarioCargo'[FUNÇÃO- MELHORES DO ANO] IN {"ENCARREGADO EXTERNO"},
        REMOVEFILTERS('f_venda'[filial]), 
        MONTH(TODAY()-31)  = d_Calendario[Mês Nº]
    )

FORMATO: Número decimal
OBSERVAÇÕES: Filtra apenas Encarregados Externos.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


74. MelhorFaturamento_TopFolguista_MesPassado
──────────────────────────────────────────────
DESCRIÇÃO: Nome do folguista destaque do mês passado.
FÓRMULA DAX:
    VAR TabelaFiliaisComPct =
        ADDCOLUMNS (
            VALUES ( f_venda[usuario] ),
            "PctCumprimento", [Faturamento_TopFolguista_MesPassado]
        )
    VAR Top1 =
        TOPN ( 1, TabelaFiliaisComPct, [PctCumprimento], DESC )
    RETURN
    CONCATENATEX ( Top1, f_venda[usuario], ", " )

FORMATO: Texto
OBSERVAÇÕES: Destaque mensal Top Folguista.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


75. Faturamento_TopPromotor_MesPassado
───────────────────────────────────────
DESCRIÇÃO: Faturamento de promotora do mês passado.
FÓRMULA DAX:
    CALCULATE(
        SUM('Top Promotora de Vendas'[Faturamento]),
        MONTH(TODAY()-31)  = d_Calendario[Mês Nº]
    )

FORMATO: Número decimal
OBSERVAÇÕES: Usa tabela específica Top Promotora de Vendas.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


76. MelhorVenda_TopPromotor_MesPassado
───────────────────────────────────────
DESCRIÇÃO: Nome da promotora destaque do mês passado.
FÓRMULA DAX:
    VAR TabelaFiliaisComPct =
        ADDCOLUMNS (
            VALUES ( 'Top Promotora de Vendas'[usuario] ),
            "PctCumprimento", [Faturamento_TopPromotor_MesPassado]
        )
    VAR Top1 =
        TOPN ( 1, TabelaFiliaisComPct, [PctCumprimento], DESC )
    RETURN
    CONCATENATEX ( Top1,'Top Promotora de Vendas'[usuario], ", " )

FORMATO: Texto
OBSERVAÇÕES: Destaque mensal Top Promotor.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


77. Pontos_TopAtendente_MesPassado
───────────────────────────────────
DESCRIÇÃO: Pontos de atendente do mês passado.
FÓRMULA DAX:
    CALCULATE(
        SUM('Top_Atendente'[Ponto Final]),
        MONTH(TODAY()-31)  = d_Calendario[Mês Nº]
    )

FORMATO: Número decimal
OBSERVAÇÕES: Para destaque Top Atendente.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


78. MelhorPonto_TopAtendente_MesPassado
────────────────────────────────────────
DESCRIÇÃO: Nome do atendente destaque do mês passado.
FÓRMULA DAX:
    VAR TabelaFiliaisComPct =
        ADDCOLUMNS (
            VALUES ( Top_Atendente[usuario] ),
            "PctCumprimento", [Pontos_TopAtendente_MesPassado]
        )
    VAR Top1 =
        TOPN ( 1, TabelaFiliaisComPct, [PctCumprimento], DESC )
    RETURN
    CONCATENATEX ( Top1, Top_Atendente[usuario], ", " )

FORMATO: Texto
OBSERVAÇÕES: Destaque mensal Top Atendente.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


79. Pontos_TopAuxiliar_MesPassado
──────────────────────────────────
DESCRIÇÃO: Pontos de auxiliar do mês passado.
FÓRMULA DAX:
    CALCULATE(
        SUM('Top_Auxiliar'[TOTAL PONTOS]),
        MONTH(TODAY()-31)  = d_Calendario[Mês Nº]
    )

FORMATO: Número decimal
OBSERVAÇÕES: Para destaque Top Auxiliar.
ÚLTIMA MODIFICAÇÃO: 14/01/2026


80. MelhorPonto_TopAuxiliar_MesPassado
───────────────────────────────────────
DESCRIÇÃO: Nome do auxiliar destaque do mês passado.
FÓRMULA DAX:
    VAR TabelaFiliaisComPct =
        ADDCOLUMNS (
            VALUES ( Top_Auxiliar[AUXILIAR] ),
            "PctCumprimento", [Pontos_TopAuxiliar_MesPassado]
        )
    VAR Top1 =
        TOPN ( 1, TabelaFiliaisComPct, [PctCumprimento], DESC )
    RETURN
    CONCATENATEX ( Top1, Top_Auxiliar[AUXILIAR], ", " )

FORMATO: Texto
OBSERVAÇÕES: Destaque mensal Top Auxiliar.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: INSIGHTS E ANÁLISES
───────────────────────────────────────────────────────────────────────────────

81. DiaMaisVendedor
───────────────────
DESCRIÇÃO: Número do dia com maior volume de vendas.
FÓRMULA DAX:
    VAR VendasPorDia = 
        SUMMARIZE(
            'd_calendario',
            'd_calendario'[Dia],
            "Total Vendas", CALCULATE(SUM('f_venda'[valortotal]) )
        )
    VAR DiaComMaisVendasTabela = 
        TOPN(
            1,
            VendasPorDia,
            [Total Vendas], DESC
        )
    RETURN
        MAXX(
            DiaComMaisVendasTabela,
            'd_calendario'[Dia]
        )

FORMATO: Número inteiro
OBSERVAÇÕES: Retorna o dia do mês (1-31).
ÚLTIMA MODIFICAÇÃO: 05/01/2026


82. DiaNome_MaisVendedor
────────────────────────
DESCRIÇÃO: Nome do dia da semana com maior volume de vendas.
FÓRMULA DAX:
    VAR VendasPorDia = 
        SUMMARIZE(
            'd_calendario',
            'd_Calendario'[Dia da Semana],
            "Total Vendas", CALCULATE(SUM('f_Venda'[valortotal])) 
        )
    VAR DiaComMaisVendasTabela = 
        TOPN(
            1,
            VendasPorDia,
            [Total Vendas], DESC
        )
    RETURN
        MAXX(
            DiaComMaisVendasTabela,
            'd_Calendario'[Dia da Semana]
        )

FORMATO: Texto
OBSERVAÇÕES: Retorna nome do dia (Segunda, Terça, etc).
ÚLTIMA MODIFICAÇÃO: 05/01/2026


83. DiaMaisVendedor_Folguista
─────────────────────────────
DESCRIÇÃO: Dia com maior venda de Encarregados Externos.
FÓRMULA DAX:
    VAR VendasPorDia = 
        SUMMARIZE(
            'd_calendario',
            'd_calendario'[Dia],
            "Total Vendas", CALCULATE(SUM('f_venda'[valortotal]), 
                                      d_FuncionarioCargo[FUNÇÃO- MELHORES DO ANO] = "Encarregado Externo") 
        )
    VAR DiaComMaisVendasTabela = 
        TOPN(
            1,
            VendasPorDia,
            [Total Vendas], DESC
        )
    RETURN
        MAXX(
            DiaComMaisVendasTabela,
            'd_calendario'[Dia]
        )

FORMATO: Número inteiro
OBSERVAÇÕES: Específico para folguistas.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


84. Dia Nome Mais Vendedor Folguista
─────────────────────────────────────
DESCRIÇÃO: Dia da semana com maior venda de Encarregados Externos.
FÓRMULA DAX:
    VAR VendasPorDia = 
        SUMMARIZE(
            'd_calendario',
            'd_Calendario'[Dia da Semana],
            "Total Vendas", CALCULATE(SUM('f_Venda'[valortotal]), 
                                      d_FuncionarioCargo[FUNÇÃO- MELHORES DO ANO] = "Encarregado Externo") 
        )
    VAR DiaComMaisVendasTabela = 
        TOPN(
            1,
            VendasPorDia,
            [Total Vendas], DESC
        )
    RETURN
        MAXX(
            DiaComMaisVendasTabela,
            'd_Calendario'[Dia da Semana]
        )

FORMATO: Texto
OBSERVAÇÕES: Nome do dia para folguistas.
ÚLTIMA MODIFICAÇÃO: 03/01/2026


85. mes
───────
DESCRIÇÃO: Retorna o número do mês máximo no contexto.
FÓRMULA DAX:
    MAX(d_Calendario[Mês Nº])

FORMATO: Número inteiro
OBSERVAÇÕES: Medida auxiliar para filtros de mês.
ÚLTIMA MODIFICAÇÃO: 04/01/2026


86. UltimaAtualizacaoTe
───────────────────────
DESCRIÇÃO: Data e hora da última atualização do modelo.
FÓRMULA DAX:
    FORMAT(MAX(UltimaAtualizacao[UltimaAtualizacao]), "dd/MM/yyyy HH:mm" )

FORMATO: Texto
OBSERVAÇÕES: Importante para controle de atualização do relatório.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


87. CorFarmaciaDestaque_Pontostotais
────────────────────────────────────
DESCRIÇÃO: Retorna 1 se tem pontos, 0 se não tem (formatação condicional).
FÓRMULA DAX:
    IF([Pontos_Totais Farmacia destaque] > 0, 1,0)

FORMATO: Número inteiro
OBSERVAÇÕES: Usado para coloração em visuais.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: VISUALIZAÇÃO E FORMATAÇÃO
───────────────────────────────────────────────────────────────────────────────

88. MaxY_TopVnds
────────────────
DESCRIÇÃO: Define eixo Y máximo para gráfico Top Vendedores.
FÓRMULA DAX:
    MAXX(ALLSELECTED(d_Calendario[Dia]), [Faturamento] ) * 1.5

FORMATO: Número decimal
OBSERVAÇÕES: 150% do máximo para dar espaço no gráfico.
ÚLTIMA MODIFICAÇÃO: 03/01/2026


89. MaxY_TopVndsExclu
─────────────────────
DESCRIÇÃO: Define eixo Y máximo para gráfico Marcas Próprias.
FÓRMULA DAX:
    MAXX(ALLSELECTED(d_Calendario[Semana do Ano]), [Faturamento_MarcasProprias] ) * 1.5

FORMATO: Número decimal
OBSERVAÇÕES: Por semana ao invés de dia.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


90. MaxY_TopIndus
─────────────────
DESCRIÇÃO: Define eixo Y máximo para gráfico Top Indústrias.
FÓRMULA DAX:
    MAXX(ALLSELECTED(d_Calendario[Dia]),[Faturamento_TopIndustria] ) * 1.5

FORMATO: Número decimal
OBSERVAÇÕES: 150% do máximo para espaçamento.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


91. LinhaFaturamento_TopFaturamento
───────────────────────────────────
DESCRIÇÃO: Linha de referência em 10% do faturamento.
FÓRMULA DAX:
    [Faturamento] * 0.1

FORMATO: Número decimal
OBSERVAÇÕES: Linha auxiliar no gráfico.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


92. LinhaFaturamento_MarcasProprias
───────────────────────────────────
DESCRIÇÃO: Linha de referência em 10% do faturamento de marcas próprias.
FÓRMULA DAX:
    [Faturamento_MarcasProprias] * 0.1

FORMATO: Número decimal
OBSERVAÇÕES: Linha auxiliar específica para marcas próprias.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


93. LinhaFaturamento_TopIndustria
──────────────────────────────────
DESCRIÇÃO: Linha de referência em 10% do faturamento de indústrias.
FÓRMULA DAX:
    sum(Top_Industrias[valortotal]) * 0.1

FORMATO: Número decimal
OBSERVAÇÕES: Linha auxiliar para Top Indústrias.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: TÍTULOS DINÂMICOS
───────────────────────────────────────────────────────────────────────────────

94. TituloVndExclu
──────────────────
DESCRIÇÃO: Título dinâmico para gráfico de marcas próprias.
FÓRMULA DAX:
    CONCATENATE("Vendas por Semana ", SELECTEDVALUE(d_ProdutosMarcasProprias[Categoria]))

FORMATO: Texto
OBSERVAÇÕES: Concatena com a categoria selecionada.
ÚLTIMA MODIFICAÇÃO: 03/01/2026


95. TituloTopIndustrias2
────────────────────────
DESCRIÇÃO: Título dinâmico para gráfico diário de indústrias.
FÓRMULA DAX:
    CONCATENATE("Vendas por Dia do Parceiro ", SELECTEDVALUE(Top_Industrias[Fabricante]))

FORMATO: Texto (com erro semântico)
OBSERVAÇÕES: **ERRO**: Coluna 'Fabricante' não existe na tabela Top_Industrias.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


96. TituloTopIndustrias
───────────────────────
DESCRIÇÃO: Título dinâmico para gráfico por filial de indústrias.
FÓRMULA DAX:
    CONCATENATE("Vendas por Filial do Parceiro ", SELECTEDVALUE(Top_Industrias[Fabricante]))

FORMATO: Texto (com erro semântico)
OBSERVAÇÕES: **ERRO**: Coluna 'Fabricante' não existe na tabela Top_Industrias.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


97. Titulo_DestaqueMes
──────────────────────
DESCRIÇÃO: Título com o nome do mês anterior.
FÓRMULA DAX:
    "Destaques do Mês de " &
    FORMAT(MAX(d_Calendario[Date]) - 31, "MMMM")

FORMATO: Texto
OBSERVAÇÕES: Subtrai 31 dias para pegar o mês anterior.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: PROGRAMA HARMO
───────────────────────────────────────────────────────────────────────────────

98. PontosHarmo
───────────────
DESCRIÇÃO: Pontos do programa Harmo.
FÓRMULA DAX:
    var  soma = SUM('Top_Farmacia_Destaque'[Harmo])
    RETURN
    SUMX(VALUES(d_Filial[nome]), soma)

FORMATO: Número inteiro
OBSERVAÇÕES: Itera sobre filiais para somar pontos Harmo.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


99. PontosHarmo_Mes
───────────────────
DESCRIÇÃO: Pontos Harmo consolidados por mês.
FÓRMULA DAX:
    SUMX(VALUES(d_Calendario[Date].[Mês]), SUM(Top_Farmacia_Destaque[Harmo]))

FORMATO: Número inteiro
OBSERVAÇÕES: Consolida por mês.
ÚLTIMA MODIFICAÇÃO: 15/01/2026


───────────────────────────────────────────────────────────────────────────────
CATEGORIA: MEDIDAS AUXILIARES E ESPECIAIS
───────────────────────────────────────────────────────────────────────────────

100. Pontos_Delivery_obsoleto
─────────────────────────────
DESCRIÇÃO: Versão antiga da medida de pontos delivery (COM ERRO).
FÓRMULA DAX:
    VAR MetaLoja = SUM(f_MetaMensalFilial[Meta Delivery])
    VAR Realizado = SUM(f_Entrega[valor_total])
    VAR Percentual = DIVIDE(Realizado, MetaLoja, 0) * 100
    RETURN
        IF(
            Percentual >= 70,
            MIN(Percentual, 120),
            0
        )

FORMATO: Desconhecido
OBSERVAÇÕES: **ERRO SEMÂNTICO**: Tabela 'f_Entrega' não existe. 
Esta medida não está em uso.
ÚLTIMA MODIFICAÇÃO: 20/01/2026


101. Medida Autoplay
────────────────────
DESCRIÇÃO: HTML para embed de vídeo com autoplay.
FÓRMULA DAX:
    "<video width=""1020"" height=""1080"" controls autoplay muted loop> <source src=""" & 
    [MedidaURL] & 
    """ type=""video/mp4""></video>"

FORMATO: Texto (HTML)
OBSERVAÇÕES: Cria tag HTML para vídeo com autoplay.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


102. MedidaURL
──────────────
DESCRIÇÃO: URL do vídeo de fundo para celebrações.
FÓRMULA DAX:
    "https://github.com/superpopularbi-pixel/Videos_Artes/raw/refs/heads/main/Create%20a%20cinematic%20video%20scene%20with%20golden%20stars%20gently%20falling%20in%20the%20background,%20shimmering%20as%20they%20descend.%20The%20main%20subject%20in%20the%20foreground%20should%20remain%20bright%20and%20radiant,%20with%20a%20glowing%20highlight%20effect%20th.mp4"

FORMATO: Texto (URL)
OBSERVAÇÕES: Link para vídeo de estrelas douradas caindo.
ÚLTIMA MODIFICAÇÃO: 05/01/2026


103. PBMnovo (da tabela Top Folguista)
───────────────────────────────────────
DESCRIÇÃO: Cálculo de PBM novo (duplicada na tabela Top Folguista).
FÓRMULA DAX:
    VAR comPBM = CALCULATE(SUM(f_venda[valortotal]), 
                           f_venda[Passou pbm] = "Passou com PBM")
    VAR valortotal = CALCULATE(SUM(f_venda[valortotal]), 
                               f_venda[Passou pbm] <> BLANK())
    RETURN
    comPBM/valortotal * 100

FORMATO: Número decimal
OBSERVAÇÕES: Medida duplicada na tabela Top Folguista (deveria estar em _Medida).
ÚLTIMA MODIFICAÇÃO: 20/01/2026


═══════════════════════════════════════════════════════════════════════════════
3. RESUMO DE MEDIDAS POR CATEGORIA
═══════════════════════════════════════════════════════════════════════════════

┌────────────────────────────────┬──────────────────────────────────────────┐
│ CATEGORIA                      │ QUANTIDADE DE MEDIDAS                    │
├────────────────────────────────┼──────────────────────────────────────────┤
│ Sistema de Pontuação (Mensal)  │ 10 medidas                              │
│ Cálculo de Pontos              │ 9 medidas                               │
│ Totalizadores de Pontos        │ 4 medidas                               │
│ Cálculos Base de Indicadores   │ 8 medidas                               │
│ Rankings                       │ 11 medidas                              │
│ Faturamento e Vendas           │ 7 medidas                               │
│ Medidas Mês Anterior           │ 5 medidas                               │
│ Análises e Comparações         │ 15 medidas                              │
│ Crescimento e Tendências       │ 6 medidas                               │
│ Destaques Mês Anterior         │ 12 medidas                              │
│ Insights e Análises            │ 7 medidas                               │
│ Visualização e Formatação      │ 6 medidas                               │
│ Títulos Dinâmicos              │ 4 medidas                               │
│ Programa Harmo                 │ 2 medidas                               │
│ Medidas Auxiliares/Especiais   │ 3 medidas                               │
├────────────────────────────────┼──────────────────────────────────────────┤
│ **TOTAL**                      │ **103 MEDIDAS**                         │
└────────────────────────────────┴──────────────────────────────────────────┘


═══════════════════════════════════════════════════════════════════════════════
4. REGRAS DE PONTUAÇÃO DETALHADAS
═══════════════════════════════════════════════════════════════════════════════

SISTEMA DE PONTUAÇÃO FARMÁCIA DESTAQUE:
---------------------------------------

1. **FATURAMENTO** (70-120 pontos)
   - < 70% da meta: 0 pontos
   - 70% da meta: 70 pontos
   - 100% da meta: 100 pontos
   - 120% da meta: 120 pontos (teto)
   - Linear entre 70% e 120%

2. **DELIVERY** (70-120 pontos ou Média)
   - Filiais SEM delivery: recebem média geral (não penalizadas)
   - Filiais COM delivery:
     - < 70% da meta: 0 pontos
     - 70% da meta: 70 pontos
     - 100% da meta: 100 pontos
     - 120% da meta: 120 pontos (teto)

3. **PBM** (até 100 pontos, penalização abaixo de 80%)
   - ≥ 80%: pontos = percentual alcançado
   - < 80%: penalização = (percentual - 80) × 10
   - Exemplo: 75% = (75-80)×10 = -50 pontos

4. **FIDELIDADE** (75-100 pontos, penalização abaixo de 75%)
   - 75% a 100%: pontos = percentual (máx 100)
   - < 75%: penalização = (percentual - 75) × 10
   - Exemplo: 70% = (70-75)×10 = -50 pontos

5. **INVENTÁRIO** (0-100 pontos, por faixas)
   - 0,00% a 0,20%: 100 pontos (excelente)
   - 0,20% a 0,29%: 70 pontos (bom)
   - 0,30% a 0,40%: 30 pontos (regular)
   - > 0,40%: penalização progressiva

6. **VALIDADE** (0-100 pontos, por faixas)
   - 0,00% a 0,10%: 100 pontos (excelente)
   - 0,10% a 0,19%: 70 pontos (bom)
   - 0,20% a 0,25%: 30 pontos (regular)
   - > 0,25%: penalização progressiva

7. **CMV** (0, 50 ou 100 pontos)
   - ≤ 97% da meta: 100 pontos (excelente)
   - 97% a 100% da meta: 50 pontos (ok)
   - > 100% da meta: 0 pontos (acima do esperado)

8. **TICKET MÉDIO** (-∞ a 200 pontos)
   - > 10% acima da meta: 200 pontos (bônus)
   - 0% a 10% acima: 100 pontos
   - Abaixo da meta: (percentual - 0) × 10 (penalização)
   - Exemplo: -5% = -5×10 = -50 pontos

**PONTOS EXTRAS:**

9. **MARCAS PRÓPRIAS** (1 ponto por R$ 100)
   - Faturamento em marcas próprias ÷ 100
   - Sem limite máximo
   - Produtos: tabela d_ProdutosMarcasProprias + VITA PREMIUM

10. **HARMO**
    - Pontos por participação no programa Harmo
    - Valores definidos na tabela Top_Farmacia_Destaque


═══════════════════════════════════════════════════════════════════════════════
5. NOTAS TÉCNICAS IMPORTANTES
═══════════════════════════════════════════════════════════════════════════════

TRANSIÇÃO DE METODOLOGIA PBM:
-----------------------------
Similar ao modelo DASH - LOJAS v3, este relatório implementa transição 
entre duas metodologias:

• **Metodologia Antiga** (até 31/12/2025):
  - Baseada na tabela f_PBM
  - Campo: PASSOU_PROGRAMA
  - Exclui cadernos "PRÉ"
  - Medida: [calculoPBM]

• **Metodologia Nova** (a partir de 01/01/2026):
  - Baseada na coluna calculada em f_venda
  - Campo: Passou pbm
  - Filtra "Passou com PBM"
  - Medida: [PBM_novo]

• **Medida Unificada**: [PBM]
  - Escolhe automaticamente baseado na data


MEDIDAS COM ERROS IDENTIFICADOS:
--------------------------------
1. **Pontos_Delivery_obsoleto**
   - ERRO: Tabela 'f_Entrega' não existe
   - STATUS: Obsoleta, não utilizada

2. **TituloTopIndustrias2** e **TituloTopIndustrias**
   - ERRO: Coluna 'Fabricante' não existe em Top_Industrias
   - IMPACTO: Títulos dinâmicos não funcionam
   - CORREÇÃO SUGERIDA: Verificar nome correto da coluna


CONVENÇÕES DE NOMENCLATURA:
---------------------------
• Prefixos:
  - f_ = Tabela Fato
  - d_ = Tabela Dimensão
  - Top_ = Tabelas de Rankings

• Sufixos de medidas:
  - "_Mes" = Consolidação mensal
  - "_MesPassado" = Dados do mês anterior
  - "Pontos_" = Sistema de pontuação
  - "Rank" = Rankings
  - "Melhor" = Identificação de destaques


PERFORMANCE E OTIMIZAÇÃO:
------------------------
• Medidas de ranking usam RANKX com DENSE para evitar pulos
• REMOVEFILTERS usado extensivamente para controlar contexto
• TREATAS usado para relacionamentos virtuais
• SUMMARIZE usado para agregações temporárias
• TOPN usado para identificar destaques


SEGURANÇA E FILTROS:
-------------------
• Usuários "admin" e "sistema" são excluídos de rankings
• Cargos específicos são filtrados por categoria
• Categorias específicas para Promotoras de Vendas
• Exclusão de caixas NFE em certos cálculos


═══════════════════════════════════════════════════════════════════════════════
6. RELACIONAMENTOS E DEPENDÊNCIAS
═══════════════════════════════════════════════════════════════════════════════

PRINCIPAIS RELACIONAMENTOS:
--------------------------
• d_Calendario → todas as tabelas fato
• d_Filial → f_venda, f_MetaMensalFilial
• d_FuncionarioCargo → f_venda
• d_ProdutosMarcasProprias → f_venda (via embalagem)

DEPENDÊNCIAS ENTRE MEDIDAS:
---------------------------
Medidas base que alimentam outras:
1. [Faturamento] → base para várias medidas
2. [cmv] → usado em [Pontos_CMV]
3. [tktmedio] → usado em [Pontos_TicketMedio]
4. [calculo_fidelidad] → usado em [PontosFidelidade]
5. [PBM] → usado em [Pontos_PBM]

Medidas de consolidação:
1. Pontos individuais → Pontos mensais → Pontos totais
2. Faturamentos → Rankings → Destaques

Medidas de comparação:
1. Mês atual vs anterior → Crescimento → Produto destaque


═══════════════════════════════════════════════════════════════════════════════
7. RECOMENDAÇÕES DE USO
═══════════════════════════════════════════════════════════════════════════════

ACOMPANHAMENTO DE RANKINGS:
--------------------------
1. Farmácia Destaque: usar [Ranking_Farmacia destaque]
2. Top Faturamento: usar [Rank por Pontos top Faturamento]
3. Top Atendente: usar [Rank por Pontos Top Atendente]
4. Top Auxiliar: usar [RANK TOP AUXILIAR]

ANÁLISE DE PERFORMANCE:
----------------------
1. Sempre comparar pontos com metas estabelecidas
2. Acompanhar evolução mensal com medidas "_Mes"
3. Identificar destaques com medidas "_MesPassado"
4. Analisar crescimento com medidas de tendência

VALIDAÇÃO DE DADOS:
------------------
1. Verificar [UltimaAtualizacaoTe] para confirmar atualização
2. Conferir se medidas de erro estão sendo usadas
3. Validar se filtros de usuário estão corretos
4. Checar se transição PBM está funcionando corretamente

CORREÇÕES SUGERIDAS:
-------------------
1. Corrigir coluna 'Fabricante' em Top_Industrias
2. Remover ou corrigir [Pontos_Delivery_obsoleto]
3. Consolidar medida [PBMnovo] (está duplicada)
4. Padronizar nomes de medidas (algumas sem pasta)


═══════════════════════════════════════════════════════════════════════════════
8. GLOSSÁRIO DE TERMOS
═══════════════════════════════════════════════════════════════════════════════

**CMV**: Custo de Mercadoria Vendida
**PBM**: Programa de Benefício de Medicamentos
**TKM**: Ticket Médio
**Harmo**: Programa específico de bonificação
**Folguista**: Encarregado Externo que atua em múltiplas filiais
**VMA**: Variação Mensal Acumulada
**AnoMês**: Formato Ano-Mês para agrupamento temporal
**DENSE**: Tipo de ranking sem pulos (1,2,3 ao invés de 1,2,4)


═══════════════════════════════════════════════════════════════════════════════
FIM DA DOCUMENTAÇÃO
═══════════════════════════════════════════════════════════════════════════════

Documento gerado automaticamente em: 30/01/2026
Modelo: MELHORES DO ANO 2026 INTERNO
Total de Medidas Documentadas: 103
Cultura do Modelo: pt-BR
Modo de Armazenamento: Import

Para dúvidas ou sugestões sobre este documento, entre em contato com a equipe
de Business Intelligence.