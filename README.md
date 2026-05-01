# Service Discovery - Consul

### O que é Service Discovery

Service Discovery (descoberta de serviços) é o processo que permite que serviços dentro de uma infraestrutura distribuída encontrem e se comuniquem uns com os outros automaticamente.

Em sistemas modernos (como microsserviços), novas máquinas e containers são criados e destruídos frequentemente. Além disso, o tráfego é muitas vezes distribuído via **load balancers**.

Sem um mecanismo de descoberta, seria inviável saber manualmente:

- Quais serviços estão ativos.
- Em quais endereços ou portas eles estão disponíveis.
- Para onde enviar o tráfego de rede corretamente.

O **Service Discovery** resolve esse problema mantendo um **registro centralizado de serviços ativos** e atualizando automaticamente quando ocorrem mudanças (como criação, remoção ou falha de instâncias).

----

### Principais Funções

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

### Consul

**Consul** é uma ferramenta criada pela **HashiCorp** que oferece múltiplas funcionalidades para ambientes distribuídos, incluindo:

- **Service Discovery**: registro e descoberta automática de serviços.
- **Health Checking**: monitora o estado dos serviços registrados.
- **Key/Value Store**: armazena dados de configuração de forma distribuída.
- **Service Mesh (Consul Connect)**: provê comunicação segura entre serviços com controle de tráfego e autenticação mútua.

No contexto de Service Discovery, o Consul atua como um **catálogo central** de serviços, permitindo que os clientes saibam onde cada serviço está executando e redirecionem o tráfego de forma dinâmica.

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