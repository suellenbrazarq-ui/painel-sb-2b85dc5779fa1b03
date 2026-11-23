# Regras da Agenda — Suellen Braz

## Calendário
- Tudo vai no calendário **principal** (suellenbraz.arq@gmail.com). Não usar calendários separados por categoria — foram todos migrados e abandonados porque a Alexa só lê um calendário por vez.

## Cores (colorId)
- **11** (Tomato/vermelho): corridas, provas, eventos esportivos — sempre como **dia inteiro** (allDay), com horário real na descrição.
- **5** (Banana/amarelo): saúde/remédios (ex.: remédios da Aurora, Venvanse).
- **3** (Grape/roxo): compromissos pessoais — médico, dentista, salão, personal trainer, aniversários, etc. (categoria padrão quando não é claramente trabalho).
- **7** (Peacock/azul): reuniões, trabalho, clientes, psicóloga.
- **10** (Basil/verde): contas mensais, pagamentos, boletos.

## Lembretes
- Todo evento novo leva **dois lembretes popup: 60 min e 30 min antes** (padrão desde que ela pediu pra parar de perder compromissos por notificação silenciosa).
- Eventos de "abertura de pré-venda/inscrição" (ex. maratonas): lembretes mais curtos (15 min e 5 min), pra garantir que ela esteja na fila de compra no instante exato.

## Contas mensais
- **Nunca** colocar valor em R$ no título ou na descrição de contas/boletos — só o nome da conta e, se relevante, dados tipo unidade consumidora.

## Eventos de dia inteiro (corridas, shows, aniversários)
- Ficam no topo da agenda (allDay = true), não como horário marcado — mesmo quando há um horário real (ex. show às 20h, largada às 19h). O horário vai na descrição.
- Aniversários: evento allDay anual (RRULE FREQ=YEARLY).

## Séries recorrentes
- Pra editar a **série toda**, usar o `eventId` igual ao `recurringEventId` (o "mestre").
- Pra editar **só uma ocorrência**, usar o eventId específico da instância (formato `<masterId>_<timestampUTC>Z`), nunca o id do mestre.
- Pra cancelar a série daquele ponto em diante sem apagar o histórico: apagar as instâncias futuras uma a uma (a API não permite editar o RRULE/UNTIL direto via update).

## Studio Haber (salão)
- Sempre incluir localização: "Studio Haber — Rua Acácio Alves Alvim, 2076, Marilândia, Juiz de Fora".
- Descrição padrão: "Studio Haber. Cancelamento com menos de 2h de antecedência cobra 50% do serviço. Tolerância de atraso: 10min."

## Dentista (Odonto Company)
- Localização padrão: "Odonto Company — Rua São João, 197 PV 2, Centro, Juiz de Fora - MG".

## Como interpretar as mensagens dela
- Mensagens chegam como voz-para-texto, cheias de autocorreção ("é... não, na verdade..."). Sempre usar o **último valor dito**, não o primeiro.
- Quando um nome, data ou "do que se trata" fica ambíguo ou incompleto, **perguntar antes de criar o evento** — não adivinhar em cima de compromissos reais.
- Fotos/PDFs de confirmação de agendamento (Studio Haber, clínicas, WhatsApp) devem virar evento direto, sem precisar perguntar.
- Sempre conferir o estado atual do calendário antes de assumir que algo já existe ou não (dumps antigos podem estar desatualizados).
