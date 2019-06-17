---
title: Estrarre dati tramite l'origine ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 10f25703-49a2-4d45-abab-6b4da2a57ba5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f8ecb517174c8cd8189ad2f7382c774df3545620
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62864948"
---
# <a name="extract-data-by-using-the-odbc-source"></a>Estrarre dati tramite l'origine ODBC
  In questa procedura viene descritto come estrarre dati utilizzando un'origine ODBC. Per aggiungere e configurare un'origine ODBC, è necessario che il pacchetto includa già almeno un'attività Flusso di dati.  
  
### <a name="to-extract-data-using-an-odbc-source"></a>Per estrarre dati tramite un'origine ODBC  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]aprire il pacchetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] desiderato.  
  
2.  Fare clic sulla scheda **Flusso di dati** e quindi trascinare l'origine ODBC dalla **Casella degli strumenti**all'area di progettazione.  
  
3.  Fare doppio clic sull'origine ODBC.  
  
4.  Nella pagina **Gestione connessione** della finestra di dialogo **Editor origine ODBC** selezionare una gestione connessione ODBC esistente oppure fare clic su **Nuova** per creare una nuova gestione connessione.  
  
5.  Selezionare il metodo di accesso ai dati.  
  
    -   **Nome tabella**: selezionare una tabella o una vista nel database o digitare un'espressione regolare per identificare la tabella a cui è connessa la gestione connessione ODBC.  
  
         Questo elenco contiene solo le prime 1000 tabelle. Se il database contiene più di 1000 tabelle, è possibile digitare l'inizio di un nome di tabella o utilizzare il carattere jolly (*) per immettere qualsiasi parte del nome e visualizzare la tabella o le tabelle che si desidera utilizzare.  
  
    -   **Comando SQL**: digitare un comando SQL o fare clic su **Sfoglia** per caricare la query SQL da un file di testo.  
  
6.  È possibile fare clic su **Anteprima** per visualizzare fino a 200 righe dei dati estratti dall'origine ODBC.  
  
7.  Per aggiornare il mapping tra colonne esterne e colonne di output, fare clic su **Colonne** e selezionare colonne diverse nell'elenco **Colonna esterna** .  
  
8.  Se necessario, aggiornare i nomi delle colonne di output modificando i valori nell'elenco **Colonna di output** .  
  
9. Per configurare l'output degli errori, fare clic su **Output errori**.  
  
10. Fare clic su **OK**.  
  
11. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine ODBC &#40;pagina Gestione connessione&#41;](../odbc-source-editor-connection-manager-page.md)   
 [Editor origine ODBC &#40;pagina Colonne&#41;](../odbc-source-editor-columns-page.md)   
 [Editor origine ODBC &#40;pagina Output degli errori&#41;](../odbc-source-editor-error-output-page.md)  
  
  
