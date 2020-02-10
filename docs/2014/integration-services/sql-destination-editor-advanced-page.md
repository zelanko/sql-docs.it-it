---
title: Editor destinazione SQL (pagina Avanzate) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdestadapter.advanced.f1
helpviewer_keywords:
- SQL Server Destination Editor
ms.assetid: 9b46bcf8-ddaf-4d7d-90a6-80bc19517e9b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 087f32510b65d7ea505bc4bf816a5ca9edcfe82d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055454"
---
# <a name="sql-destination-editor-advanced-page"></a>Editor destinazione SQL Server (pagina Avanzate)
  Usare la pagina **Avanzate** della finestra di dialogo **Editor destinazione SQL** per specificare le opzioni di inserimento bulk avanzate.  
  
 Per ulteriori informazioni sulla destinazione SQL Server, vedere [SQL Server Destination](data-flow/sql-server-destination.md).  
  
## <a name="options"></a>Opzioni  
 **Mantieni identità**  
 Consente di specificare se l'attività deve inserire valori nelle colonne Identity. Il valore predefinito di questa proprietà è `False`.  
  
 **Mantieni valori null**  
 Consente di specificare se l'attività deve mantenere i valori Null. Il valore predefinito di questa proprietà è `False`.  
  
 **Blocco di tabella**  
 Consente di specificare se la tabella viene bloccata durante il caricamento dei dati. Il valore predefinito di questa proprietà è `True`.  
  
 **Vincoli CHECK**  
 Consente di specificare se l'attività deve verificare i vincoli. Il valore predefinito di questa proprietà è `True`.  
  
 **Attiva trigger**  
 Consente di specificare se l'inserimento bulk deve attivare i trigger nelle tabelle. Il valore predefinito di questa proprietà è `False`.  
  
 **Prima riga**  
 Consente di specificare la prima riga da inserire. Il valore predefinito della proprietà è **-1**, a indicare che non è stato assegnato alcun valore.  
  
> [!NOTE]  
>  Deselezionare la casella in **Editor destinazione SQL** per indicare che non si vuole assegnare alcun valore alla proprietà. Usare -1 nella finestra **Proprietà** , in **Editor avanzato**e nel modello a oggetti.  
  
 **Ultima riga**  
 Consente di specificare l'ultima riga da inserire. Il valore predefinito di questa proprietà è **-1**, a indicare che non è stato assegnato alcun valore.  
  
> [!NOTE]  
>  Deselezionare la casella in **Editor destinazione SQL** per indicare che non si vuole assegnare alcun valore alla proprietà. Usare -1 nella finestra **Proprietà** , in **Editor avanzato**e nel modello a oggetti.  
  
 **Numero massimo di errori**  
 Consente di specificare il numero massimo di errori che possono verificarsi prima dell'arresto dell'inserimento bulk. Il valore predefinito della proprietà è **-1**, a indicare che non è stato assegnato alcun valore.  
  
> [!NOTE]  
>  Deselezionare la casella in **Editor destinazione SQL** per indicare che non si vuole assegnare alcun valore alla proprietà. Usare -1 nella finestra **Proprietà** , in **Editor avanzato**e nel modello a oggetti.  
  
 **Timeout**  
 Consente di specificare il numero di secondi di attesa prima che l'inserimento bulk venga arrestato a causa di un timeout.  
  
 **Colonne degli ordini**  
 Consente di digitare i nomi delle colonne di ordinamento. È possibile ordinare ogni colonna in ordine crescente o decrescente. Se si utilizzando più colonne di ordinamento, delimitare l'elenco con virgole.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor destinazione SQL &#40;pagina Gestione connessione&#41;](../../2014/integration-services/sql-destination-editor-connection-manager-page.md)   
 [Editor destinazione SQL &#40;pagina mapping&#41;](../../2014/integration-services/sql-destination-editor-mappings-page.md)   
 [Caricamento bulk dei dati tramite la destinazione SQL Server](data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  
