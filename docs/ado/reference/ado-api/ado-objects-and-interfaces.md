---
description: Interfacce e oggetti ADO
title: Oggetti e interfacce ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
author: rothja
ms.author: jroth
ms.openlocfilehash: 80a47336bb6453033a28b2d62eeda3700431594a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451373"
---
# <a name="ado-objects-and-interfaces"></a>Interfacce e oggetti ADO
Le relazioni tra questi oggetti sono rappresentate nel [modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md).  
  
 Ogni oggetto può essere contenuto nella raccolta corrispondente. Un oggetto [Error](../../../ado/reference/ado-api/error-object.md) , ad esempio, può essere contenuto in una raccolta [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) . Per ulteriori informazioni, vedere [raccolte ADO](../../../ado/reference/ado-api/ado-collections.md) o un argomento specifico della raccolta.  
  
|Oggetto o interfaccia|Descrizione|  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|Utilizzato per recuperare il comando OLEDB sottostante da un oggetto ADOCommand.|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|Costruisce un oggetto **record** ADO da un oggetto OLE DB **riga** in un'applicazione C/C++.|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|Costruisce un oggetto **Recordset** ADO da un oggetto OLE DB **set di righe** in un'applicazione C/C++.|  
|[Interfaccia ADOStreamConstruction](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|Costruisce un oggetto **flusso** ADO da un oggetto OLE DB **IStream** in un'applicazione C/C++.|  
|[Comando](../../../ado/reference/ado-api/command-object-ado.md)|Definisce un comando specifico che si desidera eseguire su un'origine dati.<br /><br /> L'oggetto **Command** non è sicuro per lo scripting.|  
|[Connection](../../../ado/reference/ado-api/connection-object-ado.md)|Rappresenta una connessione aperta a un'origine dati.<br /><br /> L'oggetto **Connection** è sicuro per lo scripting.|  
|[Interfaccia IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|Ottiene l'oggetto origine dati OLEDB sottostante per il provider di forme.|  
|[Error (Errore) (Error (Errore)e)](../../../ado/reference/ado-api/error-object.md)|Contiene informazioni dettagliate sugli errori di accesso ai dati relativi a una singola operazione che interessa il provider.<br /><br /> L'oggetto **errore** non è sicuro per lo scripting.|  
|[Campo](../../../ado/reference/ado-api/field-object.md)|Rappresenta una colonna di dati con un tipo di dati comune.|  
|[Parametro](../../../ado/reference/ado-api/parameter-object.md)|Rappresenta un parametro o un argomento associato a un oggetto **Command** basato su una query con parametri o stored procedure.<br /><br /> L'oggetto **Parameter** non è sicuro per lo scripting.|  
|[Proprietà](../../../ado/reference/ado-api/property-object-ado.md)|Rappresenta una caratteristica dinamica di un oggetto ADO definito dal provider.|  
|[Record](../../../ado/reference/ado-api/record-object-ado.md)|Rappresenta una riga di un **Recordset**o una directory o un file in un file System. L'oggetto **record** è sicuro per lo scripting.|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|Rappresenta il set di record di una tabella di base o i risultati di un comando eseguito. In qualsiasi momento, l'oggetto **Recordset** fa riferimento solo a un singolo record all'interno del set come record corrente.<br /><br /> L'oggetto **Recordset** è sicuro per lo scripting.|  
|[Flusso](../../../ado/reference/ado-api/stream-object-ado.md)|Rappresenta un flusso di dati binario.<br /><br /> L'oggetto **flusso** è sicuro per lo scripting.|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Raccolte ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Proprietà dinamiche ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Costanti enumerate ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Appendice B: errori ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventi ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Metodi ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Proprietà ADO](../../../ado/reference/ado-api/ado-properties.md)
