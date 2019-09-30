---
title: Configurazione destinazione file flat (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8c596f37cb0a83682c5c8dff370a92a5d3d73eb5
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285791"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>Configurazione destinazione file flat (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Se è stata selezionata una destinazione file flat, l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] visualizza **Configurazione destinazione file flat** dopo aver specificato che si vuole copiare una tabella o dopo aver indicato una query. In questa pagina è possibile specificare le opzioni di formattazione per il file flat di destinazione. Facoltativamente, è possibile esaminare il mapping di singole colonne e visualizzare in anteprima i dati di esempio.  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>Screenshot della pagina Configurare la destinazione del file flat  
 Lo screenshot seguente illustra la pagina **Configurazione destinazione file flat** della procedura guidata.
 
 In questo esempio, per creare un file CSV (valori delimitati da virgole) tipico, l'utente ha specificato le opzioni seguenti.
-   **Delimitatore di riga**. Ogni riga di dati nell'output termina con una combinazione ritorno a capo/avanzamento riga.
-   **Delimitatore di colonna**. Le colonne di dati all'interno di ogni riga sono separate da una virgola.

 ![Pagina Configurazione destinazione file flat dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/media/flat-file.png)
  
## <a name="pick-a-source-table"></a>Selezionare una tabella di origine
 **Tabella o vista di origine**  
-   Se in una pagina precedente si è specificato che si vuole copiare una tabella, selezionare la tabella o la vista di origine nell'elenco a discesa.
-   Se si è specificata una query, è disponibile un'unica opzione, `"Query"`, che è selezionata.  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>Specificare delimitatori di riga e di colonna per l'output
 **Delimitatore di riga**  
 Selezionare dall'elenco i delimitatori per separare le righe nell'output. Non è possibile specificare un delimitatore di riga *personalizzato*.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**{CR}{LF}**|Consente di delimitare le righe con una combinazione di caratteri ritorno a capo/avanzamento riga.|  
|**{CR}**|Consente di delimitare le righe con un ritorno a capo.|  
|**{LF}**|Consente di delimitare le righe con un avanzamento riga.|  
|**Punto e virgola {;}**|Consente di delimitare le righe con un punto e virgola.|  
|**Due punti {:}**|Consente di delimitare le righe con i due punti.|  
|**Virgola {,}**|Delimitare le righe con una virgola.|  
|**Tabulazione {t}**|Consente di delimitare le righe con una tabulazione.|  
|**Barra verticale {&#124;}**|Consente di delimitare le righe con una barra verticale.|  
  
 **Delimitatore di colonna**  
 Selezionare dall'elenco i delimitatori per separare le colonne nell'output. Non è possibile specificare un delimitatore di colonna *personalizzato*.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**{CR}{LF}**|Consente di delimitare le colonne con una combinazione di caratteri ritorno a capo/avanzamento riga.|  
|**{CR}**|Consente di delimitare le colonne con un ritorno a capo.|  
|**{LF}**|Consente di delimitare le colonne con un avanzamento riga.|  
|**Punto e virgola {;}**|Consente di delimitare le colonne con un punto e virgola.|  
|**Due punti {:}**|Consente di delimitare le colonne con i due punti.|  
|**Virgola {,}**|Consente di delimitare le colonne con una virgola.|  
|**Tabulazione {t}**|Consente di delimitare le colonne con una tabulazione.|  
|**Barra verticale {&#124;}**|Consente di delimitare le colonne con una barra verticale.|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Facoltativamente, rivedere i mapping delle colonne e visualizzare in anteprima i dati

**Modifica mapping**   
Facoltativamente, fare clic su **Modifica mapping** per visualizzare la finestra di dialogo **Mapping colonne** per la tabella selezionata. Nella finestra di dialogo **Mapping colonne** eseguire le operazioni seguenti.
-   Esaminare il mapping di singole colonne tra l'origine e la destinazione.
-   Copiare solo un subset di colonne selezionando **ignora** per le colonne da non copiare.

Per altre informazioni, vedere [Mapping colonne](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Anteprima**  
Facoltativamente, fare clic su **Anteprima** per visualizzare in anteprima fino a 200 righe di dati di esempio nella finestra di dialogo **Anteprima dati**. Questo permette di verificare che la procedura guidata sta per copiare i dati desiderati. Per altre informazioni, vedere [Anteprima dati](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Dopo aver visualizzato i dati in anteprima, potrebbe essere necessario modificare le opzioni selezionate nelle pagine precedenti della procedura guidata. Per apportare queste modifiche, tornare alla pagina **Configurare la destinazione del file flat** e quindi fare clic su **Indietro** per tornare alle pagine precedenti nelle quali modificare le opzioni selezionate.  

## <a name="whats-next"></a>Quali sono le operazioni successive?  
 Dopo aver specificato le opzioni di formattazione per il file flat di destinazione, la pagina successiva è **Salvare ed eseguire il pacchetto**. In questa pagina specificare se eseguire immediatamente l'operazione. A seconda della configurazione, è anche possibile salvare le proprie informazioni come pacchetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per personalizzarlo e usarlo di nuovo in seguito. Per altre informazioni, vedere [Salvare ed eseguire il pacchetto](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  

