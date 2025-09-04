⚙️ Gerenciamento de Serviços e Monitoramento no Linux (AWS EC2)

Este projeto documenta um laboratório prático em uma instância Amazon Linux EC2, focado no gerenciamento de serviços e no monitoramento de recursos do sistema. O objetivo foi aprender a verificar o status de serviços, a monitorar processos com o top e a usar o AWS CloudWatch para obter uma visão mais ampla da performance da instância.

---

### 🛠️ Tecnologias Utilizadas

<div align="left"> <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" alt="AWS" width="50" height="50"/> <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linux/linux-original.svg" alt="Linux" width="50" height="50"/>
</div>

---

### 🎯 Objetivos

* Verificar o status do serviço httpd e iniciar/parar o serviço.
* Acessar uma página web de teste na instância EC2.
* Monitorar o uso de CPU com o comando top.
* Visualizar métricas de desempenho no AWS CloudWatch.

---

### 🚀 Ambiente

* Serviço: Amazon EC2
* Tipo de instância: t3.micro (1 vCPU, 1 GiB RAM)
* Sistema Operacional: Amazon Linux 2
* Acesso: SSH (via .pem ou .ppk)

---

### 📌 Etapas do Laboratório

#### 1. Conexão via SSH

1.  Baixei a chave de acesso (.pem para Mac/Linux ou .ppk para Windows).
2.  Altere as permissões da chave:
    ```bash
    chmod 400 labsuser.pem
    ```
3.  Conectei-me à instância usando o comando:
    ```bash
    ssh -i labsuser.pem ec2-user@<public-ip>
    ```

#### 2. Verificando o Status do Serviço httpd

O serviço httpd (Apache HTTP Server) é um servidor web leve, e este exercício me ajudou a entender como gerenciá-lo.

1.  Verifiquei o status inicial:
    ```bash
    sudo systemctl status httpd.service
    ```
    O resultado mostrou que o serviço estava inativo (dead).

2.  Iniciei o serviço e verifiquei novamente:
    ```bash
    sudo systemctl start httpd.service
    sudo systemctl status httpd.service
    ```
    O status mudou para ativo (running), confirmando que o serviço foi iniciado com sucesso.

3.  Validei o funcionamento:
    Abri um novo navegador e acessei o IP Público da minha instância. Uma página de teste padrão do Apache foi exibida, provando que o servidor web estava funcionando e acessível.

4.  Parei o serviço:
    Finalizei a tarefa com o comando `sudo systemctl stop httpd.service`.

#### 3. Monitorando a Instância EC2

Nesta etapa, explorei duas formas de monitoramento: via terminal com o comando top e via console da AWS com o CloudWatch.

* **Monitoramento com top:**
    Executei o comando `top` para ver o uso de recursos em tempo real. Pressionei `q` para sair.
    Em seguida, rodei um script para simular um alto consumo de CPU:
    ```bash
    ./stress.sh & top
    ```
    Com o top aberto, observei que o processo stress.sh estava consumindo uma alta porcentagem de CPU.

* **Monitoramento com CloudWatch:**
    No console da AWS, naveguei até o serviço CloudWatch e acessei o painel Automatic dashboards > EC2.
    Consegui visualizar um pico no gráfico de CPU Utilization que correspondia exatamente ao momento em que iniciei o script de estresse. Foi impressionante ver como o CloudWatch captura e visualiza esses dados. Depois que o script parou, o uso da CPU voltou ao normal, o que também foi refletido no gráfico.

---

### 📈 Conclusão

Este laboratório me deu uma visão completa sobre o gerenciamento de serviços e o monitoramento de desempenho. Aprendi a importância de ferramentas como systemctl para controlar serviços e de top para um monitoramento rápido. O AWS CloudWatch se mostrou uma ferramenta poderosa e essencial para monitoramento em larga escala, oferecendo uma visão detalhada e histórica do desempenho da instância.
