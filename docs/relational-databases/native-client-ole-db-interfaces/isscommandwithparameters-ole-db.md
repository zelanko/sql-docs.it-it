---
title: ISSCommandWithParameters (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 08291b998c0f540b56cad59d29433135993487c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73761966"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSCommandWithParameters** espone il supporto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per XML e i tipi definiti dall'utente (UDT). Si tratta di un'interfaccia facoltativa che eredita dall'interfaccia di base OLE DB **ICommandWithParameters**. Oltre ai tre metodi ereditati da **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**e **separameterinfo**; In **ISSCommandWithParameters** sono disponibili due nuovi metodi utilizzati per gestire i tipi di dati specifici del server.  
  
> [!NOTE]  
>  L'interfaccia **ISSCommandWithParameters** può essere utilizzata quando si utilizzano i componenti del servizio, ma i componenti del servizio non utilizzeranno questa interfaccia.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[ISSCommandWithParameters:: GetParameterProperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|Restituisce una struttura del set di proprietà **SSPARAMPROPS** della matrice per ogni parametro XML o tipo definito dall'utente passato al comando. Per gli altri tipi di parametro non ne restituisce nessuna.|  
|[ISSCommandWithParameters:: SetParameterProperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|Imposta le proprietà dei parametri per ogni parametro in base al numero ordinale oppure imposta le proprietà dei parametri bulk specificando una matrice di strutture **SSPARAMPROPS** .|  
  
## <a name="see-also"></a>Vedere anche  
 [Interfacce &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [Utilizzo di tipi di dati XML](../../relational-databases/native-client/features/using-xml-data-types.md)   
 [Utilizzo dei tipi definiti dall'utente (UDT)](../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
