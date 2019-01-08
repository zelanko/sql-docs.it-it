---
title: Caricare dati tramite la destinazione ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 339ec0a8-922e-48c0-97b3-fc5ee34f95e3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bf59655f907b048d08166e8cb7ef1e0f4bc63503
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771243"
---
# <a name="load-data-by-using-the-odbc-destination"></a>Caricare dati tramite la destinazione ODBC
  In questa procedura viene descritto come caricare dati tramite la destinazione ODBC. Per aggiungere e configurare una destinazione ODBC, è necessario che il pacchetto includa già almeno un'attività Flusso di dati e un'origine.  
  
### <a name="to-load-data-using-an-odbc-destination"></a>Per caricare dati tramite una destinazione ODBC  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]aprire il pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] desiderato.  
  
2.  Fare clic sulla scheda **Flusso di dati** e quindi trascinare la destinazione ODBC dalla **Casella degli strumenti**all'area di progettazione.  
  
3.  Trascinare un output disponibile di un componente flusso di dati nell'input della destinazione ODBC.  
  
4.  Fare doppio clic sulla destinazione ODBC.  
  
5.  Nella pagina **Gestione connessione** della finestra di dialogo **Editor destinazione ODBC** selezionare una gestione connessione ODBC esistente oppure fare clic su **Nuova** per creare una nuova gestione connessione.  
  
6.  Selezionare il metodo di accesso ai dati.  
  
    -   **Nome tabella - Batch**: Selezionare questa opzione per configurare la destinazione ODBC per l'utilizzo della modalità batch. Quando si seleziona questa opzione, è possibile impostare un valore per **Dimensioni batch**.  
  
    -   **Nome tabella - riga per riga**: Selezionare questa opzione per configurare la destinazione ODBC per l'inserimento di una riga per volta nella tabella di destinazione. Quando si seleziona questa opzione, i dati vengono caricati una riga per volta nella tabella.  
  
7.  Nel campo **Nome tabella o vista** selezionare una tabella o una vista disponibile del database dall'elenco o digitare un'espressione regolare per identificare la tabella. Questo elenco contiene solo le prime 1000 tabelle. Se il database contiene più di 1000 tabelle, è possibile digitare l'inizio di un nome di tabella o utilizzare il carattere jolly (*) per immettere qualsiasi parte del nome e visualizzare la tabella o le tabelle che si desidera utilizzare.  
  
8.  È possibile fare clic su **Anteprima** per visualizzare fino a 200 righe dei dati della tabella selezionata nella destinazione ODBC.  
  
9. Fare clic su **Mapping** e quindi eseguire il mapping delle colonne nell'elenco **Colonne di input disponibili** alle colonne nell'elenco **Colonne di destinazione disponibili** , trascinando le colonne da un elenco all'altro.  
  
10. Per configurare l'output degli errori, fare clic su **Output errori**.  
  
11. Fare clic su **OK**.  
  
12. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Editor destinazione ODBC &#40;pagina Gestione connessione&#41;](../odbc-destination-editor-connection-manager-page.md)   
 [ODBC Destination Editor &#40;pagina Mapping&#41;](../odbc-destination-editor-mappings-page.md)   
 [Editor origine ODBC &#40;pagina Output degli errori&#41;](../odbc-source-editor-error-output-page.md)  
  
  
