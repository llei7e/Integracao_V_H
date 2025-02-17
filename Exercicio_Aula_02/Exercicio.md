**Colaboradores** - *Lucas Leite, Ricardo Silva, Kauan Izidoro, Gabriel Alvim, Gustavo Monteiro e Gustavo Sousa*.

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



<br>

## Benefícios e Desafios no Contexto de Industria 4.0

### **Benefícios**


**1. Maior Eficiência Operacional**

- A integração entre sistemas *ERP*, *MES*, *SCADA* e *CLPs* permite um fluxo contínuo de dados, otimizando decisões e reduzindo desperdícios
- Automatização do sequenciamento de ordens de produção evitando gargalos e melhorando a produtividade.


**2. Melhoria na Rastreabilidade e Qualidade**

- Sensores e CLPs fornecem dados em tempo real sobre condições operacionais, facilitando a rastreabilidade de produtos
- Registros detalhados que ajudam a identificar falhas e aprimorar o controle de qualidade.

**3. Otimização de Recursos e Redução de Custos**

- Monitoramento de consumo de materiais e comparação de custos planejados x realizados na gestão financeira e mitigando desperdícios.
- Ajustes em tempo real garantem um melhor aproveitamento da capacidade produtiva.

**4. Monitoramento Remoto e Supervisão em Tempo Real**

- O uso de SCADA permite visualizar o status das máquinas e processos remotamente, facilitando a manutenção preditiva e evitando paradas inesperadas.

**5. Automação Inteligente e Resposta Rápida a Falhas**

- O sistema possibilita detectar falhas automaticamente e aciona alarmes no SCADA, permitindo respostas mais rápidas e reduzindo impactos na produção.

<br>

### **Desafios**

**1. Complexidade na Integração dos Sistemas**

- Sistemas legados podem ter dificuldades em se comunicar com novas tecnologias, exigindo personalização e investimentos em *middleware*.

**2. Segurança Cibernética**

- A interconexão de sistemas aumenta a superfície de ataque, exigindo medidas robustas de segurança para evitar invasões e ou sabotagens.

**3. Alto Custo Inicial de Implementação**

- A aquisição e integração de sensores, *CLPs*, *MES* e *SCADA* podem representar um custo elevado, demandando um planejamento financeiro sólido.

**4. Dependência de Infraestrutura Tecnológica**

- A necessidade de conectividade estável e armazenamento de dados eficiente pode exigir melhorias na infraestrutura de TI da empresa.

**5. Treinamento e Adoção pela Equipe**

- A transição para um modelo digital exige treinamento e capacitação dos operadores e gestores para garantir que os benefícios da automação sejam totalmente aproveitados.



<br>

## Conclusão

A Indústria 4.0 traz avanços significativos na automação e digitalização dos processos produtivos, proporcionando maior eficiência, qualidade e controle operacional. No entanto, sua implementação requer planejamento estratégico para superar desafios como integração de sistemas, segurança, custos e adaptação da equipe.

Para um sucesso sustentável, as empresas devem investir em tecnologias abertas, infraestrutura robusta e capacitação contínua, garantindo que os benefícios da automação sejam plenamente aproveitados.