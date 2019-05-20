---
title: Ricerca incrementale in un documento attivo | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- Query Editor [SQL Server Management Studio], incremental search
- incremental searches [SQL Server Management Studio]
ms.assetid: 490bb36c-dd43-4219-9e2a-ff27046b9395
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e491d415ec1bcb62c95366f2471ba6780ad3874f
ms.sourcegitcommit: c29150492383f48ef484fa02a483cde1cbc68aca
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/17/2019
ms.locfileid: "65821964"
---
# <a name="search-an-active-document-incrementally"></a>Ricerca incrementale in un documento attivo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  È possibile eseguire una ricerca incrementale in un singolo documento o in una singola finestra immettendo il testo. Verrà evidenziato il primo set di caratteri che corrisponde ai caratteri immessi durante la ricerca incrementale nel documento o nella finestra. La ricerca viene estesa automaticamente a tutto il testo all'interno di un documento o di una finestra, fatta eccezione per il testo nascosto.  
  
 Se viene scelta l'opzione **Maiuscole/minuscole** , per la ricerca incrementale verranno usati i criteri della ricerca precedente. Se, ad esempio, in precedenza è stata eseguita una ricerca su più file tramite la finestra di dialogo **Cerca nei file** , viene selezionata l'opzione **Maiuscole/minuscole**e quindi viene eseguita una ricerca incrementale. Nella ricerca verrà fatta distinzione tra maiuscole e minuscole.  
  
### <a name="to-search-incrementally"></a>Per eseguire una ricerca incrementale  
  
1.  Aprire il file o la finestra in cui si desidera eseguire la ricerca.  
  
2.  Scegliere **Avanzate** dal menu **Modifica**e quindi fare clic su **Ricerca incrementale**.  
  
     L'icona del cursore si trasforma in un binocolo con una freccia, che indica la direzione della ricerca, mentre sulla barra di stato viene visualizzato "Ricerca incrementale".  
  
3.  Iniziare a digitare la stringa di testo.  
  
     Sulla barra di stato viene visualizzato il testo immesso mentre l'editor evidenzia la prima occorrenza corrispondente. Mentre la digitazione continua, l'editor si sposta sulla corrispondenza successiva e la evidenzia. Se non viene trovata nessuna corrispondenza, sulla barra di stato viene visualizzato quanto segue.  
  
    ```  
    Incremental Search: <text> (not found)  
    ```  
  
 Le ricerche incrementali vengono eseguite procedendo verso il basso e da sinistra a destra a partire dalla posizione corrente nel documento. È possibile utilizzare i tasti di scelta rapida.  
  
> [!NOTE]  
>  Per un elenco completo dei tasti di scelta rapida, vedere [Tasti di scelta rapida di SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca e sostituzione](../../relational-databases/scripting/search-and-replace.md)   
 [Ricerca interattiva all'interno di documenti](../../relational-databases/scripting/search-documents-interactively.md)   
 [Ricerca nei documenti utilizzando gli elenchi dei risultati](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [Testo di ricerca con caratteri jolly](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [Testo di ricerca con espressioni regolari](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
