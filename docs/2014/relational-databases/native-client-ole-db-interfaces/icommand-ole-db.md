---
title: ICommand (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ICommand [SQL Server Native Client]
ms.assetid: 5e24b3a0-0658-44fc-b653-f4c52f9eb328
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4e583b08cf0ba55268c4acb9e19722d3a693d50
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62987324"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
  In questo argomento viene illustrato il comportamento di OLE DB specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 L'inserimento di un numero di dati maggiori delle dimensioni di una colonna restituisce in genere un errore. In alcuni casi, tuttavia, viene restituito S_OK, ma *dwStatus* viene impostato su DBSTATUS_S_TRUNCATED. Questa situazione si verifica in genere quando vengono inseriti dati con parametri in una colonna di dimensioni insufficienti per contenere i dati, senza aver chiamato `ICommandWithParameters::SetParameterInfo`.  
  
## <a name="see-also"></a>Vedere anche  
 [Interfacce &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
