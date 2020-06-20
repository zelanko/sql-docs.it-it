---
title: Colonne data-at-execution e di tipo text, ntext o image | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 404fade34862fe4705ec440eef7f466a9073250b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039295"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Colonne data-at-execution di tipo text, ntext o image
  ODBC data-at-execution è una caratteristica che consente alle applicazioni di utilizzare quantità estremamente elevate di dati su colonne o parametri associati. Quando si recuperano colonne di tipo **Text**, **ntext**o **Image** di dimensioni molto grandi, un'applicazione potrebbe non essere in grado di allocare semplicemente un buffer enorme, associare la colonna al buffer e recuperare la riga. Quando si aggiornano colonne di tipo **Text**, **ntext**o **Image** di dimensioni molto grandi, l'applicazione potrebbe non essere in grado di allocare semplicemente un buffer enorme, associarlo a un marcatore di parametro in un'istruzione SQL ed eseguire l'istruzione. In questi casi, l'applicazione deve utilizzare [SQLGetData](../native-client-odbc-api/sqlgetdata.md) o [SQLPutData](../native-client-odbc-api/sqlputdata.md) con le opzioni data-at-execution.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di colonne di tipo text e image](managing-text-and-image-columns.md)  
  
  
