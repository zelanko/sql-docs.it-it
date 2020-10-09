---
description: ICommand (provider OLE DB Native Client)
title: ICommand (provider OLE DB Native Client) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ICommand [SQL Server Native Client]
ms.assetid: 5e24b3a0-0658-44fc-b653-f4c52f9eb328
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3a2d8a552d3d1efeccd24a34524bbdde273d3f09
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867146"
---
# <a name="icommand-native-client-ole-db-provider"></a>ICommand (provider OLE DB Native Client)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  In questo argomento viene illustrato il comportamento di OLE DB specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 L'inserimento di un numero di dati maggiori delle dimensioni di una colonna restituisce in genere un errore. In alcuni casi, tuttavia, viene restituito S_OK, ma *dwStatus* viene impostato su DBSTATUS_S_TRUNCATED. Questo problema si verifica in genere quando si inseriscono dati con parametri, in cui la colonna non è sufficientemente grande da poter essere contenuta nei dati e **ICommandWithParameters:: separameterinfo** non è stato chiamato.  
  
## <a name="see-also"></a>Vedere anche  
 [Interfacce &#40;OLE DB&#41;](./sql-server-native-client-ole-db-interfaces.md)  
  
