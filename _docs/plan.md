# Ferinos — Escopo Consolidado do Produto

## 1. Visão

Ferinos é um aplicativo mobile para organizar grupos recorrentes de futebol amador.

Plataformas:
- Android
- iPhone

Idioma inicial:
- Português (Brasil)

### Objetivo principal

Resolver o ciclo:

**Grupo → Próximo ferino → Confirmações → Lista de espera → Times → Jogo → Resultado → Estatísticas → Histórico**

O grupo é recorrente, mas cada rodada pode ser alterada ou cancelada individualmente.

---

## 2. Decisão estratégica: WhatsApp-first

O WhatsApp será o principal canal para a ação mais simples e frequente: **confirmar presença**.

### O que entra

- Pergunta individual automática no WhatsApp.
- Botões **VOU** e **NÃO VOU**.
- Jogador pode responder sem abrir o aplicativo.
- Resposta atualiza o Ferinos imediatamente.
- Lembretes individuais pelo WhatsApp.
- Administrador pode compartilhar manualmente conteúdos no grupo.

### O que foi abandonado

- Botão VOU dentro de grupo WhatsApp existente.
- Ferinos publicando automaticamente em grupo WhatsApp existente.
- Automação não oficial via WhatsApp Web.
- Transformar o Ferinos em bot dentro de grupos comuns.

### Filosofia

> **WhatsApp para confirmar. Ferinos para organizar e acompanhar.**

---

# 3. Grupos

## Configuração

Cada grupo possui:

- nome;
- logo opcional;
- dia da semana;
- horário padrão;
- prazo de confirmação;
- local padrão;
- duração esperada;
- limite opcional de jogadores por rodada.

O número de jogadores não é fixo.

## Rodadas

Cada rodada pode:

- ser antecipada;
- ser adiada;
- ser cancelada;
- ter horário alterado;
- ter local alterado.

Alterações de data/horário notificam os jogadores.

O local padrão pode ser sobrescrito por uma rodada específica.

Local:
- nome;
- endereço;
- link do Google Maps.

Rodada cancelada permanece no histórico, mas não entra nas estatísticas.

---

# 4. Entrada e membros

Qualquer usuário registrado pode criar um grupo.

O administrador gera um link de convite.

Ao abrir o link, o usuário cria/confirma seu perfil e entra no grupo.

Administradores podem:

- remover;
- bloquear;
- readmitir;
- alterar permissões.

Ao ser removido:
- histórico permanece;
- não participa das futuras estatísticas do grupo.

Se for convidado novamente:
- recupera o mesmo perfil;
- mantém histórico;
- depende de aprovação do administrador.

O jogador pode sair voluntariamente.

Para voltar depois de sair, precisa ser adicionado por um administrador.

### Limites

Cada usuário pode:
- participar de até 7 grupos;
- criar até 7 grupos.

---

# 5. Administradores

Qualquer jogador pode se tornar administrador mediante aprovação do criador.

Permissões são configuráveis individualmente.

O criador mantém o maior nível de controle.

Administrador pode:
- alterar configurações;
- administrar membros;
- abrir/fechar confirmações;
- adicionar jogadores;
- remover/bloquear jogadores;
- montar times;
- corrigir partidas;
- compartilhar informações.

Remoção exige confirmação.

Bloqueio não exige motivo.

---

# 6. Cadastro e conta

Login/cadastro:

**Telefone → código via WhatsApp → perfil**

Sem senha.

Em novo aparelho:
- mesmo número;
- nova validação via WhatsApp.

Troca de número:
- requer aprovação de administrador.

Exclusão de conta:
- histórico permanece;
- dados pessoais são anonimizados.

---

# 7. Perfil

Campos:

- nome;
- apelido;
- telefone;
- posição principal;
- número da camisa.

Posição:
- Goleiro;
- Defensor;
- Meia;
- Atacante.

Exatamente uma posição.

Não haverá foto de perfil no MVP.

Número da camisa:
- escolhido pelo jogador;
- pode ser alterado pelo administrador;
- único dentro de cada grupo;
- pode variar entre grupos.

---

# 8. Confirmação

O jogador responde somente:

- **Vou**
- **Não vou**

“Vou” significa presença confirmada.

Depois do prazo:
- jogador comum não altera;
- administrador pode confirmar/adicionar.

Categorias:
- Confirmados;
- Não vão;
- Não responderam.

---

# 9. Fluxo WhatsApp

## Etapa 1 — administrador abre a confirmação

O sistema conhece:
- data;
- horário;
- local;
- prazo;
- jogadores.

## Etapa 2 — administrador compartilha no grupo

Exemplo:

> ⚽ FERINO — QUINTA, 20H  
> 📍 Arena X  
>  
> Confirme sua presença:  
> [link do Ferinos]

O compartilhamento no grupo é manual.

## Etapa 3 — Ferinos pergunta individualmente

No horário configurado:

> ⚽ Ferino de quinta, 20h  
> 📍 Arena X  
>  
> Você vai jogar?  
>  
> **[⚽ VOU] [❌ NÃO VOU]**

O jogador responde sem abrir o app.

## Etapa 4 — backend

Exemplo:

`João → VOU`

O backend:
- identifica jogador;
- identifica grupo;
- identifica rodada;
- registra resposta;
- atualiza a lista;
- atualiza a lista de espera, se necessário.

O app reflete a alteração imediatamente.

Pode haver confirmação individual:

> ✅ Confirmado!  
> Te esperamos quinta às 20h.

---

# 10. Lembretes

Push:
- 24h antes do prazo;
- 2h antes do prazo.

WhatsApp:
- pergunta inicial;
- lembretes aos não respondentes, conforme regras e permissões da plataforma.

---

# 11. Lista de espera

Se a rodada tiver limite:

- novos jogadores entram na espera;
- cancelamento libera vaga;
- primeiro da fila é promovido;
- jogador promovido recebe prazo;
- se não responder, próximo é promovido.

Cancelamento libera a vaga mesmo depois do prazo.

---

# 12. Cancelamentos

Registrar:
- confirmação;
- cancelamento;
- timestamp;
- tempo restante até o jogo.

“In cima da hora”:
**menos de 2 horas antes do jogo.**

Categorias estatísticas:
- confirmou e foi;
- confirmou e não foi;
- confirmou e cancelou;
- confirmou e cancelou em cima da hora;
- não respondeu;
- não confirmou e foi adicionado/confirmado pelo ADM.

---

# 13. Presença

Administrador pode marcar **Não compareceu**.

Diferenciar:
- confirmou e foi;
- confirmou e não foi;
- não confirmou e foi adicionado pelo ADM;
- não respondeu;
- confirmou e cancelou;
- confirmou e cancelou em cima da hora.

---

# 14. Home

A Home é focada no próximo ferino.

Mostrar:
- data;
- horário;
- countdown;
- local;
- status da confirmação;
- Vou;
- Não Vou;
- quantidade de confirmados;
- lista de espera.

---

# 15. Times

Montagem manual.

Administrador atribui jogadores individualmente.

Exemplo:
- Time Azul;
- Time Vermelho.

Não haverá:
- balanceamento automático;
- titulares/reservas.

Times podem ter tamanhos diferentes.

Administrador pode alterar a atribuição depois do jogo.

As estatísticas acompanham a atribuição final.

---

# 16. Avulsos

Administrador pode adicionar jogador avulso para uma rodada.

Dados:
- nome;
- posição.

Avulso:
- possui estatísticas da partida;
- não participa dos rankings individuais mensal/anual.

---

# 17. Escalação

Depois do prazo de confirmação:

- administrador monta os times;
- jogadores visualizam a escalação;
- escalação pode ser compartilhada no WhatsApp.

---

# 18. Jogo

Tela:
- placar grande;
- times;
- gols;
- assistências.

Botão rápido:
**Gol**

Gol em tempo real:
- autor obrigatório.

Gol registrado depois:
- autor pode ser “não informado”.

Assistência:
- opcional.

Gol contra:
- jogador responsável obrigatório;
- sem assistência.

---

# 19. Correções

Administrador pode corrigir:
- times;
- placar;
- gols;
- assistências.

As estatísticas são recalculadas.

Auditoria:
- quem alterou;
- o que alterou;
- valor anterior;
- valor final.

Histórico de correções somente para administradores.

---

# 20. Cronômetro

Começa automaticamente no horário programado.

É apenas informativo.

Não exige que o administrador pare.

Duração esperada fica configurada no grupo.

---

# 21. Resultado

- Vitória;
- Empate;
- Derrota.

Empates são permitidos.

Sem disputa por pênaltis no MVP.

---

# 22. Estatísticas

Registrar:
- gols;
- assistências;
- vitórias;
- derrotas;
- gols contra;
- faltas;
- presença;
- cancelamentos;
- ausências.

W/D/L individual só conta quando:
1. confirmou;
2. compareceu;
3. foi atribuído a um time.

Gols/assistências só contam quando participou e foi atribuído a um time.

---

# 23. Rankings

Filtros:
- mês;
- ano.

Prêmios/rankings:
- Artilheiro;
- Líder de assistências;
- Mais vitórias;
- Mais derrotas;
- Defensor com mais gols;
- Meia com mais gols;
- Atacante com mais gols;
- Goleiro com mais vitórias;
- Time/cor com mais vitórias;
- Mais gols contra;
- Mais faltas;
- Mais cancelamentos após prazo;
- Maior percentual de presença.

Empates permanecem empatados.

Sem desempate artificial.

---

# 24. Histórico

Cada partida guarda:
- data;
- local;
- times;
- jogadores;
- placar;
- gols;
- assistências;
- resultado;
- estatísticas.

Todos os jogadores do grupo podem visualizar partidas antigas.

Partidas nunca são apagadas.

Podem ser:
- corrigidas;
- marcadas como canceladas.

Canceladas permanecem no histórico, mas não entram nas estatísticas.

---

# 25. Compartilhamento no WhatsApp

O Ferinos gera mensagens prontas para compartilhamento.

Exemplo:

> ⚽ FERINO — QUINTA 20H  
> 📍 Arena X  
>  
> 🟢 Confirmados: 12  
> 🔴 Não vão: 3  
> ⚪ Não responderam: 5  
>  
> **Confirmados**  
> João  
> Pedro  
> Lucas  
> Rafael

O administrador decide quando compartilhar.

## Resultado

Resultado e estatísticas finais não são enviados automaticamente ao grupo.

O administrador decide se quer compartilhar.

---

# 26. Notificações

Push para:
- confirmação aberta;
- prazo próximo;
- prazo encerrado;
- times definidos;
- jogo hoje;
- alteração de horário;
- alteração de local;
- rodada cancelada;
- promoção da lista de espera;
- mudanças relevantes.

---

# 27. Privacidade

Sem configurações individuais de visibilidade no MVP.

Outros jogadores veem:
- nome;
- apelido;
- posição;
- número da camisa.

Telefone:
- jogador;
- administradores autorizados.

---

# 28. Tema

- claro;
- escuro;
- automático.

---

# 29. Fora do MVP

Não implementar inicialmente:

- chat interno;
- feed social;
- comentários;
- curtidas;
- ranking global;
- avaliação de jogadores;
- balanceamento automático;
- cartões;
- vídeos;
- fotos;
- pagamentos;
- estatísticas avançadas;
- exportação Excel/CSV/PDF;
- versão web;
- múltiplos idiomas;
- publicação automática em grupos WhatsApp existentes;
- botão VOU dentro de grupos WhatsApp existentes.

---

# 30. Arquitetura conceitual

## Aplicativo

Responsável por:
- grupos;
- jogadores;
- confirmações;
- lista de espera;
- times;
- partidas;
- estatísticas;
- rankings;
- histórico;
- administração.

## Backend

Responsável por:
- autenticação;
- regras de negócio;
- recorrência;
- confirmações;
- lista de espera;
- estatísticas;
- auditoria;
- notificações;
- integração WhatsApp.

## WhatsApp Business Platform

Responsável principalmente por:
- mensagens individuais;
- perguntas de confirmação;
- botões VOU/NÃO VOU;
- lembretes;
- respostas rápidas.

## Grupo WhatsApp existente

Continua independente.

O administrador compartilha manualmente os conteúdos gerados pelo Ferinos.

---

# 31. Diferencial

O principal diferencial:

> **O jogador não precisa abrir o aplicativo para confirmar que vai jogar.**

O WhatsApp vira a porta de entrada rápida.

O Ferinos fica responsável pela experiência completa.

---

# 32. Spike técnico obrigatório do WhatsApp

Antes da implementação completa:

1. Meta Business;
2. WhatsApp Business Account;
3. número oficial;
4. Cloud API;
5. envio individual;
6. botões VOU/NÃO VOU;
7. webhook;
8. identificação do jogador;
9. associação à rodada;
10. confirmação;
11. lembretes;
12. opt-in;
13. templates;
14. janela de atendimento;
15. custos;
16. múltiplos jogadores simultâneos.

Critério de sucesso:

**Jogador recebe pergunta → toca VOU/NÃO VOU → backend identifica jogador e rodada → presença é atualizada imediatamente no Ferinos.**

---

# 33. Decisões fechadas sobre WhatsApp

### Confirmado

- WhatsApp faz parte do MVP.
- Confirmação individual automática faz parte do MVP.
- VOU/NÃO VOU são o objetivo.
- Jogador não precisa abrir o app.
- Lembretes individuais são suportados pelo conceito.
- Grupo existente continua sendo usado normalmente.
- Compartilhamento para grupo é manual.
- Resultado só é compartilhado se o administrador quiser.

### Abandonado

- Botão VOU dentro do grupo existente.
- Publicação automática em grupo existente.
- Automação não oficial.
- Bot controlando conta pessoal.

---

# 34. MVP resumido

## Conta
- telefone;
- código WhatsApp;
- perfil.

## Grupo
- criação;
- convite;
- administradores;
- permissões;
- recorrência;
- configurações.

## Rodada
- data;
- horário;
- local;
- confirmação;
- prazo;
- limite;
- lista de espera.

## WhatsApp
- pergunta individual;
- VOU;
- NÃO VOU;
- lembretes;
- confirmação sem abrir app.

## Times
- montagem manual;
- cores/nomes;
- escalação.

## Jogo
- placar;
- gols;
- assistências;
- gols contra;
- resultado.

## Estatísticas
- presença;
- gols;
- assistências;
- vitórias/derrotas;
- rankings;
- cancelamentos;
- faltas.

## Histórico
- partidas;
- resultados;
- escalações;
- eventos;
- auditoria.

## Compartilhamento
- convite;
- lista;
- escalação;
- resultado opcional.

---

# 35. Fluxo principal

```text
ADMIN CRIA GRUPO
        ↓
CONFIGURA RECORRÊNCIA
        ↓
PRÓXIMA RODADA
        ↓
CONFIRMAÇÃO ABERTA
        ↓
ADM COMPARTILHA LINK NO GRUPO
        ↓
FERINOS ENVIA PERGUNTA INDIVIDUAL
        ↓
   ┌───────────────┐
   │               │
  VOU          NÃO VOU
   │               │
   └───────┬───────┘
           ↓
     BACKEND ATUALIZA
           ↓
     LISTA EM TEMPO REAL
           ↓
      PRAZO ENCERRADO
           ↓
      ADM MONTA TIMES
           ↓
        ESCALAÇÃO
           ↓
           JOGO
           ↓
    GOLS / ASSISTÊNCIAS
           ↓
        RESULTADO
           ↓
    ESTATÍSTICAS
           ↓
        HISTÓRICO
           ↓
ADM DECIDE SE COMPARTILHA
       NO WHATSAPP
```

---

# 36. Princípio de produto

O Ferinos não deve tentar substituir o WhatsApp.

Ele complementa o comportamento que os grupos já possuem.

> **O grupo continua no WhatsApp.**
>
> **A confirmação acontece no WhatsApp.**
>
> **A organização acontece no Ferinos.**
>
> **As estatísticas ficam no Ferinos.**
>
> **O administrador decide o que volta para o WhatsApp.**
