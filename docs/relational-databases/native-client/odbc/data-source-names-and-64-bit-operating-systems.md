---
title: Nomi delle origini dati e sistemi operativi a 64 bit | Microsoft Docs
description: Informazioni su come compilare ed eseguire un'applicazione come applicazione a 32 bit in un sistema operativo a 64 bit mediante la creazione dell'origine dati ODBC con l'amministratore ODBC.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e88446d089473d5cae615765e21517c58ce80730
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84950428"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>Nomi di origine dati e sistemi operativi a 64 bit
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Per compilare ed eseguire un'applicazione come applicazione a 32 bit in un sistema operativo a 64 bit, è necessario creare l'origine dati ODBC con Amministratore ODBC in %windir%\SysWOW64\odbcad32.exe.  
  
## <a name="remarks"></a>Commenti  
 Un sistema operativo Windows a 64 bit include due file odbcad32.exe:  
  
-   %SystemRoot%\system32\odbcad32.exe viene utilizzato per creare e gestire nomi di origine dati per applicazioni a 64 bit.  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe viene utilizzato per creare e gestire nomi di origine dati per applicazioni a 32 bit, incluse le applicazioni a 32 bit in esecuzione in sistemi operativi a 64 bit.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
