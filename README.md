# GAN para Geração do Dígito "4" do MNIST com PyTorch

Este projeto implementa uma Rede Adversarial Generativa (GAN) para gerar imagens manuscritas do dígito "4", utilizando o subconjunto correspondente do dataset MNIST e a biblioteca PyTorch.

O notebook principal do projeto, contendo todo o código e as execuções, é o `MNIST_GAN_Digito4.ipynb`.

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dede0702/mnist-digit-4-gan/blob/main/MNIST_GAN_Digito4.ipynb)
*(Certifique-se de que o arquivo `MNIST_GAN_Digito4.ipynb` está no diretório raiz do seu repositório na branch `main` para este link funcionar corretamente)*

## 🎯 Objetivo

O objetivo principal é construir, treinar e avaliar um modelo GAN capaz de:
1. Aprender a distribuição dos dados das imagens do dígito "4" do MNIST.
2. Gerar novas amostras de imagens do dígito "4" que sejam visualmente realistas e diversificadas.
3. Demonstrar o processo de treinamento de GANs para uma tarefa de geração de imagem específica.

## 🧑‍💻 Integrantes

- Andre Rovai        (RM555848)
- Lancelot Chagas    (RM554707)

## 📂 Estrutura do Repositório

A estrutura de arquivos do projeto é a seguinte:
Use code with caution.
Markdown
mnist-digit-4-gan/
│
├── MNIST_GAN_Digito4.ipynb # Notebook principal com todo o código, treinamento e visualizações
├── generator_4.pt # Pesos do modelo Gerador treinado (state_dict)
├── discriminator_4.pt # Pesos do modelo Discriminador treinado (state_dict)
└── README.md # Este arquivo de descrição do projeto
*Observação: Os arquivos `.pt` contêm os modelos treinados. O dataset MNIST é baixado automaticamente pelo script no notebook e geralmente não é incluído no repositório.*

## 🛠️ Tecnologias Utilizadas

- Python 3.x
- PyTorch
- Torchvision (para o dataset MNIST e transformações)
- Matplotlib (para visualização de imagens)

## ⚙️ Estrutura do Código (conforme no Notebook `MNIST_GAN_Digito4.ipynb`)

O projeto está estruturado nas seguintes etapas principais dentro do notebook:

1.  **Etapa 1: Instalar dependências**
    *   Instalação das bibliotecas necessárias (`torch`, `torchvision`, `matplotlib`).

2.  **Etapa 2: Importar bibliotecas**
    *   Importação dos módulos essenciais para o projeto.

3.  **Etapa 3: Carregar apenas os dígitos 4 do MNIST (usando torchvision)**
    *   Implementação da classe `MNIST4Dataset`:
        *   Carrega o dataset MNIST utilizando `torchvision.datasets.MNIST`.
        *   Filtra o dataset para incluir apenas as imagens correspondentes ao dígito "4".
        *   Realiza o pré-processamento necessário nas imagens (normalização para o intervalo `[-1, 1]` e adição da dimensão do canal).
    *   Criação do `DataLoader` para fornecer os dados em batches.

4.  **Etapa 4: Definir o Discriminador**
    *   Implementação da classe `Discriminator`: uma rede neural convolucional (CNN) que classifica imagens como reais ou falsas.
    *   Arquitetura: Sequência de camadas `Conv2d`, `LeakyReLU`, `Dropout`, `BatchNorm2d`, `Flatten`, `Linear` e `Sigmoid`.

5.  **Etapa 5: Definir o Gerador**
    *   Implementação da classe `Generator`: uma rede neural que gera imagens a partir de um vetor de ruído.
    *   Arquitetura: Sequência de camadas `Linear`, `LeakyReLU`, `BatchNorm1d`, `Unflatten`, `ConvTranspose2d`, `BatchNorm2d` e `Tanh`.

6.  **Etapa 6: Inicializar modelos, otimizadores e parâmetros**
    *   Definição de hiperparâmetros (dimensão latente, taxa de aprendizado, betas do Adam).
    *   Inicialização dos modelos Gerador e Discriminador, otimizadores (Adam), e função de perda (BCELoss).
    *   Configuração do dispositivo (CPU ou GPU).
    *   (Opcional) Inicialização de pesos.

7.  **Etapa 7: Treinar a GAN e Visualizar Resultados Parciais**
    *   Loop principal de treinamento:
        *   Itera sobre o número de épocas e batches.
        *   Treina o Discriminador com imagens reais e falsas.
        *   Treina o Gerador para enganar o Discriminador.
        *   Imprime as perdas (Loss_D, Loss_G) ao final de cada época.
        *   Visualiza amostras de imagens geradas a cada 10 épocas.

8.  **Etapa 8: Salvar os modelos (após o treinamento)**
    *   Salva os pesos (`state_dict`) dos modelos Gerador e Discriminador treinados nos arquivos `generator_4.pt` e `discriminator_4.pt`.

## 🚀 Como Executar

A maneira mais fácil de executar o projeto é através do Google Colab:

1.  Clique no botão "Abrir no Colab" no início deste README para abrir o notebook `MNIST_GAN_Digito4.ipynb` diretamente no Google Colab.
    [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dede0702/mnist-digit-4-gan/blob/main/MNIST_GAN_Digito4.ipynb)
2.  No Colab, certifique-se de selecionar um ambiente de execução com GPU para um treinamento mais rápido (Ambiente de execução -> Alterar tipo de ambiente de execução -> Acelerador de hardware -> GPU).
3.  Execute as células do notebook em sequência.

Alternativamente, para executar localmente:

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/dede0702/mnist-digit-4-gan.git
    cd mnist-digit-4-gan
    ```

2.  **Instale as dependências:**
    ```bash
    pip install torch torchvision matplotlib
    ```
    (Recomenda-se o uso de um ambiente virtual Python: `python -m venv venv`, depois `source venv/bin/activate` ou `venv\Scripts\activate` no Windows).

3.  **Execute o notebook `MNIST_GAN_Digito4.ipynb`** usando Jupyter Notebook, JupyterLab, VS Code ou outra IDE compatível.

## 🖼️ Resultados Esperados

-   Saída no console/notebook mostrando as perdas do Discriminador (Loss_D) e do Gerador (Loss_G) a cada época de treinamento.
-   Exibição de grades de imagens (4x4) geradas pelo modelo a cada 10 épocas, permitindo visualizar a melhoria progressiva na qualidade das imagens.
-   Ao final da execução, os arquivos `generator_4.pt` e `discriminator_4.pt` serão criados (se executado localmente e a célula de salvamento for executada) ou poderão ser baixados do ambiente Colab.

Exemplo de imagem gerada (após treinamento suficiente):
*(Você pode adicionar uma pequena imagem de exemplo aqui se desejar, por exemplo, uma captura de tela de uma boa saída do gerador)*
<!-- <p align="center">
  <img src="path/to/your/sample_generated_image.png" width="200" alt="Exemplo de Dígito 4 Gerado">
</p> -->

## 🔮 Possíveis Melhorias e Próximos Passos

-   **Ajuste Fino de Hiperparâmetros**: Experimentar diferentes taxas de aprendizado, tamanhos de batch, dimensões do espaço latente, ou arquiteturas para os modelos.
-   **Técnicas de Estabilização de Treinamento**: Investigar e implementar técnicas como "label smoothing", diferentes funções de perda (ex: WGAN), ou normalização espectral.
-   **Avaliação Quantitativa**: Implementar métricas como Fréchet Inception Distance (FID) ou Inception Score (IS) para avaliar a qualidade e diversidade das imagens geradas.
-   **Geração Condicional**: Modificar a GAN para ser capaz de gerar outros dígitos ou variações específicas.
-   **Treinamento em Outros Dígitos**: Adaptar o `MNIST4Dataset` para treinar a GAN em outros dígitos individualmente.
