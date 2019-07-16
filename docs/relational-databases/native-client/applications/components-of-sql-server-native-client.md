---
title: I componenti di SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5b0f5000c84f06991d28fd80167bdae1dfae9610
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069339"
---
# <a name="components-of-sql-server-native-client"></a>Componenti di SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client sono inclusi i componenti seguenti:  
  
|Componente|Descrizione|  
|---------------|-----------------|  
|sqlncli11.dll|File della libreria di collegamento dinamico (DLL) che contiene tutte le funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Sono inclusi il provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlnclir11.rll|File di risorse associato per la libreria di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|   
|sqlncli.h|File di intestazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client che contiene tutte le nuove definizioni necessarie per utilizzare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Questo file di intestazione sostituisce entrambi i file di intestazione, odbcss.h e sqloledb.h.<br /><br /> Nota: È possibile fare riferimento a SQLNCLI. h e Odbcss. h nello stesso programma, ma è possibile fare riferimento a SQLNCLI. h e SQLOLEDB. h nello stesso programma, purché venga definito prima SQLOLEDB. h.|  
|sqlncli11.lib|Il file di libreria necessario per chiamare direttamente le **bcp** le funzioni di utilità che fanno parte di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client.<br /><br /> Nota: Se si fa riferimento al file sqlncli11.lib nel codice di programmazione, è necessario assicurarsi che il file sqlncli11.dll si sia nel percorso di sistema e nel percorso di sistema di utenti che utilizzano l'applicazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
