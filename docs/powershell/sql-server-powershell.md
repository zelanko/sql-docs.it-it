---
title: SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7a2725586a094aed0cb7d933553bc3fc389adfdf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67912209"
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

**[Installare SQL Server PowerShell](download-sql-server-ps-module.md)**

> [!NOTE]
> Esistono due moduli SQL Server PowerShell: **SqlServer** e **SQLPS**. Il modulo **SQLPS** è incluso nell'installazione di SQL Server (per la compatibilità con le versioni precedenti), ma non viene più aggiornato. Il modulo PowerShell più aggiornato è il modulo **SqlServer**. Il modulo **SqlServer** contiene versioni aggiornate dei cmdlet di **SQLPS** e include anche nuovi cmdlet per il supporto delle funzionalità SQL più recenti.  
> Le versioni precedenti del modulo **SqlServer***erano* incluse con SQL Server Management Studio (SSMS), ma solo con le versioni 16.x di SQL Server Management Studio. Per usare PowerShell con SSMS 17.0 e versioni successive, è necessario installare il modulo **SqlServer** da PowerShell Gallery.
> Per installare il modulo **SqlServer**, vedere [Installare il modulo PowerShell SqlServer](download-sql-server-ps-module.md).

**Perché il modulo è cambiato da SQLPS a SqlServer?**

Per inviare gli aggiornamenti di SQL PowerShell, è stato necessario modificare l'identità del modulo SQL PowerShell, nonché il wrapper noto come *SQLPS.exe*. A causa di questa modifica, sono ora presenti due moduli SQL PowerShell: **SqlServer** e **SQLPS**.  

**Aggiornare gli script di PowerShell che importano il modulo SQLPS.**

Se si hanno script di PowerShell script che eseguono `Import-Module -Name SQLPS` e se si vogliono sfruttare la nuova funzionalità del provider e i nuovi cmdlet, è necessario modificarli in `Import-Module -Name SqlServer`. Il nuovo modulo viene installato nella cartella `%ProgramFiles%\WindowsPowerShell\Modules\SqlServer`. Non è quindi necessario aggiornare la variabile $env:PSModulePath. Se si hanno script che usano una versione di terze parti o community di un modulo denominato **SqlServer**, usare il parametro Prefix per evitare conflitti di nome.

Non sono state apportate modifiche al modulo usato da SQL Server Agent. Di conseguenza, i passaggi del processo di tipo PowerShell usano il modulo SQLPS. Per altre informazioni, vedere [Come eseguire PowerShell con SQL Server Agent](run-windows-powershell-steps-in-sql-server-agent.md).


## <a name="sql-server-powershell-components"></a>Componenti di PowerShell di SQL Server  
Il modulo **SqlServer** carica due snap-in di Windows PowerShell:  
  
-   Un provider di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , che abilita un semplice meccanismo di navigazione simile ai percorsi del file system. È possibile compilare percorsi simili a quelli del file system, in cui l'unità è associata a un modello a oggetti di gestione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e i nodi sono basati sulle classi del modello a oggetti. È quindi possibile usare comandi comuni come **cd** e **dir** per un'esplorazione dei percorsi simile all'esplorazione delle cartelle in una finestra del prompt dei comandi. È possibile usare altri comandi, ad esempio **ren** o **del**, per eseguire azioni sui nodi nel percorso.  
  
-   Un set di cmdlet che supportano azioni quali l'esecuzione di uno script **sqlcmd** contenente istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] o XQuery.  
  
  
## <a name="sql-server-versions"></a>Versioni di SQL Server  
I cmdlet SQL PowerShell possono essere usati per gestire le istanze del database SQL di Azure, di Azure SQL Data Warehouse e di tutti i [prodotti SQL Server supportati](https://support.microsoft.com/lifecycle/search/1044).  


## <a name="sql-server-identifiers-that-contain-characters-not-supported-in-powershell-paths"></a>Identificatori SQL Server che contengono caratteri non supportati nei percorsi di PowerShell  
 
I cmdlet **Encode-Sqlname** e **Decode-Sqlname** consentono di specificare identificatori SQL Server che contengono caratteri non supportati nei percorsi di Windows PowerShell. Per altre informazioni, vedere [Identificatori di SQL Server in PowerShell](sql-server-identifiers-in-powershell.md).  
  
Usare il cmdlet **Convert-UrnToPath** per convertire l'URN (Uniform Resource Name) di un oggetto [!INCLUDE[ssDE](../includes/ssde-md.md)] in un percorso del provider PowerShell SQL Server. Per altre informazioni, vedere [Conversione di URN in percorsi di provider di SQL Server](https://docs.microsoft.com/powershell/module/sqlserver/Convert-UrnToPath).  
  
## <a name="query-expressions-and-unique-resource-names"></a>Espressioni di query e Unique Resource Name  

Le espressioni di query sono stringhe che utilizzano una sintassi analoga a XPath per specificare un set di criteri utilizzato per enumerare uno o più oggetti in una gerarchia del modello a oggetti. L'URN (Unique Resource Name) è un tipo specifico di stringa di espressione di query che identifica un singolo oggetto in modo univoco. Per altre informazioni, vedere [Espressioni di query e Uniform Resource Name](query-expressions-and-uniform-resource-names.md).       


## <a name="cmdlet-reference"></a>Informazioni di riferimento sui cmdlet
* [Cmdlet di SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)
* [Cmdlet di SQLPS](https://docs.microsoft.com/powershell/module/sqlps)
