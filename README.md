# Service Discovery - Consul

### conceito: O que é Service Discovery

Service Discovery (descoberta de serviços) é o processo que permite que serviços dentro de uma infraestrutura distribuída encontrem e se comuniquem uns com os outros automaticamente.

Em sistemas modernos (como microsserviços), novas máquinas e containers são criados e destruídos frequentemente. Além disso, o tráfego é muitas vezes distribuído via **load balancers**.

Sem um mecanismo de descoberta, seria inviável saber manualmente:

- Quais serviços estão ativos.
- Em quais endereços ou portas eles estão disponíveis.
- Para onde enviar o tráfego de rede corretamente.
  - Tráfego é o fluxo de dados ou requisições transmitidas entre computadores ou serviços em uma rede.

O **Service Discovery** resolve esse problema mantendo um **registro centralizado de serviços ativos** e atualizando automaticamente quando ocorrem mudanças (como criação, remoção ou falha de instâncias).

#### Principais Funções

1. **Descoberta de instâncias disponíveis**
    - Permite que um serviço descubra automaticamente **quais instâncias** estão disponíveis para receber requisições.
    - Exemplo: Existem 10 instâncias de **App B**, mas apenas 8 estão **saudáveis**. O Service Discovery só retorna essas 8.
2. **Segmentação e Políticas de Acesso**
    - Define **quem pode acessar quem**, de acordo com políticas e regras de segurança.
    - Evita alterações manuais complexas em firewalls.
3. **Resolução via DNS**
    - O cliente usa o **nome do serviço**.
    - O **DNS** resolve esse nome para um **IP válido** entre as instâncias registradas.
4. **Health Check**
    - Verifica a **saúde** das instâncias.
    - Faz **ping** em portas HTTP ou endereços TCP.
    - Remove (ou “desregistra”) instâncias que não respondem.
5. **Controle de Acesso**
    - Garante que somente serviços **autorizados** possam se comunicar.

----

### ferramenta: Consul

O Consul atua como intermediário entre os serviços de uma aplicação, permitindo que eles se encontrem e se comuniquem sem depender de endereços fixos. Ele é agnóstico a linguagem, sistema operacional ou framework — pode ser usado em praticamente qualquer ambiente.

**Consul** é uma ferramenta criada pela **HashiCorp** que oferece múltiplas funcionalidades para ambientes distribuídos, incluindo:

- **Service Discovery:** permite que os serviços registrem e descubram uns aos outros automaticamente.
- **Health Check:** monitora continuamente o estado dos serviços registrados e remove instâncias que não estão saudáveis.
- **Service Segmentation:** oferece controle de acesso e isolamento entre serviços.
- **Load Balancer na Borda (Layer 7):** fornece balanceamento de carga inteligente entre instâncias de serviços.
- **Armazenamento Key/Value:** permite armazenar e gerenciar configurações e segredos, como variáveis de ambiente (ex: credenciais de banco de dados, chaves de API). Pode ser usado para injeção de variáveis durante pipelines de CI.
- **Segurança:** suporta **mTLS (Mutual TLS)** para autenticação mútua e **Service Mesh**, funcionando como proxy entre microserviços

No contexto de Service Discovery, o Consul atua como um **catálogo central** de serviços, permitindo que os clientes saibam onde cada serviço está executando e redirecionem o tráfego de forma dinâmica.

#### partes

- **service registry**: É um repositório central onde todos os serviços de uma aplicação distribuída estão registrados.
- **consul agent**: - Cada aplicação (App) tem um **Consul Agent** que envia informações sobre si para o **Consul Server**.
- **Health Check**: feito pelo **Consul Agent (sidecar)** diretamente no serviço. O agente comunica o status ao servidor.
- **Servidor líder**: o Consul Server que gerencia a informação central.
- **Gossip Protocol**: protocolo usado entre agentes para informar quem está ativo ou inativo (fofoca entre nodes).
- **consul - dns server**:
- **consul - api**:

---- 

### Comandos para iniciar o ambiente

- instalar o docker

```bash
# Subir os containers em modo destaque
docker compose up -d

# Configurar o agent (adapte conforme sua necessidade)

# Acessar o container do agent (exemplo com consul01)
docker exec -it consul01 sh
```