---
id: avail-consensus
title: Консенсус Avail
sidebar_label: Consensus
description: Узнайте о механизме консенсуса Avail
keywords:
  - docs
  - polygon
  - avail
  - consensus
  - proof of stake
  - nominated proof of stake
  - pos
  - npos
image: https://wiki.polygon.technology/img/thumbnail/polygon-avail.png
slug: avail-consensus
---

# Консенсус Avail {#avail-s-consensus}

## Комитеты по доступности данных {#data-availability-committees}

До настоящего времени подход к ведению решений DA обычно осуществлялся через Комитет по обеспечению доступности данных. Комиссия отвечает за вывод подписей в основную цепочку и подтверждение наличия данных вне цепочки. Комиссия должна обеспечить готовность данных.

Благодаря DAC, решения масштабирования полагаются на DAC для достижения Validium. Проблема с DACs заключается в том, что наличие данных становится надежным сервисом для небольшой группы членов комитета, которые отвечают за хранение данных и достоверную отчетность.

Avail — это не DAC, а настоящая блокчейн-сеть, имеющая свой механизм консенсуса, и имеет свой собственный набор узлов валидатора и производителей блоков.

## Доказательство доли владения (Proof of Stake) {#proof-of-stake}

:::caution Текущие валидаторы

С первоначальным запуском тестовой сети Avail валидаторы будут
будут управляться и поддерживаться внутри Polygon.

:::

Традиционные системы стейка требуют от авторов блока создания холдинга (стейк) в цепочке для создания блоков в отличие от вычислительных ресурсов (работы).

Продукты Polygon используют PoS (доказательство стейка) или модификацию PoS. Обычно валидаторы в традиционных системах PoS, которые имеют наибольший пакет, имеют наибольшее влияние и контроль сети.

Системы, в которых много поддерживающих сети, как правило, формируют пулы вне цепочки, чтобы максимизировать прирост капитала за счет уменьшения диспропорции вознаграждения. Этот вызов централизации облегчает, когда пулы включены в цепочку, что позволяет владельцам токенов возвращать поддерживающих сети, которые они чувствуют наилучшим образом представлять их и интересы сети. Это также распределяет концентрацию полномочий валидатора, предполагая, что будут созданы механизмы правильного голосования и выборов, поскольку общий пакет акций в сети распределяется как взаимоотношения от одного к многим или от многих к другому, вместо того чтобы полагаться только на взаимоотношения "от одного к другому", где доверие поставляется в валидаторы "самых высоких staked"

Это изменение доказательства пакета может быть be посредством делегирования или номинации, обычно называемого DPoS (делегировано доказательство стей) или NPoS (назначенное доказательство стей). Решения Polygon адаптировали эти расширенные механизмы, включая Polygon Avail.

Avail использует NPoS с модификацией проверки блоков. Соответствующие субъекты по-прежнему являются валидаторами и номинантами.

Легкие клиенты также могут способствовать доступности данных в Avail. Консенсус Avail's требует, чтобы две трети плюс 1 валидаторов достигли консенсуса по действительности.

## Номинаторы {#nominators}

Номинаторы могут выбрать обратно набор валидаторов Avail с их пакетом. Номинаторы будут выдвигать тех валидаторов, которые, по их мнению, будут эффективно обеспечивать наличие данных.

## Разница между DPoS и NPoS {#difference-between-dpos-and-npos}

По номинальной стоимости, делегирование и номинация, кажется, похожи на те же действия, особенно с точки зрения заядлого стейкера. Однако различия лежат в базовых механизмах консенсуса и как происходит выбор валидатора.

В DPoS система избирательных округов определяет фиксированное число валидаторов для обеспечения сети. Делегаты могут делегировать свой пакет против валидаторов сети кандидатов, используя его в качестве права голоса обратно делегатов. Делегаты часто поддерживают валидаторов на самом высоком staked, поскольку у валидаторов с более высокими стейками есть более высокий шанс на выбор. Делегаты, набравшие наибольшее число голосов, становятся валидаторами сети, могут проверять транзакции. Используя свой пакет в качестве права голоса, в Avail, они не подлежат воздействию посредством power, если их избранный валидатор ведет себя злонамеренно. В других системах DPoS delegators могут быть подвергнуты slashing.

В NPoS delegators превращаются в номинантов и используют свой пакет акций аналогично для того, чтобы выдвинуть потенциальных валидаторов для защиты сети. Stake заблокирован в цепочке, и в отличие от DPoS, номинанты подлежат slashing на основе потенциального вредоносного поведения их номинаций. В этом отношении NPoS является более активным механизмом стейкинга, а не стейкингом, который «устанавливается и забудет», поскольку номинанты ищут хорошо вести себя и устойчивых валидаторов. Это также поощряет валидаторов создавать надежные операции валидатора для привлечения и поддержания номинаций.