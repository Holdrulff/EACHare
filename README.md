### 📌 Visão Macro do Projeto

O projeto **EACHare** é um sistema de compartilhamento de arquivos **peer-to-peer (P2P)** simplificado. Cada **peer** é um servidor TCP que pode compartilhar arquivos e manter uma lista de peers conhecidos. Ele pode solicitar arquivos de outros peers e adicionar novos peers à sua rede.

Nesta **Parte 1** do projeto, o foco é o **gerenciamento de peers conhecidos**, incluindo:

- Identificação dos peers (IP e porta).
- Comunicação via mensagens TCP padronizadas.
- Atualização do estado dos peers (ONLINE/OFFLINE).
- Sincronização de peers conhecidos através do protocolo GET_PEERS.
- Implementação de um relógio lógico local.

### 📌 Levantamento de Requisitos Funcionais

#### 📍 **Requisitos Principais**

1. **Gerenciamento de Peers**:

   - Cada peer deve armazenar uma lista de peers conhecidos.
   - Deve haver um mecanismo para atualizar a lista dinamicamente.

2. **Comunicação via Sockets TCP**:

   - Cada peer deve rodar como um servidor TCP.
   - O protocolo deve seguir um formato específico de mensagens.

3. **Operações e Comandos**:

   - **Listar peers**: Mostrar peers conhecidos e seu status.
   - **Obter peers**: Solicitar lista de peers conhecidos de outro peer.
   - **Listar arquivos locais**: Mostrar arquivos compartilhados no diretório.
   - **Sair**: Enviar mensagem de saída (BYE) e encerrar a execução.

4. **Relógio Lógico**:
   - O relógio inicia em **zero**.
   - Deve ser **incrementado** antes de enviar ou ao receber uma mensagem.
   - As atualizações do relógio devem ser exibidas na saída padrão.

#### 📍 **Requisitos Não Funcionais**

- O código deve ser escrito em **Python**.
- Comunicação via **sockets TCP**.
- Ser testado em ambiente **Linux (Ubuntu 22.04)**.
- Manter logs detalhados das mensagens trocadas.

---

### 📌 System Design do Projeto

#### 🔹 **Arquitetura**

- **Modelo Cliente-Servidor** sobre TCP (cada peer age como ambos).
- **Protocolo de Comunicação** baseado em mensagens de texto puro.
- **Relógio Lógico** simples para rastrear eventos.

#### 🔹 **Fluxo de Operações**

1. O peer inicia, lê os parâmetros (endereço, lista de peers e diretório de arquivos).
2. Cria um **servidor TCP** para ouvir conexões.
3. Ao se conectar, pode **listar peers, obter peers e listar arquivos**.
4. Pode se desconectar informando os outros peers via mensagem **BYE**.

#### 🔹 **Componentes do Sistema**

- **Gerenciador de Peers**: Mantém a lista de peers e seu estado.
- **Servidor TCP**: Gerencia conexões e mensagens recebidas.
- **Cliente TCP**: Envia mensagens para outros peers.
- **Gerenciador de Arquivos**: Lista arquivos disponíveis no diretório.

---

### 📌 Bibliotecas Python a Serem Utilizadas

1. **`socket`** – Para comunicação TCP entre peers.
2. **`threading`** – Para permitir múltiplas conexões simultâneas.
3. **`os`** – Para manipulação de arquivos e diretórios compartilhados.
4. **`sys`** – Para capturar argumentos de linha de comando.
5. **`time`** – Para controle do relógio lógico.
6. **`logging`** – Para registrar eventos e mensagens trocadas.
