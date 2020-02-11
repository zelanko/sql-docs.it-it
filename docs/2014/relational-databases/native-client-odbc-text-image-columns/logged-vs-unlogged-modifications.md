---
title: Modifiche registrate e non registrate | Microsoft Docs
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
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c722d5360ad01e7e95508c2219ceb674de381286
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63195140"
---
# <a name="logged-vs-unlogged-modifications"></a>Confronto tra modifiche registrate e non registrate
  Un'applicazione può richiedere che il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client non registri le modifiche di tipo **Text**, **ntext**e **Image** . Questa opzione deve essere utilizzata con una certa cautela e Deve essere usato solo per le situazioni in cui i dati di tipo **Text**, **ntext**o **Image** non sono critici e i proprietari di dati sono disposti a comportare la possibilità di ripristinare i dati per ottenere prestazioni più elevate.  
  
 La registrazione delle modifiche di tipo **Text**, **ntext**e **Image** viene controllata chiamando [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) con il parametro *Attribute* impostato su SQL_SOPT_SS_ TEXTPTR_LOGGING e *ValuePtr* impostati su SQL_TL_ON o SQL_TL_OFF.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di colonne di tipo text e image](managing-text-and-image-columns.md)  
  
  
