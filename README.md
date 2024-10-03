# Computação e Rede na Azure
---
Este repositório contém o resumo das lições aprendidas durante o desenvolvimento do lab Configurando Recursos e Dimensionamentos em Máquinas Virtuais na Azure na plataforma DIO

---
## Introdução
Neste laboratório foram vistos os principais tópicos abordados sobre computação e rede no Azure, com foco em serviços de computação, redes virtuais e contêineres. O Azure oferece uma infraestrutura de cloud computing flexível e escalável que inclui VMs, serviços de contêiner, Kubernetes, e redes virtuais, fornecendo alta disponibilidade, segurança e performance. 

---

## Serviços de Computação do Azure

### Máquinas Virtuais do Azure (Windows ou Linux)
- Controle total sobre processador virtual, memória, armazenamento, rede, instalação e remoção de aplicações. Responsabilidade compartilhada (IaaS).
- Ideal para migrações de "lift-and-shift", sem necessidade de alterações no aplicativo ao mover para a nuvem.
- As VMs são isoladas através da virtualização de hardware com hypervisores.
- Cada VM possui sua própria instância de sistema operacional, podendo rodar sistemas operacionais diferentes.

### Conjuntos de Dimensionamento de VMs
- Oferecem balanceamento de carga e permitem o dimensionamento automático dos recursos.

### Conjuntos de Disponibilidade de VMs
- As VMs são distribuídas em até 3 domínios de falha e em domínios de atualização para garantir alta disponibilidade.
- Se um domínio de falha falhar, a disponibilidade é mantida por outro domínio.
- Sem custos adicionais pela configuração de conjuntos de disponibilidade, pagam-se apenas pelas instâncias.

### Área de Trabalho Virtual
- Área de trabalho do Windows baseada em nuvem, permitindo a execução de aplicativos de forma remota.
- Personalização avançada, gerenciamento atualizado e possibilidade de vários usuários no mesmo computador ao mesmo tempo.
- Utiliza o EntraID para controle de permissões e segurança.
- Reduz o risco de deixar recursos desatualizados e suporta implantação de múltiplas sessões.

## Serviço de Contêineres

- Aplicativos e serviços são empacotados em contêineres que rodam sobre o sistema operacional do host.
- Contêineres são leves, rápidos e podem ser escalados ou interrompidos sob demanda.
- **Instâncias de Contêineres**: PaaS que executa contêineres de forma simplificada.
- **Aplicativos de Contêineres**: balanceiam a carga e escalam automaticamente, removendo a necessidade de gerenciamento manual.
- **Serviço de Kubernetes (AKS)**: gerencia grandes volumes de contêineres distribuídos, automatizando o ciclo de vida dos contêineres.
- Contêineres são isolados a nível de sistema operacional (compartilham o kernel), mas não fazem abstração completa do hardware como VMs.

## Azure Functions
- Plataforma PaaS que oferece computação sem servidor (serverless).
- Executa código baseado em eventos (com ou sem estado) que é disparado por gatilhos e escala conforme a demanda.
- Exemplo: notificação de compilação ou execução de atividades quando um servidor fica inativo.

## Serviços de Aplicativo
- PaaS para criar, implantar e dimensionar aplicativos Web e APIs com requisitos de alto desempenho, segurança e conformidade.
- Suporta várias linguagens: .Net, .Net Core, Node.js, Java, Python e PHP.
- Executa em Windows ou Linux.

## Serviços de Rede Virtual (VNet)
- Permite comunicação entre recursos do Azure, a internet e redes locais.
- As VNets devem ser separadas para proteger contra ataques laterais. Emparelhamento de redes é necessário para comunicação entre VNets.
- **Pontos de extremidade públicos**: acessíveis de qualquer lugar na Internet.
- **Pontos de extremidade privados**: acessíveis somente dentro da rede.
- **Gateway de VPN**: criptografa o tráfego entre redes virtuais do Azure e redes on-premise pela internet pública.
- **ExpressRoute**: conexão direta e privada entre o datacenter da empresa e o Azure, usando um provedor de conectividade, garantindo maior performance e segurança.

## DNS do Azure
- Registros de alias para apontar diretamente para recursos do Azure.
- Segurança baseada no Gerenciador de Recursos, permitindo controle de acesso baseado em função.
- Usa a rede Anycast, aproveitando uma rede global de servidores.
- Facilita o gerenciamento de DNS para recursos internos e externos.

## Laboratório: Configuração de Recursos e Dimensionamentos em Máquinas Virtuais na Azure

### Criando uma Máquina Virtual
1. **Básico**:
   - Escolher assinatura e grupo de recurso.
   - Nomear a VM e selecionar a região (East US2 é uma opção econômica).
   - Definir opções de disponibilidade (Nenhuma redundância de infraestrutura para testes).
   - Escolher configuração de escala e definir condições de dimensionamento automático.
   - **Desconto de Spot**: VMs podem ser usadas com desconto para desenvolvimento/testes, mas podem ser derrubadas se outro cliente pagar o preço cheio.
   - Escolher tamanho da VM (CPU, memória).
   - Criar conta de administrador e selecionar portas de entrada (RDP para testes).
2. **Discos**:
   - Escolher tipo de disco (Premium recomendado para produção).
   - Marcar opção de excluir disco junto com a VM para evitar custos desnecessários.
3. **Rede**:
   - Criar rede virtual ou usar uma existente, garantindo que esteja na mesma região da VM.
   - Excluir IP público e NIC junto com a VM, se desejado.
4. **Gerenciamento**:
   - Em produção, usar o EntraID para acesso.
   - Configurar desligamento automático e habilitar backup, se necessário.
5. **Monitoramento**:
   - Definir regras de alerta e diagnósticos de inicialização, se necessário.
6. **Avançado**:
   - Instalar extensões e aplicar tags durante a criação da VM.
7. **Revisão e criação**:
   - Revisar todas as configurações e custos estimados antes de criar a VM.

### Área de Trabalho Virtual
- Escolher tipo de pool de hosts (Pessoal para uso dedicado, ou Em Pool para compartilhamento entre usuários).

### Aplicativo de Funções
- Definir nome, se será código ou contêiner, e a pilha de runtime.
