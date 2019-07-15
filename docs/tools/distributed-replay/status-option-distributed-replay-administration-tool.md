---
title: Opzione Stato (strumento di amministrazione Riesecuzione distribuita) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c8b3ec71769f38036e6af46e1738676a242fd607
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732563"
---
# <a name="status-option-distributed-replay-administration-tool"></a>Opzione status (strumento di amministrazione Distributed Replay)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Lo strumento di amministrazione Riesecuzione distribuita di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , **DReplay.exe**, è uno strumento da riga di comando che consente di comunicare con il controller di Riesecuzione distribuita. Questo argomento descrive l'opzione della riga di comando **status** e la sintassi corrispondente.  
  
 L'opzione **status** esegue query sul controller e visualizza lo stato corrente.  
  
 ![Icona di collegamento all'argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento all'argomento")Per altre informazioni sulle convenzioni relative alla sintassi dello strumento di amministrazione, vedere [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
dreplay status [-m controller] [-f status_interval]  
```  
  
#### <a name="parameters"></a>Parametri  
 **Controller** _-m_  
 Specifica il nome computer del controller. È possibile utilizzare "`localhost`" o "`.`" per fare riferimento al computer locale.  
  
 Se il parametro **-m** non è specificato, viene usato il computer locale.  
  
 _intervallo_stato_ **-f**  
 Specifica la frequenza in secondi in base alla quale visualizzare lo stato.  
  
 Se il parametro **-f** non è specificato, l'intervallo predefinito è 30 secondi.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente lo stato corrente viene visualizzato ogni 60 secondi. Il valore `localhost` indica che il servizio controller viene eseguito nello stesso computer dello strumento di amministrazione.  
  
```  
dreplay status -m localhost -f 60  
```  
  
## <a name="permissions"></a>Autorizzazioni  
 È necessario eseguire lo strumento di amministrazione come utente interattivo, scegliendo tra utente locale e account utente di dominio. Per utilizzare un account utente locale, lo strumento di amministrazione e il controller devono essere eseguiti nello stesso computer.  
  
 Per altre informazioni, vedere [Sicurezza di Distributed Replay](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Debugger Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
