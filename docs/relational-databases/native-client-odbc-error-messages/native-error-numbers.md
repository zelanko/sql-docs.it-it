---
title: Numeri di errore nativi | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1bc1f9383ab615a24b0506b86cf0ec5e37b6c74
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783402"
---
# <a name="native-error-numbers"></a>Numeri di errori nativi
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Per gli errori che si verificano nell'origine dati (restituiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client restituisce il numero di errore nativo restituito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per gli errori rilevati dal driver, il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client restituisce un numero di errore nativo pari a 0. Per ulteriori informazioni su un elenco di numeri di errore nativi, vedere la colonna Error della tabella di sistema **sysmessages** nel database **Master** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per informazioni sui codici di errore di stato, [vedere &#40;codici&#41;di errore SQLSTATE ODBC](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md). Per gli errori restituiti dalla libreria di rete, il numero di errori nativi viene derivato dal software di rete sottostante.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di errori e messaggi](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
