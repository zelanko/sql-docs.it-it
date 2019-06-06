---
title: Proprietà dinamiche ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2ad6c2804b70011380a12b5b9e0cd1f52fd56398
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696869"
---
# <a name="ado-dynamic-properties"></a>Proprietà dinamiche ADO
Proprietà dinamica possono essere aggiunte alle [le proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolte del [connessione](../../../ado/reference/ado-api/connection-object-ado.md), [comando](../../../ado/reference/ado-api/command-object-ado.md), o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetti. L'origine per queste proprietà è di provider di dati, ad esempio la [il Provider OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), o un provider di servizi, ad esempio le [Microsoft Cursor Service per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md). Vedere la documentazione di provider di servizio per altre informazioni su una proprietà dinamica specifica o provider di dati appropriato.  
  
 Il [indice proprietà dinamica ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) fornisce un riferimento incrociato tra i nomi ADO e OLE DB per ogni proprietà dinamica di provider OLE DB standard.  
  
 Le seguenti proprietà dinamiche sono particolarmente interessanti e sono documentate anche nelle origini indicate in precedenza. Funzionalità speciali con ADO è documentata negli argomenti della Guida ADO nell'elenco seguente.  
  
|||  
|-|-|  
|[Ottimizzazione](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Specifica se è necessario creare un indice su questo campo.|  
|[Prompt](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|Specifica se il provider OLE DB deve richiedere all'utente le informazioni di inizializzazione.|  
|[Proprietà dinamica Reshape Name](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Specifica un nome per il **Recordset** oggetto.|  
|[La risincronizzazione di comando](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Specifica un comando fornito dall'utente di stringhe che il **Risincronizza** i problemi di metodi per aggiornare i dati nella tabella denominata nel **tabella univoca** proprietà dinamica.|  
|[Tabella univoca, Schema univoco, catalogo univoco](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**Tabella univoca** specifica il nome della tabella di base su cui sono consentite aggiornamenti, inserimenti ed eliminazioni.<br /><br /> **Schema univoco** specifica lo schema, o nome del proprietario della tabella.<br /><br /> **Catalogo univoco** specifica il catalogo, o il nome del database contenente la tabella.|  
|[Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|Specifica se il **UpdateBatch** metodo è seguito da implicita **Risincronizza** operazione del metodo e in questo caso, l'ambito di tale operazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Raccolte di ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Costanti enumerate ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Appendice B: Errori ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventi ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Metodi ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfacce e oggetti ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Proprietà ADO](../../../ado/reference/ado-api/ado-properties.md)
