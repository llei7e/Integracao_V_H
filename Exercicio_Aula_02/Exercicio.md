# Levantamento de Módulos e Integrações

Uma indústria de fabricação possui uma linha de produção automatizada que inclui esteiras transportadoras, robôs para montagem, CLPs (Controladores Lógicos Programáveis), além de sensores e atuadores para controle de processos. O objetivo é garantir a eficiência, rastreabilidade e integração entre os diferentes sistemas utilizados na empresa.


## Diagrama de integração entre módulos e sistemas
O diagrama centraliza o ERP e acima temos o processo de informações dos `Sensores ao ERP`, e abaixo do `ERP aos Atuadores`

```mermaid
---
config:
  theme: neo-dark
  flowchart:
    curve: linear
---
flowchart TD
    A1 --> |Reservas de estoque para produção| B
    A2 --> |Materiais disponíveis e necessidade de aquisição| B
    A3 --> |Detalhes das ordens emitidas pelo PCP| B
    A4 --> |Comparação de custos Planejados x Realizados| B
    A5 --> |Demanda de Pedidos| B
    A6 --> |Dados de Inspeção| B

    subgraph ERP_to_Sensors["ERP aos Atuadores"]
        B["MES - Recebimento de dados<br><br>*Execução e Monitoramento da Produção*"]

        B --> |Envia setpoints e parâmetros de produção| C[SCADA - Recebimento de dados]
        B --> |Repassa ordens de produção e sequenciamento| C

        C --> |Supervisão em tempo real| D[CLP]
        C --> |Controle em tempo real| D

        D --> |Controle em tempo real| E[Atuadores]
    end
    subgraph ERP["ERP"]
        A1["**Compras** <br><br> *Gestão de Pedidos e Estoque*"]
        A2["**MRP1** <br><br> *Aquisições com base em vendas e estoque*"]
        A3["**PCP** <br><br> *Emissão de Ordens de Produção*"]
        A4["**Custos** <br><br> *Precificação*"]
        A5["**Faturamento** <br><br> *Processamento de vendas e emissão de boletos*"]
        A6["**Controle de Qualidade** <br><br> *Inspeção de qualidade*"]
    end

    B1 --> |Atualizar o estoque no ERP| A1
    B1 --> |Ajustar futuras compras e previsões do MRP1| A2
    B1 --> |Atualização do andamento de cada ordem| A3
    B1 --> |Consumo real de recursos| A4
    B1 --> |Registros de defeitos e refugos| A6
    B1 --> |Relatórios e rastreabilidade| A5

    subgraph Sensors_to_ERP["Sensores ao ERP"]
        B1["MES - Envio de dados<br><br>*Execução e Monitoramento da Produção*"]

        C1[SCADA] --> |Envia dados de produção| B1
        C1 --> |Geração de eventos e alarmes para análise no MES| B1
        C1 --> |Envia dados para rastreabilidade e qualidade| B1

        D1[CLP] --> |Envia dados dos sensores e estados das máquinas| C1
        D1 --> |Envia sinais de alarmes caso ocorram falhas ou valores críticos| C1

        E1[Sensores] --> |Envia sinais dos sensores| D1
    end


```


## Benefícios e desafios no contexto de Industria 4.0