---
title: Sasabot (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7195311fefe3f0f1b7b4d6d789aa8d8487bc3bfe
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933503"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  L'interfaccia **ISSAbort** , esposta nel provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, fornisce il metodo [ISSAbort::Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) che viene utilizzato per annullare il set di righe corrente oltre a qualsiasi comando eseguito in batch insieme al comando che ha inizialmente generato il set di righe e non ha ancora completato l'esecuzione.  
  
 **ISSAbort** è un'interfaccia specifica del provider di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client disponibile mediante **QueryInterface** sull'oggetto **IMultipleResults** restituito da **ICommand::Execute** o **IOpenRowset::OpenRowset**.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[Dissabot:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|Annulla il set di righe corrente oltre a qualsiasi comando eseguito in batch associato al comando corrente.|  
  
## <a name="see-also"></a>Vedere anche  
 [Interfacce &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
