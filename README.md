# NiverNote - Sistema de Lembretes de Aniversários para MS-DOS

## Descrição do Projeto

O NiverNote foi desenvolvido para resolver um problema comum dos anos 1980: o esquecimento de datas de aniversário importantes. Antes da era dos smartphones e calendários digitais avançados, as pessoas dependiam de calendários físicos e anotações em papel, o que frequentemente resultava em esquecimentos.

Este programa para MS-DOS oferece uma solução simples e eficiente, exibindo automaticamente lembretes na tela quando é o aniversário de alguém cadastrado no sistema.

## Requisitos Funcionais

### Cadastro de Aniversários
- Permite inserção do nome do aniversariante, dia e mês do aniversário
- Armazena os dados localmente no computador do usuário
- Exibe mensagem de confirmação "Aniversário salvo" após cadastro

### Consulta e Notificações
- Verifica automaticamente aniversários do dia durante a inicialização
- Exibe lembretes visualmente destacados na tela
- Oferece interface simples para cadastro e consulta
- Mostra aniversários de hoje e do dia seguinte quando solicitado
- Exibe contagem regressiva (dias/meses restantes) para próximos aniversários

## Requisitos Não-Funcionais

### Interface
- Design simples e intuitivo
- Fluxo máximo de 2 etapas para cadastro (nome + data)

### Desempenho
- Tempo de carregamento inferior a 5 segundos após inicialização
- Consumo mínimo de recursos do sistema (CPU e memória)
- Taxa de sucesso de 99,9% na exibição de lembretes

## Funcionalidades Detalhadas

1. **Cadastro Simplificado**
   - Tela única com campos para:
     - Nome do aniversariante (até 30 caracteres)
     - Dia do aniversário (1-31)
     - Mês do aniversário (1-12)
   - Validação automática de datas inválidas

2. **Sistema de Notificações**
   - Exibição automática ao iniciar o computador
   - Destaque visual usando cores e bordas
   - Lista completa de aniversários do dia

3. **Ferramentas de Consulta**
   - Visualização de todos aniversários cadastrados
   - Filtro por data específica
   - Ordenação por nome ou por data
   - Cálculo de dias restantes para próximos aniversários

## Especificações Técnicas

- **Plataforma**: MS-DOS (versão 3.0 ou superior)
- **Armazenamento**: Arquivo ANIVERS.DAT no diretório do programa
- **Requisitos de Sistema**:
  - 512KB de RAM
  - Qualquer placa de vídeo compatível com MS-DOS
  - Disco rígido ou disquete para armazenamento

## Fluxo de Operação

1. Durante a inicialização:
   - Programa carrega automaticamente via AUTOEXEC.BAT
   - Verifica a data atual no sistema
   - Compara com o banco de dados de aniversários
   - Exibe notificação se houver correspondência

2. Modo interativo:
   - Menu principal com opções:
     [1] Cadastrar novo aniversário
     [2] Ver aniversários de hoje
     [3] Listar todos aniversários
     [4] Sair

## Considerações de Design

- Interface totalmente baseada em texto
- Navegação via teclado (setas e Enter)
- Cores utilizadas apenas para destacar informações importantes
- Mensagens de erro claras e objetivas

## Limitações Conhecidas

- Não suporta registro do ano de nascimento
- Limite de 255 entradas no banco de dados
- Formato fixo de data (DD/MM)
