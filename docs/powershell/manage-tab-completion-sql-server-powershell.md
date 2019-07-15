---
title: Gestire il completamento alla pressione del tasto TAB (SQL Server PowerShell) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b02c72e49e2f7c8230f6e60e47c3e3ff9120d8e2
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730644"
---
# <a name="manage-tab-completion-sql-server-powershell"></a>Gestione del completamento alla pressione del tasto TAB (SQL Server PowerShell)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]


Gli snap-in PowerShell di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] introducono tre variabili ( **$SqlServerMaximumTabCompletion**, **$SqlServerMaximumChildItems**e **$SqlServerIncludeSystemObjects**) per controllare il completamento alla pressione del tasto TAB di Windows PowerShell. Il completamento alla pressione del tasto TAB consente di ridurre la digitazione restituendo tabelle di elementi i cui nomi iniziano con la stringa che si sta digitando.  

> [!NOTE]
> Esistono due moduli SQL Server PowerShell: **SqlServer** e **SQLPS**. Il modulo **SQLPS** è incluso nell'installazione di SQL Server (per la compatibilità con le versioni precedenti), ma non viene più aggiornato. Il modulo PowerShell più aggiornato è il modulo **SqlServer**. Il modulo **SqlServer** contiene versioni aggiornate dei cmdlet di **SQLPS** e include anche nuovi cmdlet per il supporto delle funzionalità SQL più recenti.  
> Le versioni precedenti del modulo **SqlServer** *erano* incluse con SQL Server Management Studio (SSMS), ma solo con le versioni 16.x di SQL Server Management Studio. Per usare PowerShell con SSMS 17.0 e versioni successive, è necessario installare il modulo **SqlServer** da PowerShell Gallery.
> Per installare il modulo **SqlServer**, vedere [Installare il modulo PowerShell SqlServer](download-sql-server-ps-module.md).
  
Con il completamento alla pressione del tasto TAB di Windows PowerShell, dopo aver digitato parte del nome di un percorso o di un cmdlet, è possibile premere il tasto TAB per ottenere un elenco degli elementi il cui nome corrisponde a quanto già digitato. È quindi possibile selezionare l'elemento desiderato dall'elenco senza digitare il resto del nome.  
  
Se si usa un database che contiene molti oggetti, gli elenchi di completamento alla pressione del tasto TAB possono diventare molto grandi. Anche alcuni tipi di oggetto di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , ad esempio le viste, includono numerosi oggetti di sistema.  
  
Gli snap-in di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] introducono tre variabili di sistema che possono essere usate per controllare la quantità di informazioni generata dal completamento alla pressione del tasto TAB e da **Get-ChildItem**.  
  
 **$SqlServerMaximumTabCompletion =** *n*  
 Specifica il numero massimo di oggetti da includere in un elenco di completamento alla pressione del tasto TAB. Se si seleziona il tasto TAB in un nodo del percorso con più di *n* oggetti, l'elenco di completamento alla pressione del tasto TAB viene troncato in corrispondenza di *n*. *n* è un numero intero. L'impostazione predefinita è 0, che indica che non esiste alcun limite al numero di oggetti elencati.  
  
 **$SqlServerMaximumChildItems =** *n*  
 Specifica il numero massimo di oggetti visualizzati da **Get-ChildItem**. Se **Get-ChildItem** viene eseguito in un nodo del percorso con più di *n* oggetti, l'elenco viene troncato in corrispondenza di *n*. *n* è un numero intero. L'impostazione predefinita è 0, che indica che non esiste alcun limite al numero di oggetti elencati.  
  
 **$SqlServerIncludeSystemObjects =** { **$True** |  **$False** }  
 Se **$True**, gli oggetti di sistema vengono visualizzati dal completamento alla pressione del tasto TAB e da **Get-ChildItem**. Se **$False**, non viene visualizzato alcun oggetto di sistema. L'impostazione predefinita è **$False**.  
  
## <a name="set-the-sql-server-tab-completion-variables"></a>Impostazione delle variabili per il completamento alla pressione del tasto TAB  
 Per tutte le variabile di cui si desidera modificare il valore predefinito, impostare la variabile sul nuovo valore.  
  
### <a name="example-powershell"></a>Esempio (PowerShell)  
 Nell'esempio seguente vengono impostate tutte e tre le variabili e vengono elencate le relative impostazioni:  
  
```  
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
