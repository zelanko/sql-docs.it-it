---
title: Quando usare SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
ms.assetid: 08f18b36-209d-4cf7-9623-ebc61859a91d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5d16f4dc681042babcedc8d7ddffa8fbc0389506
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704105"
---
# <a name="when-to-use-sql-server-native-client"></a>Utilizzo di SQL Server Native Client
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è una tecnologia che è possibile utilizzare per accedere ai dati in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Per una discussione sulle diverse tecnologie di accesso ai dati, vedere [Panoramica delle tecnologie di accesso ai dati](https://go.microsoft.com/fwlink/?LinkID=179186)  
  
 Quando si decide se utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client come tecnologia di accesso ai dati dell'applicazione, è necessario considerare diversi fattori.  
  
 Per le nuove applicazioni, se si utilizza un linguaggio di programmazione gestito, come Microsoft Visual C# o Visual Basic, e si desidera accedere alle nuove caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario utilizzare il provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluso in .NET Framework.  
  
 L'utilizzo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è consigliabile se si sviluppa un'applicazione basata su COM e si ha l'esigenza di accedere alle nuove caratteristiche introdotte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se non è necessario accedere alle nuove caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile continuare a utilizzare Windows Data Access Components (WDAC).  
  
 Per le applicazioni OLE DB e ODBC esistenti, il problema principale è dato dalla necessità o meno di accedere alle nuove caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In caso di un'applicazione obsoleta per la quale non sono richieste le nuove funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile continuare a utilizzare WDAC. Tuttavia, se è necessario accedere a queste nuove funzionalità, ad esempio il [tipo di dati XML](/sql/t-sql/xml/xml-transact-sql), è necessario utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Sia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client che MDAC supportano l'isolamento delle transazioni Read Committed mediante il controllo delle versioni delle righe, ma solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supporta l'isolamento delle transazioni snapshot. In termini di programmazione, l'isolamento delle transazioni Read Committed mediante il controllo delle versioni delle righe equivale a una transazione Read Committed.  
  
 Per informazioni sulle differenze tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client e MDAC, vedere [aggiornamento di un'applicazione a SQL Server Native Client da MDAC](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Procedure per ODBC](../native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Procedure relative a OLE DB](../native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
