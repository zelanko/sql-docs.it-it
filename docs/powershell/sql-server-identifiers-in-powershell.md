---
title: Identificatori di SQL Server in PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Cmdlets [SQL Server], Encode-Sqlname
- PowerShell [SQL Server], identifiers
- Encode-Sqlname cmdlet
- PowerShell [SQL Server], Encode-Sqlname
- Decode-Sqlname cmdlet
- PowerShell [SQL Server], Decode-Sqlname
- identifiers [SQL Server], PowerShell
- Cmdlets [SQL Server], Decode-Sqlname
ms.assetid: 651099b0-33b4-453a-a864-b067f21eb8b9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 654bd3d29de94401fc95d1a5d4d580f299b95297
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62672423"
---
# <a name="sql-server-identifiers-in-powershell"></a>Identificatori di SQL Server in PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Il provider di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per Windows PowerShell usa gli identificatori di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nei percorsi di Windows PowerShell. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ha identificatori che possono contenere caratteri non supportati nei percorsi di Windows PowerShell. Per tali caratteri è necessario usare caratteri di escape oppure la codifica speciale quando gli identificatori vengono usati nei percorsi di Windows PowerShell.  
  
> [!NOTE]
> Esistono due moduli SQL Server PowerShell: **SqlServer** e **SQLPS**. Il modulo **SQLPS** è incluso nell'installazione di SQL Server (per la compatibilità con le versioni precedenti), ma non viene più aggiornato. Il modulo PowerShell più aggiornato è il modulo **SqlServer**. Il modulo **SqlServer** contiene versioni aggiornate dei cmdlet di **SQLPS** e include anche nuovi cmdlet per il supporto delle funzionalità SQL più recenti.  
> Le versioni precedenti del modulo **SqlServer** *erano* incluse con SQL Server Management Studio (SSMS), ma solo con le versioni 16.x di SQL Server Management Studio. Per usare PowerShell con SSMS 17.0 e versioni successive, è necessario installare il modulo **SqlServer** da PowerShell Gallery.
> Per installare il modulo **SqlServer**, vedere [Installare il modulo PowerShell SqlServer](download-sql-server-ps-module.md).


## <a name="sql-server-identifiers-in-windows-powershell-paths"></a>Identificatori di SQL Server nei percorsi di Windows PowerShell  
 I provider Windows PowerShell espongono le gerarchie di dati tramite una struttura di percorso simile a quella del file system di Windows. Il provider [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] implementa i percorsi degli oggetti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per il [!INCLUDE[ssDE](../includes/ssde-md.md)], l'unità è impostata su SQLSERVER: la prima cartella è impostata su \SQL e agli oggetti di database viene fatto riferimento come contenitori ed elementi. Di seguito è riportato il percorso della tabella Vendor nello schema Purchasing del database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] in un'istanza predefinita del [!INCLUDE[ssDE](../includes/ssde-md.md)]:  
  
```  
SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Purchasing.Vendor  
```  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ha identificatori che sono i nomi degli oggetti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , ad esempio i nomi di tabelle o colonne. Esistono due tipi di identificatori di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] :  
  
-   Gli identificatori regolari sono limitati a un set di caratteri supportati anche nei percorsi di Windows PowerShell. Questi nomi possono essere utilizzati nei percorsi di Windows PowerShell senza essere modificati.  
  
-   Gli identificatori delimitati possono utilizzare caratteri non supportati nei nomi dei percorsi di Windows PowerShell. Gli identificatori delimitati sono chiamati identificatori tra parentesi se sono racchiusi tra parentesi quadre ([IdentifierName]) e identificatori tra virgolette se sono racchiusi tra virgolette doppie ("IdentifierName"). Se un identificatore delimitato utilizza caratteri non supportati nei percorsi di Windows PowerShell, i caratteri devono essere codificati o devono essere utilizzati caratteri di escape prima di utilizzare l'identificatore come nome di contenitore o di elemento. La codifica è supportata per tutti i caratteri. Per alcuni caratteri, come i due punti (:), non è possibile utilizzare caratteri di escape.  
  
## <a name="sql-server-identifiers-in-cmdlets"></a>Identificatori di SQL Server nei cmdlet  
 Alcuni cmdlet di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dispongono di un parametro che accetta un identificatore come input. I valori del parametro vengono generalmente forniti come costanti di stringa tra virgolette o nelle variabili di stringa. Quando gli identificatori vengono forniti come costanti di stringa o nelle variabili, non si verifica alcun conflitto con il set dei caratteri supportati da Windows PowerShell.  
  
## <a name="sql-server-identifier-tasks"></a>Attività degli identificatori di SQL Server  
  
|Descrizione dell'attività|Articolo|  
|----------------------|-----------|  
|Viene descritto come specificare un nome dell'istanza, includendo il nome del computer in cui è in esecuzione l'istanza.|[Specifica di istanze nel provider SQL Server PowerShell](specify-instances-in-the-sql-server-powershell-provider.md)|  
|Viene descritto come specificare la codifica esadecimale per i caratteri negli identificatori delimitati che non sono supportati nei percorsi di Windows PowerShell. Viene inoltre descritto come decodificare i caratteri esadecimali.|[Codificare e decodificare identificatori di SLQ Server](encode-and-decode-sql-server-identifiers.md)|  
|Viene descritto come utilizzare il carattere di escape di Windows PowerShell per i caratteri non supportati nei percorsi di PowerShell.|[Identificatori di escape di SQL Server](escape-sql-server-identifiers.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Provider PowerShell per SQL Server](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)   
 [Identificatori del database](../relational-databases/databases/database-identifiers.md)  
  
  
