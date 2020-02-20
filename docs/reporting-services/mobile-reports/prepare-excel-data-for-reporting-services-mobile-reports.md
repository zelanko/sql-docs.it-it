---
title: Preparare i dati di Excel per i report per dispositivi mobili di Reporting Services | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 16698f8d-bfc7-4eca-9e97-82c99d8bc08e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9285b9b89930fe540f9b5493f1730184cf4e9526
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "62499945"
---
# <a name="prepare-excel-data-for-reporting-services-mobile-reports"></a>Preparare i dati di Excel per i report per dispositivi mobili di Reporting Services
  
Ecco alcuni aspetti da prendere in considerazione durante la preparazione di un file e dei fogli di lavoro Excel da usare per un report per dispositivi mobili:  
  
## <a name="do"></a>Cosa fare  
  
- Preparare un foglio di lavoro per ogni set di dati.  
- Disporre le intestazioni di colonna nella prima riga.  
- Garantire coerenza tra i tipi di dati all'interno di ogni colonna.  
- Formattare le celle in Excel con il tipo corretto.  
- Disporre i dati nei fogli di lavoro e non nel modello di dati di Excel.  
- Quando si usano le formule, verificare che l'intera colonna venga calcolata usando la stessa formula.  
- Usare Excel 2007 o versione successiva.  
- Salvare i file di Excel con estensione XLSX.  
          
## <a name="dont"></a>Cosa non fare  
  
- Includere immagini, grafici, tabelle pivot o altri oggetti incorporati nei fogli di lavoro del set di dati.  
- Inserire righe totali o calcolate.  
- Lasciare il file aperto in Excel durante l'importazione.  
- Formattare i numeri manualmente aggiungendo simboli di valuta o altri simboli.  
- Usare una cartella di lavoro con i dati archiviati nel modello di dati.  
  
## <a name="worksheets"></a>Fogli di lavoro  
          
Quando si prepara un file di Excel come set di dati per un report per dispositivi mobili, verificare di avere un solo set di dati per ogni foglio di lavoro. Ogni singolo foglio di lavoro viene importato in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] come tabella separata. I fogli di lavoro con nome uguale provenienti da più origini di Excel vengono rinominati in fase di importazione aggiungendo i numeri incrementali. Se ad esempio una cartella di lavoro dispone di tre fogli di lavoro con nome "MyWorksheet", il secondo e il terzo verranno rinominati "MyWorksheet0" e "MyWorksheet1". La schermata seguente illustra le prime righe di un foglio di Excel ideale e pronto per l'importazione.  
  
![SS_MRP_ExcelDataSheet](../../reporting-services/mobile-reports/media/ss-mrp-exceldatasheet.png)  
          
## <a name="column-headers"></a>Intestazioni di colonna  
  
Come si può notare nell'esempio precedente, la prima riga contiene il nome della metrica della rispettiva colonna. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] consente di mantenere le intestazioni delle colonne per semplificarne la consultazione all'interno delle impostazioni dell'elemento della raccolta. Tuttavia, le intestazioni delle colonne non sono obbligatorie. In assenza, [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] genera le intestazioni usando la convenzione di Excel A,B,C,...,AA,BB,...  
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] rileva automaticamente le intestazioni della prima riga durante l'importazione dei fogli di lavoro di Excel tramite il confronto tra i tipi di dati delle prime due celle di ogni colonna. Se i tipi di dati delle prime due celle di qualsiasi colonna non corrispondono, la prima riga viene assegnata per contenere le intestazioni di colonna. Se una tabella è dotata di intestazioni di colonna numeriche, assegnare un prefisso ai nomi delle intestazioni aggiungendo una stringa in modo che possano essere rilevate come intestazioni nel processo di importazione.  
  
## <a name="cells"></a>Celle  
  
I dati contenuti nelle celle di ogni colonna del set di dati del foglio di lavoro devono essere coerenti. In fase di importazione, a ogni colonna viene assegnato un tipo di dati. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] rileva automaticamente i tipi di dati come stringa, double (numerico), booleano (true/false) o datetime. Tipi di dati misti nella stessa colonna possono causare impossibilità di rilevamento o generare rilevamenti non accurati. Questo rilevamento rappresenta la possibilità che le intestazioni di colonna siano di tipo stringa. Le celle devono essere formattate con il tipo corretto in Excel per garantire che [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] rilevi i tipi desiderati. Nell'esempio precedente, le sei colonne sarebbero suddivise come segue:  
*  Una colonna datetime  
*  Una colonna stringa  
*  Quattro colonne double  
  
Se un foglio di lavoro contiene formule o celle calcolate, solo il valore di visualizzazione risultante verrà importato in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].  
  
## <a name="file-location-and-refreshing-excel-data"></a>Percorso del file e aggiornamento dei dati di Excel  
  
Non esistono restrizioni sul percorso di archiviazione dei file Excel da importare in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]. Tuttavia, se si sposta o si rinomina il file dopo l'importazione, non sarà possibile aggiornare i dati tramite il comando **Aggiorna tutti i dati** della visualizzazione dati.   
  
>**Nota**: [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] non aggiorna i dati di Excel in automatico. È possibile aggiornare i dati con il comando **Aggiorna** di [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)], ma solo se il file non è stato spostato.  
  
## <a name="dates"></a>Date  
  
I campi data sono essenziali per molti report per dispositivi mobili. Per questo motivo è importante garantire che le celle in Excel vengano formattate correttamente come date. In alcuni casi potrebbe essere necessaria una conversione. Di seguito sono riportati esempi di formule per la conversione delle celle da testo a date in Excel.  
  
    Week 24-2013=DATE(MID(A2,9,4),1,-2)-WEEKDAY(DATE(MID(A2,9,4),1,3))+MID(A2,6,2)*7  
  
    2013/03/21=DATEVALUE(A1)  
  
    2013-mar-12=DATEVALUE(RIGHT(A1,2)&"-"&MID(A1,6,3)&"-"&LEFT(A1,4))  
  
Dopo aver convertito le celle, è necessario formattarle come date selezionando le singole celle o l'intera colonna > menu **di scelta rapida** > **Formato celle** > **Data** dall'elenco **Categoria**. Per convertire le celle testo in date correttamente formattate, è anche possibile usare la procedura guidata per la conversione delle colonne di formato testo su Excel.  
  
## <a name="unsupported"></a>Non supportato  
  
I dati del foglio di lavoro in formati diversi da quelli descritti in precedenza potrebbero provocare risultati imprevisti durante l'importazione. È consigliabile limitare i fogli di lavoro in un file di Excel solo ai dati in formato corretto da usare con un report per dispositivi mobili.  
  
Gli oggetti personalizzati nei fogli di lavoro di Excel, tra cui tabelle pivot, grafici e immagini, non vengono importati in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].  
  
### <a name="see-also"></a>Vedere anche  
- [Preparare i dati per i report per dispositivi mobili di Reporting Services](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)  
- [Creare e pubblicare report per dispositivi mobili con SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  Vedere [Visualizzare report per dispositivi mobili e indicatori KPI di SQL Server nell'app iPad](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI per iOS)  
-  [Visualizzare report per dispositivi mobili e indicatori KPI di SQL Server nell'app iPhone](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI per iOS)  
  
  
  
  
  
  
  

