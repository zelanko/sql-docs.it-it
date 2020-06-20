---
title: Gestione di colonne di testo e immagini | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e9d7d5b0f48c68e8ac911f5e274c9afdb8cfe17d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049697"
---
# <a name="managing-text-and-image-columns"></a>Gestione di colonne di tipo text e image
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]i dati di tipo **Text**, **ntext**e **Image** (detti anche Long Data) sono tipi di dati stringa di tipo carattere o binario che possono contenere valori troppo grandi per essere contenuti in colonne **char**, **varchar**, **Binary**o **varbinary** . Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati **Text** viene mappato al tipo di dati ODBC SQL_LONGVARCHAR; **ntext** esegue il mapping a SQL_WLONGVARCHAR; e il mapping di **Immagini** a SQL_LONGVARBINARY. Alcuni elementi di dati, ad esempio i documenti lunghi o le bitmap di grandi dimensioni, potrebbero essere troppo grandi per essere archiviati correttamente in memoria. Per recuperare dati Long da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in parti sequenziali, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client consente a un'applicazione di chiamare [SQLGetData](../native-client-odbc-api/sqlgetdata.md). Per inviare dati Long in parti sequenziali, l'applicazione può chiamare [SQLPutData](../native-client-odbc-api/sqlputdata.md). I parametri per i quali i dati vengono inviati in fase di esecuzione sono noti come parametri data-at-execution.  
  
 Un'applicazione può effettivamente scrivere o recuperare qualsiasi tipo di dati (non solo i dati di tipo Long) con **SQLPutData** o **SQLGetData**, sebbene sia possibile inviare o recuperare solo dati di tipo **carattere** e **binario** in parti. Tuttavia, se i dati sono sufficientemente piccoli da adattarsi a un singolo buffer, in genere non esiste alcun motivo per utilizzare **SQLPutData** o **SQLGetData**. È molto più semplice associare il singolo buffer al parametro o alla colonna.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Colonne di tipo text e image associate e non associate](bound-vs-unbound-text-and-image-columns.md)  
  
-   [Modifiche registrate e non registrate](logged-vs-unlogged-modifications.md)  
  
-   [Colonne data-at-execution di tipo text, ntext o image](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
