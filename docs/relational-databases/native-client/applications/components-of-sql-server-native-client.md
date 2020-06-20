---
title: Componenti
description: Informazioni sui componenti del SQL Server Native Client, ad esempio sqlncli11.dll, sqlnclir11. rll, sqlncli. h e sqlncli11. lib.
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f298c7e3c453da1a20826d91509ca61778ad65b0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965198"
---
# <a name="components-of-sql-server-native-client"></a>Componenti di SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client sono inclusi i componenti seguenti:  
  
|Componente|Descrizione|  
|---------------|-----------------|  
|sqlncli11.dll|File della libreria di collegamento dinamico (DLL) che contiene tutte le funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Sono inclusi il provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlnclir11.rll|File di risorse associato per la libreria di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|   
|sqlncli.h|File di intestazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client che contiene tutte le nuove definizioni necessarie per utilizzare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Questo file di intestazione sostituisce entrambi i file di intestazione, odbcss.h e sqloledb.h.<br /><br /> Nota: non è possibile fare riferimento a sqlncli. h e a ODBCs. h nello stesso programma, ma è possibile fare riferimento a sqlncli. h e SQLOLEDB. h nello stesso programma purché venga definito per primo SQLOLEDB. h.|  
|sqlncli11.lib|File di libreria necessario per chiamare direttamente le funzioni dell'utilità **bcp** che fanno parte del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client.<br /><br /> Nota: se si fa riferimento al file sqlncli11. lib nel codice di programmazione, è necessario assicurarsi che il file di sqlncli11.dll si trovi nel percorso di sistema e nel percorso di sistema degli utenti che usano l'applicazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
