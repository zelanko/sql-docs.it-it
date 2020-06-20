---
title: MSSQLSERVER_802 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 802 (Database Engine error)
ms.assetid: 5892ed24-4dcb-4bf9-a8a4-a7ca898832d5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a599b6b4eb5f980096824ccd655ef9bb33448f59
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85031893"
---
# <a name="mssqlserver_802"></a>MSSQLSERVER_802
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|802|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|NO_BUFS|  
|Testo del messaggio|Memoria insufficiente nel pool di buffer.|  
  
## <a name="explanation"></a>Spiegazione  
 L'errore è causato dal fatto che il pool di buffer è pieno e non è possibile aumentarne le dimensioni.  
  
## <a name="user-action"></a>Azione dell'utente  
 Nell'elenco seguente viene illustrata la procedura generale per la risoluzione degli errori di memoria:  
  
1.  Verificare se altre applicazioni o servizi utilizzano la memoria nel server specificato. Riconfigurare le applicazioni o i servizi meno critici per utilizzare una quantità di memoria inferiore.  
  
2.  Iniziare a raccogliere i dati dei contatori di Performance Monitor per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **: Gestione buffer** e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **: Gestione memoria**.  
  
3.  Verificare i seguenti parametri di configurazione della memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
     Valutare eventuali impostazioni non comuni e correggerle se necessario. Considerare i requisiti di memoria aggiuntivi per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le impostazioni predefinite sono elencate nell'argomento "Impostazione delle opzioni di configurazione del server" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Osservare l'output di DBCC MEMORYSTATUS e il modo in cui viene modificato quando vengono visualizzati questi messaggi di errore.  
  
5.  Verificare il carico di lavoro (numero di sessioni simultanee, query attualmente in esecuzione).  
  
 Per aumentare la quantità di memoria disponibile per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], effettuare le operazioni seguenti:  
  
-   Se le risorse vengono utilizzate da altre applicazioni oltre a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], provare ad arrestare tali applicazioni o a eseguirle in un server distinto.  
  
-   Se è stata configurata l'opzione **max server memory,** , aumentarne il valore impostato.  
  
 Eseguire i comandi DBCC seguenti per liberare diverse cache in memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 Se il problema persiste, sarà necessario analizzarlo in modo più dettagliato e cercare di ridurre il carico di lavoro.  
  
  
