---
title: Proprietà database (pagina Filegroup) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.filegroups.f1
ms.assetid: 8d06e859-73dd-4019-b6e8-99c5c5297697
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b8de45556d3c19ee8460b33e7f07ceb485b37597
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62917118"
---
# <a name="database-properties-filegroups-page"></a>Proprietà database (pagina Filegroup)
  Utilizzare questa pagina per visualizzare i filegroup o aggiungere un nuovo filegroup al database selezionato. I tipi di filegroup sono suddivisi in filegroup di *righe*, in filegroup di dati FILESTREAM e in filegroup ottimizzati per la memoria.  
  
 I filegroup di righe contengono file di dati e di log standard. I filegroup di dati FILESTREAM contengono file di dati FILESTREAM. Questi file di dati archiviano informazioni sulle modalità con cui i dati BLOB (binary large object) vengono archiviati nel file system quando si utilizza l'archiviazione FILESTREAM. Le opzioni sono le stesse per entrambi tipi di filegroup.  
  
 Se FILESTREAM non è stato abilitato, la sezione **Filestream** non sarà disponibile. È possibile abilitare l'archiviazione FILESTREAM usando la finestra di dialogo [Proprietà server (pagina Avanzate)](../../database-engine/configure-windows/server-properties-advanced-page.md).  
  
 Per altre informazioni sul modo in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa i filegroup righe, vedere [Filegroup e file di database](database-files-and-filegroups.md). Per altre informazioni sui filegroup e i dati FILESTREAM, vedere [FILESTREAM &#40;SQL Server&#41;](../blob/filestream-sql-server.md).  
  
 I filegroup ottimizzati per la memoria sono necessari per consentire ai database di contenere una o più tabelle ottimizzate per la memoria.  
  
## <a name="row-and-filestream-data-filegroup-options"></a>Opzioni di filegroup di righe e di dati FILESTREAM  
 **Nome**  
 Consente di immettere il nome del filegroup.  
  
 **File**  
 Visualizza il numero dei file contenuti nel filegroup.  
  
 **Sola lettura**  
 Consente di impostare il filegroup sullo stato di sola lettura.  
  
 **Default**  
 Consente di impostare il filegroup come filegroup predefinito. È possibile avere un filegroup predefinito per le righe e un filegroup predefinito per i dati FILESTREAM.  
  
 **Aggiungere**  
 Consente di aggiungere una nuova riga vuota alla griglia in cui sono elencati i filegroup per il database.  
  
 **Rimuovi**  
 Consente di rimuovere il filegroup selezionato dalla griglia.  
  
## <a name="memory-optimized-data-filegroup-options"></a>Opzioni di filegroup di dati con ottimizzazione per la memoria  
 **Nome**  
 Consente di immettere il nome del filegroup ottimizzato per la memoria.  
  
 **File FILESTREAM**  
 Visualizza il numero di file (contenitori) nel filegroup di dati ottimizzato per la memoria. È possibile aggiungere contenitori nella pagina **File** .  
  
 **Aggiungere**  
 Consente di aggiungere una nuova riga vuota alla griglia in cui sono elencati i filegroup per il database.  
  
 **Rimuovi**  
 Consente di rimuovere il filegroup selezionato dalla griglia.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
