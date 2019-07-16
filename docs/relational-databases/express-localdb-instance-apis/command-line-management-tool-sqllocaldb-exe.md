---
title: 'Strumento di gestione della riga di comando: SqlLocalDB.exe | Microsoft Docs'
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apilocation:
- sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a41daed808b51df59ba80e0113b84e46c501c9b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126952"
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>Strumento di gestione della riga di comando: SqlLocalDB.exe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SqlLocalDB.exe è uno strumento semplice che consente all'utente di gestire facilmente le istanze del database locale dalla riga di comando. Viene implementato come un semplice wrapper dell'API dell'istanza del database locale. Come in molti strumenti SQL Server simili, ad esempio SQLCMD, i parametri vengono passati a SqlLocalDB come argomenti della riga di comando e l'output viene inviato alla console.  
  
 SqlLocalDB consente agli sviluppatori di utilizzare il database locale senza la necessità di scrivere codice per chiamare l'API o dipendere da altri strumenti per effettuare tale operazione.  
  
## <a name="sqllocaldb-options"></a>Opzioni di SqlLocalDB  
 SqlLocalDB supporta le opzioni seguenti.  
  
|Opzione|Descrizione|  
|------------|------------------|  
|`-?`|Viene stampato il testo della Guida.|  
|`create\|c "instance name" [version-number] [-s]`|Viene creata una nuova istanza del database locale con una versione e un nome specificati.<br /><br /> Se il parametro [version-number] viene omesso, il valore predefinito è la versione della build di SqlLocalDB.<br /><br /> Tramite il parametro -s viene avviata la nuova istanza del database locale dopo la relativa creazione.|  
|`delete\|d "instance name"`|Viene eliminata l'istanza del database locale con il nome specificato.|  
|`start\|s "instance name"`|Viene avviata l'istanza del database locale con il nome specificato.|  
|`stop\|p "instance name" [-i\|-k]`|Viene arrestata l'istanza del database locale con il nome specificato, al termine dell'esecuzione delle query correnti.<br /><br /> Tramite il parametro -i viene richiesto l'arresto dell'istanza del database locale con l'opzione NOWAIT.<br /><br /> Tramite il parametro -k viene terminato il processo dell'istanza del database locale senza contattare quest'ultimo.|  
|`share\|h ["owner SID or account"] "private name" "shared name"`|Viene condivisa l'istanza privata specificata tramite il nome condiviso indicato. Se viene omesso il SID dell'utente o il nome dell'account, il valore predefinito è l'utente corrente.|  
|`unshare\|u "shared name"`|Viene rimossa la condivisione dell'istanza del database locale condivisa specificata.|  
|`info\|i`|Vengono elencate tutte le istanze del database locale esistenti di proprietà dell'utente corrente nonché tutte le istanze del database locale condivise.|  
|`info\|i "instance name"`|Vengono stampate le informazioni sull'istanza specificata del database locale.|  
|`versions\|v`|Vengono elencate tutte le versioni del database locale installate nel computer.|  
|||  
|`trace\|t on\|off`|Viene abilitata o disabilitata la traccia.|  
  
 Gli spazi in SqlLocalDB vengono considerati come delimitatori. È necessario racchiudere tra virgolette i nomi delle istanze contenenti spazi e caratteri speciali. Ad esempio:  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
