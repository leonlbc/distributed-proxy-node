# Distributed Proxy Node

## Aplicação Distribuída de Proxy para LAN

Esta aplicação implementa um sistema distribuído de proxy para uma rede local (LAN). Ela garante que exatamente um nó na rede atue como proxy para lidar com requisições que exigem conectividade com um serviço que apenas um dos nós está conectado. Outros nós na LAN descobrem automaticamente e redirecionam as requisições para o proxy ativo.

![DistributedProxy](https://github.com/user-attachments/assets/1b664660-88c4-4d4f-a78d-252595199925)

## Principais Funcionalidades

1. **Checagem Periódica de Conexão Externa**  
   Cada nó verifica periodicamente se possui acesso ao serviço.

2. **Seleção Automática do Proxy
   - O nó com conectividade torna-se o proxy ativo.
   - Caso nenhum nó possua conectividade, o sistema detecta a ausência de um proxy.

4. **Broadcast e Descoberta**  
   - O proxy ativo envia periodicamente um broadcast via UDP com informações sobre sua disponibilidade (IP e porta).
   - Nós não-proxy ouvem os broadcasts para descobrir o proxy.

5. **Servidor HTTP Proxy**  
   - O nó proxy executa um servidor HTTP em Flask.
   - Disponibiliza o endpoint (ex.: `/requestExternalData`) para encaminhar requisições para o serviço externo.

6. **Implementação**  
   Todos os componentes, incluindo a checagem de conexão, broadcast, listener e servidor HTTP, estão encapsulados em um único script Python.

## Como Funciona

### Fluxo de Trabalho
1. **Checagem de Conectividade**  
   Cada nó verifica acesso ao serviço target.

2. **Broadcast do Proxy**  
   Se um nó tiver acesso ao serviço, ele inicia um broadcast de seu IP e porta do servidor HTTP pela LAN.

3. **Listener**  
   Nós sem conectividade ouvem os broadcasts para identificar o proxy ativo.

4. **Servidor Flask**  
   O nó proxy executa um servidor Flask para lidar com requisições de outros nós e encaminhá-las para o serviço.

### Papéis
- **Nó Proxy**
   Lida com todas as requisições externas e envia broadcasts de sua disponibilidade.
- **Nós Não-Proxy**  
   Ouvem o proxy ativo, redirecionam suas requisições através dele e assumem o papel de proxy caso ganhem conectividade.



