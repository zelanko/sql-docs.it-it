---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ecf72f0015d9ed197b3b7a33d4f9bb3246134b1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056156"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
  L' `IRowsetFastLoad` interfaccia espone il supporto per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le operazioni di copia bulk basate sulla memoria. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]I consumer del provider OLE DB di Native client utilizzano l'interfaccia per aggiungere rapidamente dati a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella esistente.  
  
 Se si imposta SSPROP_ENABLEFASTLOAD su VARIANT_TRUE per una sessione, non è possibile leggere dati dai set di righe restituiti successivamente dalla sessione. Quando SSPROP_ENABLEFASTLOAD è impostato su VARIANT_TRUE, tutti i set di righe creati nella sessione saranno del tipo IRowsetFastLoad. I set di righe IRowsetFastLoad non supportano la funzionalità di recupero del set di righe, quindi non è possibile leggere i set di righe.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[IRowsetFastLoad::Commit &#40;OLE DB&#41;](irowsetfastload-commit-ole-db.md)|Contrassegna la fine di un batch di righe inserite e scrive le righe nella tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[IRowsetFastLoad::InsertRow &#40;OLE DB&#41;](irowsetfastload-insertrow-ole-db.md)|Aggiunge una riga al set di righe della copia bulk.|  
  
## <a name="see-also"></a>Vedere anche  
 [Interfacce &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [Copia dati bulk con IRowsetFastLoad &#40;OLE DB&#41;](../native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [Inviare dati BLOB a SQL Server usando IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
