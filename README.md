# 🐧 Gerenciamento de Serviços e Monitoramento no Linux (AWS EC2)

---

Este repositório documenta um laboratório prático em uma instância Amazon Linux EC2, focado no gerenciamento de serviços e no monitoramento de recursos do sistema. O objetivo foi aprender a verificar o status de serviços, a monitorar processos com o top e a usar o AWS CloudWatch para obter uma visão mais ampla da performance da instância.

---

# 📂 **Estrutura do Projeto**

```
gerenciamento-e-monitoramento-linux/
│
├── imagens/
│
└── README.md
```
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
2.  Alterei as permissões da chave:
    ```bash
    chmod 400 labsuser.pem
    ```
3.  Conectei-me à instância usando o comando:
    ```bash
    ssh -i labsuser.pem ec2-user@<public-ip>
    ```

    <img width="1299" height="735" alt="01-acesso-ssh" src="https://github.com/user-attachments/assets/f6b2e389-4034-4a08-9e81-2c240b534029" />

---

#### 2. Verificando o Status do Serviço httpd

O serviço httpd (Apache HTTP Server) é um servidor web leve, e este exercício me ajudou a entender como gerenciá-lo.

1.  Verifiquei o status inicial:
    ```bash
    sudo systemctl status httpd.service
    ```
    
    <img width="1299" height="735" alt="02-status-inicial" src="https://github.com/user-attachments/assets/ff4811e5-f764-4e51-95e1-42b55b621a6f" />

    O resultado mostrou que o serviço estava inativo (dead).

1.  Iniciei o serviço e verifiquei novamente:
    ```bash
    sudo systemctl start httpd.service
    sudo systemctl status httpd.service
    ```
    
    <img width="1299" height="735" alt="03-inicio-servico" src="https://github.com/user-attachments/assets/ec764dbd-3ba2-4c03-b5f2-b090bdbd35c3" />

    O status mudou para ativo (running), confirmando que o serviço foi iniciado com sucesso.

2.  Validei o funcionamento:
    Abri um novo navegador e acessei o IP Público da minha instância. Uma página de teste padrão do Apache foi exibida, provando que o servidor web estava funcionando e acessível.

    <img width="1058" height="557" alt="04-instancia-funcionando" src="https://github.com/user-attachments/assets/6ccec09e-09fe-441d-8766-d973309351c7" />

    <img width="1296" height="694" alt="05-validacao-funcionamento" src="https://github.com/user-attachments/assets/ae797c60-f655-48b3-ab78-76ab3638e56c" />

4.  Parei o serviço:
    Finalizei a tarefa com o comando `sudo systemctl stop httpd.service`.

    <img width="1297" height="736" alt="06-parada-servico" src="https://github.com/user-attachments/assets/5c31eb25-d4f3-44c5-a8ed-12291f407ffc" />

---

#### 3. Monitorando a Instância EC2

Nesta etapa, explorei duas formas de monitoramento: via terminal com o comando top e via console da AWS com o CloudWatch.

* **Monitoramento com top:**
    Executei o comando `top` para ver o uso de recursos em tempo real.

    <img width="1297" height="736" alt="07-monitoramento-top" src="https://github.com/user-attachments/assets/2afed66a-f666-4aaa-bb50-424a1b5b6170" />

    Em seguida, rodei um script para simular um alto consumo de CPU:
    ```bash
    ./stress.sh & top
    ```
    
    Com o top aberto, observei que o processo stress.sh estava consumindo uma alta porcentagem de CPU.

    <img width="1297" height="736" alt="08-monitoramento-stress-top" src="https://github.com/user-attachments/assets/c14bbf5b-0236-44a9-809a-eb98d1333b79" />

---

* **Monitoramento com CloudWatch:**
    No console da AWS, naveguei até o serviço CloudWatch e acessei o painel Automatic dashboards > EC2.
    Consegui visualizar um pico no gráfico de CPU Utilization que correspondia exatamente ao momento em que iniciei o script de estresse. Foi impressionante ver como o CloudWatch captura e visualiza esses dados. Depois que o script parou, o uso da CPU voltou ao normal, o que também foi refletido no gráfico.

  <img width="1299" height="652" alt="09-monitoramento-cloudwatch" src="https://github.com/user-attachments/assets/e6c12b5f-89de-4446-ab3d-95f90ec875a2" />

---

### 📈 Conclusão

Este laboratório me deu uma visão completa sobre o gerenciamento de serviços e o monitoramento de desempenho. Aprendi a importância de ferramentas como systemctl para controlar serviços e de top para um monitoramento rápido. O AWS CloudWatch se mostrou uma ferramenta poderosa e essencial para monitoramento em larga escala, oferecendo uma visão detalhada e histórica do desempenho computacional da instância.
