---
title: Finestra di dialogo Anteprima dati (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.previewdata.f1
ms.assetid: 423ac26a-ba02-4fdf-88b4-07995fe4a97e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: feeef370bc64697e3fa9ef3a279e31ba047301fd
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296315"
---
# <a name="preview-data-dialog-box-sql-server-import-and-export-wizard"></a>Finestra di dialogo Anteprima dati (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Dopo aver specificato i dati che si desidera copiare, è possibile scegliere facoltativamente **Anteprima** per aprire la finestra di dialogo **Anteprima dati** . In questa pagina è possibile visualizzare in anteprima fino a 200 righe di dati di esempio dall'origine dati. Questo permette di verificare che la procedura guidata sta per copiare i dati desiderati.
  
## <a name="screen-shot-of-the-preview-data-page"></a>Screenshot della pagina Anteprima dati 
 L'immagine riportata di seguito illustra la finestra di dialogo **Anteprima dati** della procedura guidata.  
 
![Pagina Anteprima dati dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/media/preview-data.png "Pagina Anteprima dati dell'Importazione/Esportazione guidata")  
  
## <a name="preview-sample-data"></a>Visualizzare in anteprima i dati di esempio  
 **Origine**  
Visualizza la query usata dalla procedura guidata per caricare i dati dall'origine dati.

Se è stata selezionata una tabella da copiare, il campo **Origine** mostra una query `SELECT * FROM <table>` anziché il nome della tabella. 
  
 **Griglia Dati di esempio**  
 Visualizza fino a 200 righe di dati di esempio dell'origine dati restituite dalla query.  


## <a name="thats-not-right-i-want-to-change-something"></a>Se sono necessarie modifiche
Dopo aver visualizzato i dati in anteprima, potrebbe essere necessario modificare le opzioni selezionate nelle pagine precedenti della procedura guidata. Per apportare queste modifiche, fare clic su **OK** per tornare alla pagina **Seleziona tabelle e viste di origine** e quindi fare clic su **Indietro** per tornare alle pagine precedenti in cui modificare le opzioni selezionate.

## <a name="whats-next"></a>Quali sono le operazioni successive?  
 Dopo aver visualizzato in anteprima i dati che si stanno per copiare e aver fatto clic su **OK**, la finestra di dialogo **Anteprima dati** consente di tornare alla pagina **Seleziona tabelle e viste di origine** o **Configurare la destinazione del file flat** . Per altre informazioni, vedere [Seleziona tabelle e viste di origine](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) o [Configurare la destinazione del file flat](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Vedere anche
[Iniziare con questo semplice esempio dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)
