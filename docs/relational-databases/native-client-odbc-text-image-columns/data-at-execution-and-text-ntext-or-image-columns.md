---
description: Colonne data-at-execution di tipo text, ntext o image
title: Data-at-execution e di tipo text, ntext e image
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 32f2bb59a0632c7070230750c720398a419b96b0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464922"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Colonne data-at-execution di tipo text, ntext o image
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC data-at-execution è una caratteristica che consente alle applicazioni di utilizzare quantità estremamente elevate di dati su colonne o parametri associati. Quando si recuperano colonne di tipo **Text**, **ntext** o **Image** di dimensioni molto grandi, un'applicazione potrebbe non essere in grado di allocare semplicemente un buffer enorme, associare la colonna al buffer e recuperare la riga. Quando si aggiornano colonne di tipo **Text**, **ntext** o **Image** di dimensioni molto grandi, l'applicazione potrebbe non essere in grado di allocare semplicemente un buffer enorme, associarlo a un marcatore di parametro in un'istruzione SQL ed eseguire l'istruzione. In questi casi, l'applicazione deve utilizzare [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) o [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md) con le opzioni data-at-execution.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di colonne di tipo text e image](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
