---
title: Gestione di colonne di testo e immagini | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 221d83188a3d48fe5383a109b878c7b5a59bdad5
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73758400"
---
# <a name="managing-text-and-image-columns"></a>Gestione di colonne di tipo text e image
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati di tipo **Text**, **ntext**e **Image** (detti anche Long Data) sono tipi di dati stringa di tipo carattere o binario che possono contenere valori di dati troppo grandi per adattarsi a **char**, **varchar**, **Binary**o **varbinary** colonne. Il tipo di dati **text** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene mappato al tipo di dati ODBC SQL_LONGVARCHAR; **ntext** esegue il mapping a SQL_WLONGVARCHAR; e il mapping di **Immagini** a SQL_LONGVARBINARY. Alcuni elementi di dati, ad esempio i documenti lunghi o le bitmap di grandi dimensioni, potrebbero essere troppo grandi per essere archiviati correttamente in memoria. Per recuperare dati Long da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in parti sequenziali, il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client consente a un'applicazione di chiamare [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). Per inviare dati Long in parti sequenziali, l'applicazione può chiamare [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md). I parametri per i quali i dati vengono inviati in fase di esecuzione sono noti come parametri data-at-execution.  
  
 Un'applicazione può effettivamente scrivere o recuperare qualsiasi tipo di dati (non solo i dati di tipo Long) con **SQLPutData** o **SQLGetData**, sebbene sia possibile inviare o recuperare solo dati di tipo **carattere** e **binario** in parti. Tuttavia, se i dati sono sufficientemente piccoli da adattarsi a un singolo buffer, in genere non esiste alcun motivo per utilizzare **SQLPutData** o **SQLGetData**. È molto più semplice associare il singolo buffer al parametro o alla colonna.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Colonne del testo e dell'immagine non associato](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [Modifiche registrate e non registrate](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [Colonne data-at-execution di tipo text, ntext o image](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
