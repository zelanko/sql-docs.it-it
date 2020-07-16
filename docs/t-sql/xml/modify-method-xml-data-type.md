---
title: Metodo modify() (tipo di dati xml)
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 52a2766833d6ab4349c3f6b000f35e9d686396bd
ms.sourcegitcommit: cb620c77fe6bdefb975968837706750c31048d46
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2020
ms.locfileid: "86393089"
---
# <a name="modify-method-xml-data-type"></a>Metodo modify() (tipo di dati xml)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Modifica il contenuto di un documento XML. Usare questo metodo per modificare il contenuto di una variabile o colonna di tipo **xml**. Il metodo richiede un'istruzione XML DML per inserire, aggiornare o eliminare i nodi dai dati XML. Il metodo **modify()** del tipo di dati **xml** può essere usato unicamente nella clausola SET di un'istruzione UPDATE.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
modify (XML_DML)  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 XML_DML  
 Stringa nel linguaggio di manipolazione dei dati (DML, Data Manipulation Language) XML. Il documento XML viene aggiornato in base a questa espressione.  
  
> [!NOTE]  
>  Se il metodo **modify()** viene chiamato su un valore Null oppure restituisce un valore Null, viene restituito un errore.  
  
## <a name="examples"></a>Esempi  
 Dato che il metodo **modify()** richiede una stringa nel linguaggio di manipolazione dei dati XML (DML, Data Manipulation Language), gli esempi per **modify()** sono contenuti negli argomenti che descrivono le istruzioni XML DML. Per questi esempi, vedere [insert &#40;XML DML&#41;](../../t-sql/xml/insert-xml-dml.md), [delete &#40;XML DML&#41;](../../t-sql/xml/delete-xml-dml.md) e [replace value of &#40;XML DML&#41;](../../t-sql/xml/replace-value-of-xml-dml.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creare istanze di dati XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [metodi con tipo di dati XML](../../t-sql/xml/xml-data-type-methods.md)   
 [Linguaggio XML di manipolazione dei dati &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
