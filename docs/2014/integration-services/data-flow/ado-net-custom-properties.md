---
title: Proprietà personalizzate ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e062a9ab-1e6b-4061-845a-4f8a0552b09d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 531c613ccc1fdda19f50b9f4a7c5c2ad2d09d8c1
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84916789"
---
# <a name="ado-net-custom-properties"></a>Proprietà personalizzate ADO NET
  **Proprietà personalizzate delle origini**  
  
 L'origine ADO NET include sia proprietà personalizzate sia le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine ADO.NET. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|CommandTimeout|string|Valore che specifica il numero di secondi di attesa prima che si verifichi il timeout del comando SQL. Il valore 0 indica che non è impostato alcun timeout del comando.|  
|SqlCommand|string|Istruzione SQL utilizzata dall'origine ADO.NET per l'estrazione dei dati.<br /><br /> Durante il caricamento del pacchetto, è possibile aggiornare dinamicamente la proprietà con l'istruzione SQL che verrà utilizzata dall'origine ADO.NET. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md) e [Utilizzo delle espressioni di proprietà nei pacchetti](../expressions/use-property-expressions-in-packages.md).|  
|AllowImplicitStringConversion|Boolean|Valore che indica se si verificano le condizioni seguenti:<br /><br /> Nessuna generazione di un errore di convalida in caso di mancata corrispondenza tra i tipi di metadati esterni e i tipi stringa delle colonne di output (DT_WSTR o DT_NTEXT).<br /><br /> Conversione implicita dei tipi di metadati esterni nel tipo di dati stringa utilizzato dalla colonna di output.<br /><br /> <br /><br /> Il valore predefinito è TRUE.<br /><br /> Per altre informazioni, vedere [Origine ADO NET](ado-net-source.md).|  
  
 L'output e le colonne di output dell'origine ADO.NET non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Origine ADO NET](ado-net-source.md).  
  
 **Proprietà personalizzate delle destinazioni**  
  
 La destinazione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] include sia proprietà personalizzate che le proprietà comuni a tutti i componenti flusso di dati.  
  
 La tabella seguente descrive le proprietà personalizzate della destinazione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] . Tutte le proprietà sono di lettura/scrittura. Tali proprietà non sono disponibili in **Editor di destinazione ADO.NET**, ma possono essere impostate tramite **Editor avanzato**.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|BatchSize|Integer|Numero di righe in un batch inviato al server. Il valore **0** indica che le dimensioni del batch corrispondono alle dimensioni del buffer interno. Il valore predefinito di questa proprietà è **0**.|  
|CommandTimeout|Integer|Numero massimo di secondi durante i quali è possibile eseguire il comando SQL prima del timeout. Il valore **0** corrisponde a un intervallo infinito. Il valore predefinito di questa proprietà è **0**.|  
|TableOrViewName|string|Nome della tabella o vista di destinazione.|  
  
 Per altre informazioni, vedere [Destinazione ADO NET](ado-net-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](../common-properties.md)  
  
  
