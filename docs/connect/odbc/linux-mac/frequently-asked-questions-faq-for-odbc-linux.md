---
title: Domande frequenti per ODBC in Linux e macOS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cc31a8ae385f2dbb28db30b299377ab5b38058f9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "68702772"
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

Per un esempio, vedere l'articolo relativo all' [uso di esempi ODBC C++ di MSDN per il driver ODBC in Linux](https://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) . Questa operazione è applicabile anche al driver ODBC macOS. 

**Il driver ODBC in Linux o macOS è open source?**

No, i driver ODBC in Linux e macOS non sono un prodotto open source.  

## <a name="see-also"></a>Vedere anche
[Installazione di Microsoft ODBC Driver for SQL Server in Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
