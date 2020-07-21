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
ms.openlocfilehash: 0495e3d3b4ec835f33254152874b21f5f989808b
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553207"
---
# <a name="mssqlserver_802"></a>MSSQLSERVER_802
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
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
  
2.  Iniziare a raccogliere i dati dei contatori di Performance Monitor per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **: Gestione buffer**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **: Memory Manager**.  
  
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
  
  
