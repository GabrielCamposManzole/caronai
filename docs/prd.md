# 📄 Product Requirements Document (PRD)

**Projeto:** Caronas UTFPR
**Versão:** 0.0.0 · esqueleto — em revisão
**Última atualização:** 2026-09-16

> 🤖 Este documento é a fonte da verdade sobre o QUE o produto faz. Regras de negócio que não estiverem aqui não existem para o projeto nem para a IA.
> Tecnologia não se discute aqui: isso é assunto do `architecture.md`.

---

## 🎯 1. Visão Geral e Objetivo

**O problema:** Estudantes da UTFPR precisam organizar deslocamentos entre campus, bairros e pontos próximos, mas ainda dependem de formas improvisadas de comunicação, como grupos de WhatsApp ou mensagens isoladas. Isso gera perda de tempo, dificuldade para encontrar caronas compatíveis e pouca organização entre motoristas e passageiros.

**A solução:** A aplicação será uma plataforma web para facilitar a organização de caronas entre alunos da UTFPR, permitindo que motoristas publiquem ofertas de carona, passageiros procurem trajetos compatíveis e recebam avisos relevantes quando houver correspondência de rota.

**Como saberemos que deu certo:** O sistema conseguirá conectar motorista e passageiro com base em origem, destino e caminho desejado, facilitar o acerto de carona e reduzir a fricção na busca por transporte entre campus e região.

---

## 📖 2. Glossário Ubíquo

| Termo | Significa | Não confundir com |
| :---- | :-------- | :---------------- |
| Carona | deslocamento compartilhado de um motorista com passageiros | transporte individual |
| Motorista | usuário que oferece carona | passageiro |
| Passageiro | usuário que busca carona | motorista |
| Oferta de carona | anúncio de viagem com origem, destino, vagas e horários | pedido de carona |
| Pedido de carona | solicitação de vaga para um trajeto específico | oferta de carona |
| Aviso | notificação de compatibilidade entre oferta e pedido | mensagem geral |
| Trajeto desejado | origem e destino ou caminho que o usuário pretende percorrer | qualquer rota aleatória |
| Combinação | acordo entre motorista e passageiro para a viagem | conversa fora do app |

---

## 👤 3. Atores e Permissões

| Ator | Quem é | Pode | Não pode |
| :--- | :----- | :--- | :------- |
| Estudante | usuário da plataforma | criar conta, publicar oferta, buscar carona, receber avisos, participar de combinações | alterar dados de outros usuários |
| Motorista | estudante que oferece carona | publicar viagens, definir vagas, aceitar passageiros, cancelar oferta | forçar participação sem confirmação |
| Passageiro | estudante que busca carona | criar pedido, visualizar ofertas compatíveis, receber avisos, confirmar interesse | cancelar uma carona sem ter vínculo |
| Sistema | plataforma | combinar ofertas e pedidos por compatibilidade, enviar aviso, validar campos obrigatórios | assumir decisão de carona sem confirmação |

---

## 📝 4. Escopo Funcional (User Stories)

### US01 — Informar destino/caminho desejado · Must Have · S · Status: Draft

Como passageiro, eu quero informar meu ponto de origem e o destino ou caminho desejado para que o sistema possa encontrar caronas compatíveis e me avisar quando houver uma oferta relevante.

**Critérios de aceite:**

- [ ] **Dado** que o passageiro está criando ou editando um pedido de carona, **quando** ele informa origem e destino ou rota desejada, **então** o pedido fica válido para busca.
- [ ] **Dado** que o pedido não possui destino ou caminho desejado, **quando** o usuário tenta salvar, **então** o sistema deve bloquear e pedir esse dado.
- [ ] **Dado** que o passageiro possui um pedido válido, **quando** houver uma oferta compatível, **então** o sistema deve disparar o aviso correspondente.

---

### US02 — Receber aviso de carona compatível · Must Have · S · Status: Draft

Como passageiro, eu quero receber um aviso quando houver uma oferta de carona compatível com o meu trajeto para que eu possa entrar em contato com o motorista.

**Critérios de aceite:**

- [ ] **Dado** que um passageiro cadastrou um pedido com origem e destino ou caminho desejado, **quando** uma oferta compatível for publicada ou atualizada, **então** o sistema deve enviar um aviso.
- [ ] **Dado** que a rota do passageiro não combina com a oferta, **quando** o sistema avaliar a correspondência, **então** o aviso não deve ser disparado.
- [ ] **Dado** que o aviso foi enviado, **quando** o usuário abrir a notificação, **então** ele deve conseguir visualizar os detalhes da oferta e entrar em contato com o motorista.

---

### US03 — Publicar oferta de carona · Must Have · M · Status: Draft

Como motorista, eu quero publicar uma oferta de carona com origem, destino, vagas e horário para que passageiros compatíveis possam encontrar a viagem.

**Critérios de aceite:**

- [ ] **Dado** que o motorista está autenticado, **quando** ele cria uma oferta de carona, **então** o sistema deve persistir origem, destino, horários, vagas e dados da viagem.
- [ ] **Dado** que a oferta não possui destino válido ou vagas disponíveis, **quando** o usuário tenta salvar, **então** o sistema deve impedir a criação.
- [ ] **Dado** que a oferta está cadastrada, **quando** um pedido compatível existir, **então** ela deve ser considerada no processo de aviso.

---

### US04 — Solicitar carona · Must Have · S · Status: Draft

Como passageiro, eu quero solicitar uma vaga em uma carona para que eu possa me conectar com o motorista da rota desejada.

**Critérios de aceite:**

- [ ] **Dado** que o passageiro está autenticado, **quando** ele seleciona uma oferta compatível, **então** o sistema deve permitir a solicitação de vaga.
- [ ] **Dado** que a oferta já atingiu o limite de vagas, **quando** o usuário tenta solicitar, **então** o sistema deve informar que não há vagas disponíveis.
- [ ] **Dado** que a solicitação foi enviada, **quando** o motorista visualizar, **então** ele deve poder aceitar ou recusar.

---

### US05 — Aceitar ou recusar solicitação · Must Have · S · Status: Draft

Como motorista, eu quero aceitar ou recusar a solicitação de passageiros para controlar quem vai compor a viagem.

**Critérios de aceite:**

- [ ] **Dado** que o motorista recebeu uma solicitação, **quando** ele aceita, **então** a vaga é reservada para aquele passageiro.
- [ ] **Dado** que o motorista recebeu uma solicitação, **quando** ele recusa, **então** a solicitação deve ser marcada como recusada e não deve mais aparecer como pendente.
- [ ] **Dado** que a viagem está confirmada, **quando** a vaga for preenchida, **então** o sistema deve impedir novas solicitações quando não houver vagas.

---

### US06 — Ver lista de ofertas compatíveis · Should Have · S · Status: Draft

Como passageiro, eu quero visualizar as ofertas compatíveis com o meu trajeto para que eu possa procurar carona mesmo sem depender apenas de um aviso.

**Critérios de aceite:**

- [ ] **Dado** que o passageiro criou um pedido, **quando** ele abrir a tela de busca, **então** deve ver as ofertas relevantes.
- [ ] **Dado** que não há ofertas compatíveis, **quando** o sistema buscar por correspondência, **então** deve indicar que nenhuma carona foi encontrada.
- [ ] **Dado** que a oferta está indisponível, **quando** a lista for carregada, **então** ela deve ser excluída do resultado.

---

### US07 — Cancelar oferta, pedido ou combinação · Should Have · M · Status: Draft

Como usuário, eu quero cancelar uma oferta, um pedido ou um combinado para que eu possa controlar a minha participação na carona.

**Critérios de aceite:**

- [ ] **Dado** que o motorista criou uma oferta, **quando** ele cancelar a viagem, **então** os passageiros devem ser avisados.
- [ ] **Dado** que o passageiro cancelou um pedido, **quando** a solicitação for removida, **então** o motorista deve receber a atualização.
- [ ] **Dado** que uma viagem já foi combinada, **quando** qualquer participante cancelar, **então** o sistema deve registrar a alteração.

---

### US08 — Histórico de caronas · Could Have · S · Status: Draft

Como usuário, eu quero consultar o histórico das minhas caronas para que eu possa lembrar o que já aconteceu e acompanhar o meu uso da plataforma.

**Critérios de aceite:**

- [ ] **Dado** que o usuário concluiu ou cancelou uma carona, **quando** ele acessar o histórico, **então** o sistema deve listar as viagens relacionadas.
- [ ] **Dado** que não há viagens anteriores, **quando** o usuário abrir o histórico, **então** deve aparecer uma mensagem de vazio.

---

### US09 — Avaliação de carona · Could Have · S · Status: Draft

Como usuário, eu quero avaliar a experiência depois da viagem para que eu possa contribuir para a confiança da comunidade.

**Critérios de aceite:**

- [ ] **Dado** que uma viagem foi concluída, **quando** o usuário avaliar o motorista ou passageiro, **então** a avaliação deve ser registrada.
- [ ] **Dado** que a avaliação já foi enviada, **quando** o usuário tentar repetir, **então** o sistema deve impedir duplicidade.

---

## 🛡️ 5. Regras de Negócio (Constraints)

| ID | Regra |
| :-- | :---- |
| RN01 | Todo pedido de carona deve conter origem e destino ou caminho desejado. |
| RN02 | Um aviso de carona só pode ser disparado quando há compatibilidade de rota entre demanda e oferta. |
| RN03 | O motorista pode ofertar carona somente com vagas disponíveis. |
| RN04 | O passageiro só pode solicitar vaga em uma oferta com vagas restantes. |
| RN05 | A solicitação precisa ser confirmada pelo motorista para transformar-se em combinação válida. |
| RN06 | A combinação só é válida quando houver confirmação explícita entre as partes. |
| RN07 | A plataforma deve informar ao usuário quando não houver caronas compatíveis para o seu trajeto. |
| RN08 | A presença de origem e destino ou caminho desejado é obrigatória para que o pedido seja considerado completo. |

---

## 🚫 6. Fora de Escopo (Non-goals)

> O que o produto deliberadamente não faz neste semestre.

- pagamento de gasolina no app;
- localização em tempo real por mapa;
- chat de voz ou vídeo;
- integração com autenticação oficial da UTFPR no MVP;
- garantia de carona em tempo real sem confirmação;
- mecanismo de avaliação em profundidade e reputação avançada.

---

## ⚙️ 7. Requisitos Não Funcionais (Qualidade)

- A aplicação deve ser responsiva e adequada a uso em mobile.
- A experiência deve priorizar simplicidade e rapidez na busca por caronas.
- As regras de negócio devem ser claras e válidas tanto para motorista quanto para passageiro.
- O sistema deve permitir que o usuário entenda o estado da carona em cada momento: disponível, solicitado, recusado, confirmado ou cancelado.
- O fluxo de avisos deve ser confiável e não depender de dados incompletos.

---

## 🛠️ 8. Histórico

| Data | Versão | O que mudou |
| :--- | :----- | :---------- |
| 2026-09-16 | 1.0.0 | Ajuste do PRD para incluir destino/caminho desejado como Must Have e reforçar dependência da lógica de aviso |