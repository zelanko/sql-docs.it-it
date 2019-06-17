---
title: Supporto di FOR XML per i tipi di dati stringa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- strings [SQL Server], XML
ms.assetid: bf069da8-de1e-44d2-a1fb-ade383076ac1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77a061d9a4bc1b1e320cf8af01599cdc52e139f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205020"
---
# <a name="for-xml-support-for-string-data-types"></a>Supporto di FOR XML per i tipi di dati stringa
  Il codice XML generato dagli spazi vuoti FOR XML nei dati viene sostituito con delle entità.  
  
 Nell'esempio seguente viene creata la tabella **T** e vengono inseriti dati di esempio che includono i caratteri di avanzamento riga, ritorno a capo e tabulazione. L'istruzione SELECT recupera i dati dalla tabella.  
  
```  
CREATE TABLE T  
(  
  c1 int identity primary key,  
  c2 varchar(100)  
);  
go  
  
INSERT T (c2) VALUES ('Special character 0xD for carriage return ' + convert(varchar(10), 0xD) + ' after carriage return');  
INSERT T (c2) VALUES ('Special character 0x9 for tab ' + convert(varchar(10), 0x9) + ' after tab' );  
INSERT T (c2) VALUES ('Special character 0xA for line feed ' + convert(varchar(10), 0xA) + ' after line feed');  
go  
SELECT *   
FROM T  
FOR XML AUTO;  
go  
```  
  
 Questo è il risultato:  
  
```  
 <T c1="1" c2="Special character 0xD for carriage return   
 after carriage return" />  
 <T c1="2" c2="Special character 0x9 for tab     after tab" />  
 <T c1="3" c2="Special character 0xA for line feed   
after line feed" />  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Il carattere di ritorno a capo nella prima riga viene sostituito con l'entità &#xD.  
  
-   Il carattere di tabulazione nella seconda riga viene sostituito con l'entità &#x09.  
  
-   Il carattere di avanzamento riga nella terza riga viene sostituito con l'entità &#xA.  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto di FOR XML per vari tipi di dati di SQL Server](for-xml-support-for-various-sql-server-data-types.md)  
  
  
