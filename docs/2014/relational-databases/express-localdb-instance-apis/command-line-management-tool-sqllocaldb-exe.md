---
title: 'Strumento di gestione da riga di comando: SqlLocalDB.exe | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_location:
- sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 58ea983555fdcb4bb177813db88d40f4bcc59c0e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52765473"
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>Strumento di gestione da riga di comando: SqlLocalDB.exe
  SqlLocalDB.exe è uno strumento semplice che consente all'utente di gestire facilmente le istanze del database locale dalla riga di comando. Viene implementato come un semplice wrapper dell'API dell'istanza del database locale. Come in molti strumenti SQL Server simili, ad esempio SQLCMD, i parametri vengono passati a SqlLocalDB come argomenti della riga di comando e l'output viene inviato alla console.  
  
 SqlLocalDB consente agli sviluppatori di utilizzare il database locale senza la necessità di scrivere codice per chiamare l'API o dipendere da altri strumenti per effettuare tale operazione.  
  
## <a name="sqllocaldb-options"></a>Opzioni di SqlLocalDB  
 SqlLocalDB supporta le opzioni seguenti.  
  
|Opzione|Descrizione|  
|------------|------------------|  
|`-?`|Viene stampato il testo della Guida.|  
|`create&#124;c "instance name" [version-number] [-s]`|Viene creata una nuova istanza del database locale con una versione e un nome specificati.<br /><br /> Se il parametro [version-number] viene omesso, il valore predefinito è la versione della build di SqlLocalDB.<br /><br /> Tramite il parametro -s viene avviata la nuova istanza del database locale dopo la relativa creazione.|  
|`delete&#124;d "instance name"`|Viene eliminata l'istanza del database locale con il nome specificato.|  
|`start&#124;s "instance name"`|Viene avviata l'istanza del database locale con il nome specificato.|  
|`stop&#124;p "instance name" [-i&#124;-k]`|Viene arrestata l'istanza del database locale con il nome specificato, al termine dell'esecuzione delle query correnti.<br /><br /> Tramite il parametro -i viene richiesto l'arresto dell'istanza del database locale con l'opzione NOWAIT.<br /><br /> Tramite il parametro -k viene terminato il processo dell'istanza del database locale senza contattare quest'ultimo.|  
|`share&#124;h ["owner SID or account"] "private name" "shared name"`|Viene condivisa l'istanza privata specificata tramite il nome condiviso indicato. Se viene omesso il SID dell'utente o il nome dell'account, il valore predefinito è l'utente corrente.|  
|`unshare&#124;u "shared name"`|Viene rimossa la condivisione dell'istanza del database locale condivisa specificata.|  
|`info&#124;i`|Vengono elencate tutte le istanze del database locale esistenti di proprietà dell'utente corrente nonché tutte le istanze del database locale condivise.|  
|`info&#124;i "instance name"`|Vengono stampate le informazioni sull'istanza specificata del database locale.|  
|`versions&#124;v`|Vengono elencate tutte le versioni del database locale installate nel computer.|  
|||  
|`trace&#124;t on&#124;off`|Viene abilitata o disabilitata la traccia.|  
  
 Gli spazi in SqlLocalDB vengono considerati come delimitatori. È necessario racchiudere tra virgolette i nomi delle istanze contenenti spazi e caratteri speciali. Ad esempio:  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
