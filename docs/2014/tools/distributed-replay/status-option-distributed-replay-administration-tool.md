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
ms.openlocfilehash: 42e06144f35ab2db8f124dddff74fb836b6d9c4c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150362"
---
# <a name="status-option-distributed-replay-administration-tool"></a>Opzione status (strumento di amministrazione Distributed Replay)
  Lo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] strumento di amministrazione riesecuzione distribuita `DReplay.exe`,, è uno strumento da riga di comando che è possibile utilizzare per comunicare con il controller di riesecuzione distribuita. Questo argomento descrive l'opzione della riga di comando **status** e la sintassi corrispondente.  
  
 L'opzione **status** esegue query sul controller e visualizza lo stato corrente.  
  
 ![Icona di collegamento all'argomento](../../database-engine/media/topic-link.gif "Icona di collegamento a un argomento") Per ulteriori informazioni sulle convenzioni di sintassi utilizzate con la sintassi dello strumento di amministrazione, vedere [convenzioni della sintassi Transact-sql &#40;&#41;Transact-SQL ](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
dreplay status [-mcontroller] [-fstatus_interval]  
```  
  
#### <a name="parameters"></a>Parametri  
 **-m** *controller*  
 Specifica il nome computer del controller. È possibile utilizzare "`localhost`" o "`.`" per fare riferimento al computer locale.  
  
 Se il parametro **-m** non è specificato, viene usato il computer locale.  
  
 **-f** *status_interval*  
 Specifica la frequenza in secondi in base alla quale visualizzare lo stato.  
  
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
 [SQL Server Riesecuzione distribuita](sql-server-distributed-replay.md)   
 [Debugger Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
