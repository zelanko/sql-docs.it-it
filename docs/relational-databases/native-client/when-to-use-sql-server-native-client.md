---
title: Quando utilizzare SQL Server Native Client Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
ms.assetid: 08f18b36-209d-4cf7-9623-ebc61859a91d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4340b1a5e79c17e1b7e8bf6dcff69d2a5789572d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305013"
---
# <a name="when-to-use-sql-server-native-client"></a>Utilizzo di SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è una tecnologia che è possibile utilizzare per accedere ai dati in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Per una discussione sulle diverse tecnologie di accesso ai dati, vedere [Panoramica delle tecnologie di accesso ai dati](https://go.microsoft.com/fwlink/?LinkID=179186)  
  
 Quando si decide se utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client come tecnologia di accesso ai dati dell'applicazione, è necessario considerare diversi fattori.  
  
 Per le nuove applicazioni, se si utilizza un linguaggio di programmazione gestito, come Microsoft Visual C# o Visual Basic, e si desidera accedere alle nuove caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario utilizzare il provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluso in .NET Framework.  
  
 L'utilizzo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è consigliabile se si sviluppa un'applicazione basata su COM e si ha l'esigenza di accedere alle nuove caratteristiche introdotte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se non è necessario accedere alle nuove caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile continuare a utilizzare Windows Data Access Components (WDAC).  
  
 Per le applicazioni OLE DB e ODBC esistenti, il problema principale è dato dalla necessità o meno di accedere alle nuove caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In caso di un'applicazione obsoleta per la quale non sono richieste le nuove funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile continuare a utilizzare WDAC. Tuttavia, se è necessario accedere a queste nuove funzionalità, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ad esempio il tipo di dati [xml](../../t-sql/xml/xml-transact-sql.md), è necessario utilizzare Native Client.  
  
 Sia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client che MDAC supportano l'isolamento delle transazioni Read Committed mediante il controllo delle versioni delle righe, ma solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supporta l'isolamento delle transazioni snapshot. In termini di programmazione, l'isolamento delle transazioni Read Committed mediante il controllo delle versioni delle righe equivale a una transazione Read Committed.  
  
 Per informazioni sulle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] differenze tra Native Client e MDAC, vedere [Aggiornamento di un'applicazione a SQL Server Native Client da MDAC](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client Programming](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Argomenti relativi alle procedure ODBC](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Procedure per l'utilizzo di OLE DB](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
