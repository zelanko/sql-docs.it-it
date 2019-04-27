---
title: Formati di dati per l'importazione o l'esportazione bulk (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], choosing
- bulk importing [SQL Server], data formats
ms.assetid: 73fe6741-9437-4b26-b030-28b863e74399
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 676b5a8d8d05c5cb26a30eaa1b1fe9426ac30ea7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62661896"
---
# <a name="data-formats-for-bulk-import-or-bulk-export-sql-server"></a>Formati di dati per l'importazione o l'esportazione bulk (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può accettare dati nel formato dati di tipo carattere o nel formato dati binario nativo. Utilizzare il formato carattere se vengono spostati dati tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e un'altra applicazione (ad esempio [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel) o un altro server di database (ad esempio Oracle o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). È possibile utilizzare il formato nativo unicamente se si trasferiscono dati tra due istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   [Formati di dati per l'importazione o l'esportazione bulk](#ComponentsAndConcepts)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> Formati di dati per l'importazione o l'esportazione bulk  
 Nella tabella seguente viene indicato quale formato di dati è generalmente appropriato utilizzare in base alla modalità di rappresentazione dei dati e all'origine o destinazione dell'operazione.  
  
|Operazione|Nativo|nativi Unicode|Carattere|carattere Unicode|  
|---------------|------------|--------------------|---------------|-----------------------|  
|Trasferimenti bulk di dati tra più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite un file di dati che non contiene caratteri estesi o DBCS (Double-Byte Character Set). A meno che non venga utilizzato un file di formato, la definizione delle tabelle deve essere identica.|Sì<sup>1</sup>|-|-|-|  
|Per le colonne `sql_variant` è consigliabile utilizzare il formato di dati nativo perché, a differenza dei formati carattere o Unicode, mantiene i metadati per ogni valore `sql_variant`.|Yes|-|-|-|  
|Trasferimenti bulk di dati tra più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite un file di dati contenente caratteri estesi o DBCS.|-|Yes|-|-|  
|Importazione bulk di dati da un file di testo creato da un altro programma.|-|-|Yes|-|  
|Esportazione bulk di dati in un file di testo che verrà utilizzato in un altro programma.|-|-|Yes|-|  
|Trasferimenti bulk di dati tra più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite un file di dati contenente dati Unicode e che non contiene caratteri estesi o DBCS.|-|-|-|Yes|  
  
 <sup>1</sup> metodo più veloce per l'esportazione bulk di dati dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando si usa **bcp**.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Usare il formato nativo per importare o esportare dati &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato carattere per importare o esportare dati &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Utilizzo del formato carattere Unicode per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Importare dati in formato nativo e carattere da versioni precedenti di SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Specificare i formati di dati per la compatibilità con bcp &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)  
  
  
