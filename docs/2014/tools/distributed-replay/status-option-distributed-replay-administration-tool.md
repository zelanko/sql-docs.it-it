---
title: Opzione Stato (strumento di amministrazione Riesecuzione distribuita) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e56a5229f0f26dfe701a425653b3d7f5a4ece842
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78171940"
---
# <a name="status-option-distributed-replay-administration-tool"></a>Opzione status (strumento di amministrazione Distributed Replay)
  Lo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] strumento di amministrazione riesecuzione distribuita `DReplay.exe`,, è uno strumento da riga di comando che è possibile utilizzare per comunicare con il controller di riesecuzione distribuita. Questo argomento descrive l'opzione della riga di comando **status** e la sintassi corrispondente.

 L'opzione **status** esegue query sul controller e visualizza lo stato corrente.

 ![Icona di collegamento all'argomento](../../database-engine/media/topic-link.gif "Icona di collegamento a un argomento") Per altre informazioni sulle convenzioni relative alla sintassi dello strumento di amministrazione, vedere [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql).

## <a name="syntax"></a>Sintassi

```

dreplay status [-mcontroller] [-fstatus_interval]
```

#### <a name="parameters"></a>Parametri
 **-m** *controller* specifica il nome computer del controller. È possibile utilizzare "`localhost`" o "`.`" per fare riferimento al computer locale.

 Se il parametro **-m** non è specificato, viene usato il computer locale.

 **-f** *status_interval* specifica la frequenza (in secondi) in cui visualizzare lo stato.

 Se il parametro **-f** non è specificato, l'intervallo predefinito è 30 secondi.

## <a name="examples"></a>Esempi
 Nell'esempio seguente lo stato corrente viene visualizzato ogni 60 secondi. Il valore `localhost` indica che il servizio controller viene eseguito nello stesso computer dello strumento di amministrazione.

```
dreplay status -m localhost -f 60
```

## <a name="permissions"></a>Autorizzazioni
 È necessario eseguire lo strumento di amministrazione come utente interattivo, scegliendo tra utente locale e account utente di dominio. Per utilizzare un account utente locale, lo strumento di amministrazione e il controller devono essere eseguiti nello stesso computer.

 Per altre informazioni, vedere [Sicurezza di Riesecuzione distribuita](distributed-replay-security.md).

## <a name="see-also"></a>Vedere anche
 [SQL Server riesecuzione distribuita](sql-server-distributed-replay.md) [debugger Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)


