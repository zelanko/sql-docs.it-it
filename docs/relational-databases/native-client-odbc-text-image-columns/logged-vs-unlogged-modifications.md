---
title: Modifiche Le modifiche registrate | Microsoft Docs
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
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 91e832a0f2abdfea91a63f17414bf431e7275103
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128895"
---
# <a name="logged-vs-unlogged-modifications"></a>Modifiche registrate e non registrate
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Un'applicazione può richiedere che il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client non registro **testo**, **ntext**, e **immagine** le modifiche. Questa opzione deve essere utilizzata con una certa cautela e Deve essere usato solo per quelle situazioni in cui il **testo**, **ntext**, o **immagine** dati non critici e i proprietari sono disposti a rinunciare alla possibilità di ripristinare i dati per prestazioni più elevate.  
  
 La registrazione delle **testo**, **ntext**, e **immagine** le modifiche vengono controllate chiamando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) con i  *Attributo* parametro è impostato su sql_sopt_ss _ TEXTPTR_LOGGING e *ValuePtr* impostato su SQL_TL_ON o SQL_TL_OFF.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di colonne di tipo text e image](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
