---
title: Origine dati i nomi e i sistemi operativi a 64 Bit | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 961f4e2f5a4c08dd39a2b274ceac1b87f84e0391
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913230"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>Nomi di origine dati e sistemi operativi a 64 bit
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Per compilare ed eseguire un'applicazione come applicazione a 32 bit in un sistema operativo a 64 bit, è necessario creare l'origine dati ODBC con Amministratore ODBC in %windir%\SysWOW64\odbcad32.exe.  
  
## <a name="remarks"></a>Note  
 Un sistema operativo Windows a 64 bit include due file odbcad32.exe:  
  
-   %SystemRoot%\system32\odbcad32.exe viene utilizzato per creare e gestire nomi di origine dati per applicazioni a 64 bit.  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe viene utilizzato per creare e gestire nomi di origine dati per applicazioni a 32 bit, incluse le applicazioni a 32 bit in esecuzione in sistemi operativi a 64 bit.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
