# Regras da Agenda — Suellen Braz

## Calendário
- Tudo vai no calendário **principal** (suellenbraz.arq@gmail.com). Não usar calendários separados por categoria — foram todos migrados e abandonados porque a Alexa só lê um calendário por vez.

## Cores (colorId)
- **11** (Tomato/vermelho): corridas, provas, eventos esportivos — sempre como **dia inteiro** (allDay), com horário real na descrição.
- **5** (Banana/amarelo): saúde/remédios (remédios da Aurora — cachorra —, Venvanse, vermífugo das cachorras).
- **3** (Grape/roxo): compromissos pessoais — médico, dentista, salão, personal trainer, aniversários avulsos, favores pra amigos/família. Categoria padrão quando não é claramente trabalho.
- **7** (Peacock/azul): reuniões, trabalho, clientes, vistorias, psicóloga.
- **10** (Basil/verde): contas mensais, pagamentos, boletos.

## Lembretes
- Todo evento novo leva **dois lembretes popup: 60 min e 30 min antes** (padrão desde que ela pediu pra parar de perder compromissos por notificação silenciosa no celular).
- Eventos de "abertura de pré-venda/inscrição" (maratonas, sorteios): lembretes mais curtos (15 min e 5 min), pra garantir que ela esteja na fila de compra no instante exato.
- Reminders do telefone (fora do meu controle): ela precisa deixar o Google Agenda como "Alertas" (não "Notificações") no app, tirar o celular do silencioso e liberar o app no Não Perturbe — isso eu só posso orientar, não configurar.

## Contas mensais
- **Nunca** colocar valor em R$ no título ou na descrição de contas/boletos — só o nome da conta e dado relevante (ex. unidade consumidora da Cemig).
- Padrão de horário: 08:00–08:05 (bloco de 5 min, só pra servir de lembrete visual).

## Eventos de dia inteiro (corridas, shows, aniversários)
- Ficam no topo da agenda (allDay = true), não como horário marcado — mesmo quando há um horário real (show às 20h, largada às 19h, etc.). O horário vai na descrição.
- Aniversários: evento allDay anual (RRULE FREQ=YEARLY).

## Séries recorrentes — como editar
- Pra editar a **série toda** (nome, cor, horário): usar `update_event` com o `eventId` igual ao `recurringEventId` (o "mestre").
- Pra editar **só uma ocorrência**: usar o eventId específico da instância, formato `<masterId>_<timestampUTC>Z` (nunca o id do mestre nesse caso).
- Pra cancelar a série dali pra frente sem apagar o histórico: apagar as instâncias futuras uma a uma — a API não deixa editar o RRULE/UNTIL direto via `update_event` (não existe campo `recurrenceData` no update, só no create).
- Pra fechar de vez: `delete_event` no id do mestre cancela a série inteira, passado incluído.

## Studio Haber (salão)
- Localização padrão: "Studio Haber — Rua Acácio Alves Alvim, 2076, Marilândia, Juiz de Fora".
- Descrição padrão: "Studio Haber. Cancelamento com menos de 2h de antecedência cobra 50% do serviço. Tolerância de atraso: 10min."

## Dentista (Odonto Company)
- Localização padrão: "Odonto Company — Rua São João, 197 PV 2, Centro, Juiz de Fora - MG".
- Ela troca de dentista às vezes (Dra. Ana Laura, Dra. Ariane) — manter o nome da profissional no título.

## Como interpretar as mensagens dela
- Mensagens chegam como voz-pra-texto, cheias de autocorreção ("é... não, na verdade..."). Sempre usar o **último valor dito**, não o primeiro.
- Quando um nome, data, horário ou "do que se trata" fica ambíguo ou incompleto, **perguntar antes de criar o evento** — não adivinhar em cima de compromissos reais. Uma pergunta objetiva (AskUserQuestion com opções, ou texto direto) é melhor que supor errado.
- Fotos/PDFs/prints de WhatsApp de confirmação de agendamento (Studio Haber, clínicas, Odonto Company, Unimed, convênios) viram evento direto, sem precisar perguntar — os dados já vêm completos.
- Mensagens que são só endereço/contato sem data viram pergunta ("isso é pra marcar o quê, que dia?"), não viram evento.
- Sempre conferir o estado atual do calendário antes de assumir que algo já existe, já foi cancelado, ou que um horário bate — não confiar em dumps antigos sem checar de novo (já aconteceu de uma série "cancelada" aparecer num dump desatualizado).
- Ela acompanha amigos/família em consultas (ex. Camila, Sidney) — esses eventos entram como compromisso dela também, com nota de quem é o paciente de verdade.

## Limitações conhecidas
- Não tenho acesso a Telegram, WhatsApp (enviar mensagens) nem a um "bot" separado — só ao Google Agenda dela via essas ferramentas. Lembretes de terceiros (ex. Sidney) só dá pra fazer adicionando o e-mail da pessoa como convidado do evento.
