---
description: Oggetti ADOX
title: Oggetti ADOX | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- objects [ADOX]
- ADOX, objects
ms.assetid: 3f5287e9-f62c-40c4-bb59-985102be956e
author: rothja
ms.author: jroth
ms.openlocfilehash: ca5131235b4c34c05f4cc3b783087f25dc027e95
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771580"
---
# <a name="adox-objects"></a>Oggetti ADOX
## <a name="adox-object-summary"></a>Riepilogo oggetto ADOX  
  
|Oggetto|Descrizione|  
|------------|-----------------|  
|[Catalogo](./catalog-object-adox.md)|Contiene le raccolte che descrivono il catalogo dello schema di un'origine dati.|  
|[Colonna](./column-object-adox.md)|Rappresenta una colonna di una tabella, un indice o una chiave.|  
|[Gruppo](./group-object-adox.md)|Rappresenta un account di gruppo che dispone di autorizzazioni di accesso all'interno di un database protetto.|  
|[Index](./index-object-adox.md)|Rappresenta un indice di una tabella di database.|  
|[Chiave](./key-object-adox.md)|Rappresenta un campo chiave primaria, esterna o univoca di una tabella di database.|  
|[Procedura](./procedure-object-adox.md)|Rappresenta un stored procedure.|  
|[Tabella](./table-object-adox.md)|Rappresenta una tabella di database, inclusi colonne, indici e chiavi.|  
|[User](./user-object-adox.md)|Rappresenta un account utente che dispone di autorizzazioni di accesso all'interno di un database protetto.|  
|[Visualizzazione](./view-object-adox.md)|Rappresenta un set filtrato di record o una tabella virtuale.|  
  
 Le relazioni tra questi oggetti sono illustrate nel [modello a oggetti ADOX](./adox-object-model.md).  
  
 Ogni oggetto può essere contenuto nella raccolta corrispondente. Un oggetto **Table** , ad esempio, può essere contenuto in una raccolta [Tables](./tables-collection-adox.md) . Per ulteriori informazioni, vedere [ADOX Collections](./adox-collections.md) o un argomento specifico della raccolta.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di riferimento sull'API ADOX](./adox-object-model.md?view=sql-server-ver15)   
 [Raccolte ADOX](./adox-collections.md)   
 [Modello a oggetti ADOX](./adox-object-model.md)   
 [ADO Extensions for Data Definition Language and Security (ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)