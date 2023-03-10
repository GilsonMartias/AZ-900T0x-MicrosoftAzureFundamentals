---
wts:
  title: 04 – Criar uma rede virtual (20 min)
  module: Module 02 - Core Azure Services (Workloads)
---
# <a name="04---create-a-virtual-network-20-min"></a>04 – Criar uma rede virtual (20 min)

Neste passo a passo, vamos criar uma rede virtual, implantar duas máquinas virtuais nessa rede e configurá-las para permitir que uma máquina virtual execute ping na outra dentro dessa rede virtual.

# <a name="task-1-create-a-virtual-network"></a>Tarefa 1: criar uma rede virtual 

Nesta tarefa, você criará uma rede virtual. 

Observação: antes de iniciar o laboratório, desabilite o firewall público e privado em sua máquina virtual abrindo a Rede menu Iniciar > Configurações > e a Internet > Localize Windows Firewall

1. Entre no portal do Microsoft Azure em <a href="https://portal.azure.com" target="_blank"><span style="color: #0066cc;" color="#0066cc">https://portal.azure.com</span></a>

2. Na folha **Todos os serviços**, procure e selecione **Máquinas virtuais** e, em seguida, selecione **+ Adicionar, + Criar, + Novo**. 

3. Na guia **Básico**, preencha as seguintes informações (mantenha os padrões para todo o resto):

    | Configuração | Valor | 
    | --- | --- |
    | Subscription | **Manter a padrão fornecida** |
    | Grupo de recursos | **Criar grupo de recursos** |
    | Nome | **vnet1** |
    | Região | **(EUA) Leste dos EUA** |
    
   
4. Clique no botão **Examinar + criar**. Certifique-se de que a validação seja aprovada. Depois clique em criar para implantar o recurso.


# <a name="task-2-create-two-virtual-machines"></a>Tarefa 2: Criar duas máquinas virtuais

Nesta tarefa, criaremos duas máquinas virtuais na rede virtual. 

1. Na folha **Todos os serviços**, procure **Máquinas virtuais**, selecione **+ Adicionar, + Criar, + Novo** e, na lista suspensa, escolha **Máquina Virtual**. 

2. Na guia **Básico**, preencha as seguintes informações (mantenha os padrões para todo o resto):

   | Configuração | Valor | 
   | --- | --- |
   | Subscription | **Use a padrão fornecida** |
   | Resource group |  **Selecionar o padrão na lista suspensa** |
   | Nome da máquina virtual | **vm1**|
   | Região | **(EUA) Leste dos EUA** |
   | Image | **Windows Server 2019 Datacenter – Gen2** |
   | Nome de Usuário| **azureuser** |
   | Senha| **Pa$$w0rd1234** |
   | Porta de entrada públicas| Selecione **Permitir portas selecionadas**  |
   | Portas de entrada selecionadas| **RDP (3389)** |
   

3. Selecione a guia **Rede**. Certifique-se de que a máquina virtual seja colocada na rede virtual **vnet1**. Revise as configurações padrão, mas não faça nenhuma outra alteração. 

4. Clique em **Revisar + Criar**. Após a validação, selecione **Criar**. O tempo de implantação pode variar, mas geralmente leva de três a seis minutos para ser concluído.

5. Monitore sua implantação, mas continue na próxima etapa. 

6. Crie uma segunda máquina virtual repetindo as etapas **2 a 4** acima. Use um nome de máquina virtual diferente e garanta que a máquina virtual esteja dentro da mesma rede virtual e esteja usando um novo endereço IP público:

    | Configuração | Valor |
    | --- | --- |
    | Resource group | **selecione o padrão no menu suspenso (o mesmo que Tarefa1-3 e Tarefa2-2)** |
    | Nome da máquina virtual |  **vm2** |
    | Rede virtual | **vnet1** |
    | IP público | **vm2-ip** |

7. Espere as duas máquinas virtuais serem implantadas e o status mudar para *em execução*.

# <a name="task-3-test-the-connection"></a>Tarefa 3: Testar a conexão 

Nesta tarefa, vamos testar se as máquinas virtuais podem se comunicar (executar ping). Caso contrário, vamos instalar uma regra para permitir uma conexão ICMP. No geral, as conexões ICMP são bloqueadas automaticamente.

1. Na folha **Todos os recursos**, procure **vm1**, abra sua folha **Visão geral** e certifique-se de que seu **Status** seja **Em execução**. Talvez seja necessário **Atualizar** a página.

2. Na folha **Visão geral**, selecione **Conectar** e depois **RDP** na lista suspensa.

    **Observação**: As instruções a seguir mostram como se conectar à VM a partir de um computador Windows. 

3. Na folha **Conectar ao RDP**, mantenha as opções padrão para se conectar ao endereço IP na porta 3389 e selecione **Baixar Arquivo RDP**.

4. Abra o arquivo RDP baixado (no canto inferior esquerdo da VM) e selecione **Conectar** quando solicitado. 

5. Na janela **Segurança do Windows**, digite o nome de usuário **azureuser** e a senha **Pa$$w0rd1234** e clique em **OK**.

6. Você pode receber um aviso do certificado durante o processo de logon. Clique em **Sim** para criar a conexão e se conectar à VM implantada. Você deve se conectar com sucesso. Feche o Windows Server e as janelas pop-up do Painel. Deve ser exibido um plano de fundo azul do Windows. Agora você está na máquina virtual.

7. Em **ambas** as máquinas virtuais recém-criadas, conecte-se por meio de RDP e desabilite o firewall público e privado abrindo o menu Iniciar > Configurações > Rede e Internet > Localizar Windows Firewall.

8. Abra o PowerShell na máquina virtual selecionando o botão **Iniciar**. Em Pesquisar, insira **PowerShell** e clique com o botão direito em **Windows PowerShell** para **Executar como administrador**

9. No PowerShell, tente executar ping na vm2 inserindo:

   ```PowerShell
   ping vm2
   ```

 10. É provável que você tenha êxito. Você executou ping na VM2 a partir da VM1.


**Parabéns!** Você configurou e implantou duas máquinas virtuais em uma rede virtual e conseguiu conectá-las.

**Observação**: Para evitar custos adicionais, você tem a opção de remover este grupo de recursos. Procure grupos de recursos, clique em seu grupo de recursos e, em seguida, clique em **Excluir grupo de recursos**. Verifique o nome do grupo de recursos e clique em **Excluir**. Monitore as **Notificações** para ver como a exclusão está ocorrendo.
