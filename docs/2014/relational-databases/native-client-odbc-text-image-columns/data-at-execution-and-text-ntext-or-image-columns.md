---
title: Data-at-Execution e Text, ntext o Image colonne | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e7c57cf6444e5833b6deee0dcae36d71b7a6430
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63195133"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Colonne data-at-execution di tipo text, ntext o image
  ODBC data-at-execution è una caratteristica che consente alle applicazioni di utilizzare quantità estremamente elevate di dati su colonne o parametri associati. Quando si recuperano grandi **testo**, **ntext**, o **immagine** colonne, un'applicazione potrebbe non essere in grado di allocare un buffer molto grande, associare la colonna nel buffer e recuperare semplicemente la riga. Durante l'aggiornamento di dimensioni molto grandi **testo**, **ntext**, o **immagine** colonne, l'applicazione potrebbe non essere in grado di allocare un buffer molto grande, associarlo a un marcatore di parametro in un SQL semplicemente istruzione e quindi eseguire l'istruzione. In questi casi, l'applicazione deve utilizzare [SQLGetData](../native-client-odbc-api/sqlgetdata.md) oppure [SQLPutData](../native-client-odbc-api/sqlputdata.md) con le relative opzioni data-at-execution.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di colonne di tipo text e image](managing-text-and-image-columns.md)  
  
  
