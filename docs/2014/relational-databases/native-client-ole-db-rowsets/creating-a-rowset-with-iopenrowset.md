---
title: Creazione di un set di righe con IOpenRowset | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3d8865f6a6e38e9764b7aa2c67d069eeb6a4ec84
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704683"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Creazione di un set di righe con IOpenRowset
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client supporta il metodo **IOpenRowset:: OPENROWSET** con le restrizioni seguenti:  
  
-   Una vista o una tabella di base deve essere specificata in una struttura del database (DBID) a cui punta il parametro *pTableID*.  
  
-   Il membro DBID *eKind* deve indicare DBKIND_NAME.  
  
-   Il membro DBID *uName* deve specificare il nome di una vista o di una tabella di base esistente come stringa di caratteri Unicode.  
  
-   Il parametro *pIndexID* di **OpenRowset** deve essere NULL.  
  
 Il set di risultati di **IOpenRowset::OpenRowset** contiene un solo set di righe. I set di risultati che contengono un singolo set di righe possono essere supportati dai [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursori. Il supporto del cursore consente allo sviluppatore di utilizzare i meccanismi di concorrenza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Set di righe](rowsets.md)  
  
  
