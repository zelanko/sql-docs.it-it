---
title: Numeri di errore nativi Documenti Microsoft
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0b5572ee784f47b0444e1d825de1b6dd53db8066
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291607"
---
# <a name="native-error-numbers"></a>Numeri di errori nativi
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Per gli errori che si verificano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nell'origine dati (restituita da ), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]driver ODBC Native Client restituisce il numero di errore nativo restituito da . Per gli errori rilevati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal driver, il driver ODBC Native Client restituisce un numero di errore nativo pari a 0. Per ulteriori informazioni su un elenco di numeri di errore nativi, **master** vedere la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]colonna di errore della tabella di sistema **sysmessages** nel database master in .  
  
 Per informazioni sui codici di errore di stato, vedere Codici di [errore ODBC SQLSTATE &#40;&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md). Per gli errori restituiti dalla libreria di rete, il numero di errori nativi viene derivato dal software di rete sottostante.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di errori e messaggi](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
