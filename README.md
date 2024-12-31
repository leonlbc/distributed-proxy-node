# Distributed Proxy Node

## Aplicação Distribuída de Proxy para LAN

Esta aplicação implementa um sistema distribuído de proxy para uma rede local (LAN). Ela garante que exatamente um nó na rede atue como proxy para lidar com requisições que exigem conectividade com um serviço que apenas um dos nós está conectado. Outros nós na LAN descobrem automaticamente e redirecionam as requisições para o proxy ativo.


![DistributedProxy](https://github.com/user-attachments/assets/d1246e45-33d8-4eb4-9007-796f2e65ab72)


## Fluxo

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

