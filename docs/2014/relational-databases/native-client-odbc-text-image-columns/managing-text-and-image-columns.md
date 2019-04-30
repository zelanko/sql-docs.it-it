---
title: La gestione di colonne Text e Image | Microsoft Docs
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
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a161b009239db3c17acb64f8d8eeaaa61321cd9f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63195322"
---
# <a name="managing-text-and-image-columns"></a>Gestione di colonne di tipo text e image
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **testo**, **ntext**, e **immagine** dati (detto anche dati di tipo long) sono carattere o i tipi di dati stringa binaria che possono contenere valori di dati troppo grandi per rientrare nella **char**, **varchar**, **binary**, o **varbinary** colonne. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **testo** tipo di dati esegue il mapping al tipo di dati ODBC SQL_LONGVARCHAR. **ntext** a SQL_WLONGVARCHAR e **immagine** a SQL_LONGVARBINARY. Alcuni elementi di dati, ad esempio i documenti lunghi o le bitmap di grandi dimensioni, potrebbero essere troppo grandi per essere archiviati correttamente in memoria. Da cui recuperare dati long [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in parti sequenziali, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client consente a un'applicazione chiamare [SQLGetData](../native-client-odbc-api/sqlgetdata.md). Per inviare dati di tipo long in parti sequenziali, l'applicazione può chiamare [SQLPutData](../native-client-odbc-api/sqlputdata.md). I parametri per i quali i dati vengono inviati in fase di esecuzione sono noti come parametri data-at-execution.  
  
 Un'applicazione in realtà può scrivere o recuperare qualsiasi tipo di dati (non solo lunga) con **SQLPutData** oppure **SQLGetData**, ma solo **carattere** e  **binario** i dati possono essere inviati o recuperati in parti. Tuttavia, se i dati sono sufficientemente piccoli da rientrare in un singolo buffer, non è in genere necessario usare **SQLPutData** oppure **SQLGetData**. È molto più semplice associare il singolo buffer al parametro o alla colonna.  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Colonne di tipo text e image associate e non associate](bound-vs-unbound-text-and-image-columns.md)  
  
-   [Modifiche registrate e non registrate](logged-vs-unlogged-modifications.md)  
  
-   [Colonne data-at-execution di tipo text, ntext o image](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
