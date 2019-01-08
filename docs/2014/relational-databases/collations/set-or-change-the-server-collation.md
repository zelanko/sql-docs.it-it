---
title: Impostare o modificare le regole di confronto del server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- server collations [SQL Server]
- collations [SQL Server], server
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4501bc77a28746de3b0ce97b7b619889093650d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52778733"
---
# <a name="set-or-change-the-server-collation"></a>Impostazione o modifica di regole di confronto del server
  Le regole di confronto del server costituiscono le regole di confronto predefinite per tutti i database di sistema installati con l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e per ogni database utente creato successivamente. Le regole di confronto del server vengono specificate durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Collation and Unicode Support](collation-and-unicode-support.md).  
  
## <a name="changing-the-server-collation"></a>Modifica di regole di confronto del server  
 La modifica delle regole di confronto predefinite per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere un'operazione complessa e richiede i passaggi seguenti:  
  
-   Assicurarsi che siano disponibili tutte le informazioni o gli script necessari per ricreare i database utente e tutti gli oggetti in essi contenuti.  
  
-   Esportare tutti i dati usando uno strumento come [l'utilità bcp](../../tools/bcp-utility.md). Per altre informazioni, vedere [Importazione ed esportazione bulk di dati &#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md).  
  
-   Eliminare tutti i database utente.  
  
-   Ricompilare il database master specificando le nuove regole di confronto nella proprietà SQLCOLLATION del comando **setup** . Ad esempio:  
  
    ```  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName   
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]   
    /SQLCOLLATION=CollationName  
    ```  
  
     Per altre informazioni, vedere [Ricompilare database di sistema](../databases/system-databases.md).  
  
-   Creare tutti i database e tutti gli oggetti in essi contenuti.  
  
-   Importare tutti i dati.  
  
> [!NOTE]  
>  Anziché modificare le regole di confronto predefinite di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile specificare regole di confronto predefinite per ogni nuovo database creato.  
  
## <a name="see-also"></a>Vedere anche  
 [Collation and Unicode Support](collation-and-unicode-support.md)   
 [Impostare o modificare le regole di confronto del database](set-or-change-the-database-collation.md)   
 [Impostare o modificare le regole di confronto delle colonne](set-or-change-the-column-collation.md)   
 [Ricompilare database di sistema](../databases/system-databases.md)  
  
  
