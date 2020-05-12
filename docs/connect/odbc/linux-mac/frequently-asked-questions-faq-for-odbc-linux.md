---
title: Domande frequenti su ODBC in Linux e macOS
description: Trovare le risposte alle domande più comuni su Microsoft ODBC Driver for SQL Server in Linux e macOS.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 700c89b520cdaa33a60f1adabe69c669388bcccb
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886455"
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>Domande frequenti su ODBC in Linux e macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Di seguito sono riportate le risposte a domande riguardanti il driver ODBC per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS.
  
## <a name="frequently-asked-questions"></a>Domande frequenti

**Come funzionano le applicazioni ODBC esistenti in Linux o macOS con il driver?**  
Dovrebbe essere possibile compilare ed eseguire le applicazioni ODBC compilate ed eseguite in Linux o macOS con altri driver. 
  
**Quali funzionalità di [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] supporta questa versione del driver?**

Il driver ODBC in Linux e macOS supporta tutte le funzionalità server di [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ad eccezione del database locale. Per altre informazioni sulle funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supportate, vedere [Linee guida per la programmazione](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
**Il driver supporta l'autenticazione Kerberos?**  
Sì. Se esiste una configurazione dell'ambiente Kerberos esistente, sarà possibile connettersi ai server usando l'opzione DSN `Trusted_Connection=Yes` o la stringa di connessione. Per altre informazioni, vedere [Uso dell'autenticazione integrata](../../../connect/odbc/linux-mac/using-integrated-authentication.md).  
  
**Quale codifica Unicode deve essere usata dall'applicazione?**  
UTF-8 per i dati SQL_CHAR e UTF-16 per i dati SQL_WCHAR. A seconda delle impostazioni locali del sistema e della versione del driver, possono essere supportati anche i dati non UTF-8 in una delle diverse codifiche. Per altre informazioni, vedere [Linee guida per la programmazione](../../../connect/odbc/linux-mac/programming-guidelines.md).

**Sono disponibili esempi ODBC che è possibile scaricare ed eseguire con il driver per provarlo o valutarlo?**

Per un esempio, vedere l'articolo relativo all' [uso di esempi ODBC C++ di MSDN per il driver ODBC in Linux](/archive/blogs/sqlblog/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver) . Questa operazione è applicabile anche al driver ODBC macOS.

**Il driver ODBC in Linux o macOS è open source?**

No, i driver ODBC in Linux e macOS non sono un prodotto open source.  

## <a name="see-also"></a>Vedere anche

- [Installazione di Microsoft ODBC Driver for SQL Server in Linux](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Installazione di Microsoft ODBC Driver for SQL Server in macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)
