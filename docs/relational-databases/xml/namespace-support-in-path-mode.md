---
title: Supporto dello spazio dei nomi in modalità di PATH | Microsoft Docs
description: Informazioni sul supporto dello spazio dei nomi quando si usa la modalità PATH per generare codice XML da una query SELECT.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode, namespace support
- namespaces [XML in SQL Server]
ms.assetid: 5f128ea2-0ceb-4b23-bce7-c8b3fd615466
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb8691f3cdd847a626db99a43e949a4b87a5aefe
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85661643"
---
# <a name="namespace-support-in-path-mode"></a>Supporto dello spazio dei nomi in modalità di PATH
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  In questa versione, il supporto dello spazio dei nomi in modalità PATH è disponibile utilizzando WITH NAMESPACES. Ad esempio, nella query seguente viene illustrata la sintassi WITH NAMESPACES per la dichiarazione di uno spazio dei nomi ("a:") che è possibile utilizzare nell'istruzione SELECT successiva:  
  
```  
WITH XMLNAMESPACES('a' as a)  
SELECT 1 as 'a:b'  
FOR XML PATH  
```  
  
## <a name="examples"></a>Esempi  
 In questi esempi viene illustrato l'utilizzo della modalità PATH nella generazione di codice XML da una query SELECT. Molte di queste query vengono specificate sui documenti XML di istruzioni per la produzione di biciclette archiviate nella colonna Instructions della tabella ProductModel.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzare la modalità PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
