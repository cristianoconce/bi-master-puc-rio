# Turismo Inteligente RJ: Uma Abordagem Integrada com RAG e Otimização de Planejamento

#### Aluno: [Cristiano Conceição](https://github.com/cristianoconce).
#### Orientadora: [Evelyn Batista](https://github.com/evysb).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.ele.puc-rio.br/cursos/mba-bi-master/) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- [Link para o código](https://github.com/cristianoconce/bi-master-puc-rio). 



---

### Resumo


Este trabalho propõe uma solução inovadora para turistas que visitam a cidade do Rio de Janeiro, oferecendo um maior conhecimento sobre os principais pontos turísticos e as melhores rotas para seus passeios. A primeira etapa do projeto consiste no desenvolvimento de um modelo baseado em Retrieval-Augmented Generation (RAG), que fornece informações detalhadas e personalizadas sobre os locais de interesse. Na segunda etapa, será realizada a modelagem de uma solução de otimização de planejamento, permitindo que, após a seleção dos pontos turísticos, sejam traçadas as rotas mais eficientes. Essa abordagem visa ajudar os turistas a otimizar seu tempo e reduzir os custos com deslocamento, proporcionando uma experiência mais prática e agradável.


This work proposes an innovative solution for tourists visiting the city of Rio de Janeiro, offering greater knowledge about the main tourist attractions and the best routes for their trips. The first stage of the project involves developing a model based on Retrieval-Augmented Generation (RAG), providing detailed and personalized information about the points of interest. In the second stage, a planning optimization solution will be modeled, enabling the creation of the most efficient routes after selecting the tourist attractions. This approach aims to help tourists optimize their time and reduce transportation costs, providing a more practical and enjoyable experience.

### 1. Introdução

O Rio de Janeiro é mundialmente conhecido por suas belezas naturais, pontos turísticos icônicos e rica diversidade cultural, atraindo milhões de turistas todos os anos. Apesar da ampla oferta de informações sobre a cidade, muitos visitantes enfrentam desafios na organização de seus passeios, como a dificuldade em selecionar os locais mais relevantes e otimizar suas rotas de deslocamento. Esse cenário ressalta a necessidade de soluções que integrem tecnologia e planejamento, permitindo aos turistas uma experiência mais prática, personalizada e eficiente.

Diante disso, este trabalho propõe uma abordagem inovadora para auxiliar turistas na exploração da cidade do Rio de Janeiro. A solução baseia-se em um modelo de Retrieval-Augmented Generation (RAG), projetado para fornecer informações detalhadas e adaptadas sobre os principais pontos turísticos. Além disso, a proposta inclui uma ferramenta de otimização de planejamento que, com base nos locais escolhidos, calcula as rotas mais eficientes. Essa combinação de tecnologia e logística visa otimizar o tempo dos visitantes, reduzir custos com deslocamentos e enriquecer a experiência turística, contribuindo para um aproveitamento mais completo da cidade.

### 2. Modelagem

1. Tecnologias e Modelos Envolvidos
1.1 Retrieval-Augmented Generation (RAG) e Banco de Dados Vetorial
O modelo proposto utiliza a abordagem Retrieval-Augmented Generation (RAG) para enriquecer a experiência dos turistas com informações detalhadas e personalizadas. Nesse contexto, o modelo baseia-se em representações vetoriais de textos e imagens associadas aos pontos turísticos, permitindo a busca eficiente e semântica de informações relevantes. Para isso, emprega-se o Milvus, um banco de dados vetorial altamente escalável e otimizado para consultas de similaridade.

O Milvus armazena vetores gerados a partir de embeddings de texto ou imagens utilizando modelos de aprendizado profundo, como BERT ou CLIP. A busca no banco é realizada com base na métrica de distância Euclidiana (L2), que mede a similaridade entre os vetores representativos das consultas do usuário e os pontos turísticos armazenados. Esse método garante que as informações retornadas sejam altamente relevantes e contextualizadas, fornecendo recomendações precisas aos turistas.<br />

<img src="https://milvus.io/images/embedding.png" alt="Distância Euclidiana (L2)" />

Para implementar a funcionalidade de busca, o processo segue os seguintes passos:

Conversão de Dados em Vetores: As descrições dos pontos turísticos e outros dados relacionados são transformados em embeddings vetoriais por meio de modelos de processamento de linguagem natural.
Armazenamento no Milvus: Os vetores são indexados no banco, facilitando consultas rápidas.
Busca Semântica: Quando o turista realiza uma consulta, o texto é transformado em um vetor, e o Milvus utiliza a métrica L2 para identificar os pontos turísticos mais relevantes.
Geração de Respostas Personalizadas: Após a recuperação das informações, o modelo RAG combina os dados encontrados para gerar respostas claras e personalizadas.
Essa integração entre RAG e Milvus permite não apenas oferecer informações precisas, mas também adaptar as respostas ao perfil e às necessidades de cada turista.

2. Otimização de Planejamento
2.1 Modelagem da Solução
A segunda etapa do projeto envolve a criação de um sistema de otimização para planejar os trajetos mais eficientes entre os pontos turísticos selecionados. Para isso, utiliza-se uma matriz de distâncias que representa os custos de deslocamento entre os locais, considerando fatores como tempo, distância geográfica e possíveis restrições logísticas.

O problema de planejamento é modelado como uma função objetivo a ser minimizada. A formulação do problema inclui:

Função Objetivo: Minimizar o custo total do deslocamento, dado pela soma das distâncias entre os pontos turísticos no trajeto escolhido.
Restrições: Garantir que todos os pontos selecionados sejam visitados uma única vez e que o trajeto forme um circuito fechado (no caso de retorno ao ponto de partida).
2.2 Implementação com FitnessMin e Operadores
O modelo de otimização utiliza um algoritmo genético baseado em operadores evolutivos, como seleção, cruzamento e mutação, para explorar diferentes combinações de rotas possíveis. A abordagem implementa:

Modelo FitnessMin: Avalia a aptidão de cada solução (rota) com base no custo total de deslocamento, buscando minimizar essa métrica.
Operadores Evolutivos:
Seleção: Baseada na aptidão, garantindo a sobrevivência das melhores soluções.
Cruzamento: Combina partes de diferentes soluções para criar novas rotas promissoras.
Mutação: Introduz pequenas alterações aleatórias para aumentar a diversidade e evitar soluções locais.
2.3 Hall of Fame e Matriz de Distâncias
Para aprimorar o desempenho do modelo, utiliza-se um Hall of Fame, que armazena as melhores soluções encontradas ao longo das gerações. Isso permite monitorar o progresso do algoritmo e resgatar as soluções mais eficientes.

A leitura da matriz de distâncias é feita previamente, utilizando dados reais ou estimados das distâncias entre os pontos turísticos. A matriz é estruturada como uma tabela simétrica, onde cada entrada 
e representa a distância entre o ponto turístico. Essas informações são fundamentais para calcular o custo total de cada rota e alimentar o algoritmo genético.


### 3. Resultados

1. Resultados da Implementação do Modelo RAG
A primeira etapa do projeto, que envolveu o desenvolvimento do modelo baseado em Retrieval-Augmented Generation (RAG), apresentou resultados satisfatórios em termos de relevância e precisão das informações fornecidas aos turistas. O uso do banco de dados vetorial Milvus permitiu:

Alta Eficiência na Busca Semântica: As consultas realizadas foram respondidas em tempo real, com informações altamente relevantes. A métrica de distância Euclidiana (L2) mostrou-se eficaz para identificar pontos turísticos que correspondiam ao contexto das buscas dos usuários.
Personalização das Respostas: O modelo foi capaz de adaptar as respostas de acordo com as preferências do turista, como o interesse por locais históricos, praias ou eventos culturais.
Escalabilidade: O Milvus demonstrou um desempenho consistente mesmo com grandes volumes de dados, garantindo a viabilidade da solução em um cenário com milhares de pontos turísticos e descrições associadas.

Exemplos de busca por informações no RAG:

No Milvus faremos a gravação dos dados com o seguinte schema:<br /><br />

ID - ID será uma chave primária gerada automaticamente.<br />
subject - Assunto para categoria de um contexto de negócio.<br />
text - O texto gravado com determinado contexto de negócio.<br />
vector - Estrutura de dados vetorial que vamos decodificar o texto que será gravado no formato do embedding.<br /><br />


Ponto turístico: Lagoa Rodrigo de Freitas.<br />
Pergunta do usuário: nível de vida populacional<br />
Top 3 melhores respostas:<br />
![image](https://github.com/user-attachments/assets/0f54918b-dc82-44e1-ba93-28e74ed37cff)

Ponto turístico: Praia de Copacabana.<br />
Pergunta do usuário: em termos populacionais<br />
Top 3 melhores respostas:<br />
![image](https://github.com/user-attachments/assets/011b4310-c2f4-4115-b0ad-90566401d531)

Ponto turístico: Praia da Barra da Tijuca.<br />
Pergunta do usuário: estrutura e arquitetura<br />
Top 3 melhores respostas:<br />
![image](https://github.com/user-attachments/assets/4efdd2c6-1334-4f98-9af4-ffaf49d9f1fc) 
<br /><br />


2. Resultados da Otimização de Planejamento
Na segunda etapa, o algoritmo de otimização baseado em métodos evolutivos foi avaliado em cenários com diferentes números de pontos turísticos selecionados pelos usuários.

Geramos uma matriz entre as distâncias de cada ponto turístico em Km:<br />
![image](https://github.com/user-attachments/assets/63944b6d-0eac-4be1-9648-e36777d59b9e)


Indicadores de Desempenho:<br />
Redução do Custo Total de Deslocamento: A melhor rota foi indicada pelos pontos turísticos 'Praça Mauá RJ', 'Pão de açucar RJ', 'Praia de Copacabana RJ',
       'Arpoador RJ', 'Praia de Ipanema RJ', 'Lagoa Rodrigo de Freitas RJ',
       'Cristo Redentor RJ', 'Praia da Barra da Tijuca'. <br />

Gráfico da melhor função objetivo: <br />
![image](https://github.com/user-attachments/assets/8ac2b247-ae9d-4425-ae36-67657533e17c)


### 4. Conclusões

4. Integração das Soluções
A integração entre o sistema de informações baseado em RAG e o otimizador de rotas resulta em uma experiência completa para o turista. O modelo identifica os pontos turísticos mais relevantes e, em seguida, organiza o trajeto de maneira eficiente, considerando preferências e restrições. Essa abordagem proporciona economia de tempo e custo, além de maximizar o aproveitamento das atrações da cidade.

A integração entre o modelo RAG e a otimização de planejamento foi testada em um cenário completo, simulando a experiência de um turista que seleciona 8 pontos turísticos para visitar. 

Os resultados mostraram que:

Experiência do Usuário: A combinação de informações detalhadas e rotas otimizadas aumentou a praticidade e a satisfação dos usuários no planejamento de seus passeios.
Eficiência Operacional: A solução reduziu significativamente o tempo total necessário para planejar o roteiro, oferecendo uma abordagem automatizada e precisa.

---

Matrícula: 222.100.314  

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
