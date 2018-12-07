---
title: Scaricare SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 09/28/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
keywords:
- installare ssdt, scaricare ssdt, versione più recente di ssdt
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 3067b05783d7a83118e87dc8db4cdc6a83d40a1c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515996"
---
# <a name="download-and-install-sql-server-data-tools-ssdt-for-visual-studio"></a>Scaricare e installare SQL Server Data Tools (SSDT) per Visual Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

> [!div class="nextstepaction"]
> [Contribuisci a migliorare la documentazione di SQL Server](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

**SQL Server Data Tools** è uno strumento di sviluppo moderno che consente di compilare database relazionali SQL Server, database SQL di Azure, modelli di dati di Analysis Services (AS), pacchetti di Integration Services (IS) e report di Reporting Services (RS). Con SSDT è possibile progettare e distribuire qualsiasi tipo di contenuto SQL Server con la stessa facilità con la quale si sviluppa un'applicazione in Visual Studio.

*Per la maggior parte degli utenti, SQL Server Data Tools (SSDT) viene installato durante l'installazione di Visual Studio. Se si installa SSDT usando il programma di installazione di Visual Studio, vengono aggiunte le funzionalità SSDT di base. È pertanto necessario eseguire il [programma di installazione di SSDT autonomo](#ssdt-for-vs-2017-standalone-installer) per ottenere AS, IS ed RS.*

## <a name="install-ssdt-with-visual-studio-2017"></a>Installare SSDT con Visual Studio 2017

Per installare SSDT durante l'[installazione di Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio), selezionare il carico di lavoro **Elaborazione ed archiviazione dati** e quindi selezionare **SQL Server Data Tools**. Se Visual Studio è già installato, è possibile [modificare l'elenco dei carichi di lavoro](https://docs.microsoft.com/visualstudio/install/modify-visual-studio) per includere SSDT: ![Carico di lavoro Elaborazione ed archiviazione dati](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload.png)



## <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>Installare Analysis Services, Integration Services e Reporting Services
Per installare AS, IS ed RS come supporto per i progetti, eseguire il [programma di installazione di SSDT autonomo](#ssdt-for-vs-2017-standalone-installer). 

Il programma di installazione elenca le istanze di Visual Studio disponibili per l'aggiunta degli strumenti di SSDT. Se Visual Studio non è installato, selezionando **Install a new SQL Server Data Tools instance** (Installa una nuova istanza di SQL Server Data Tools) è possibile installare SSDT con una versione minima di Visual Studio. Per un'esperienza ottimale, tuttavia, è consigliabile usare SSDT con [la versione più recente di Visual Studio](https://www.visualstudio.com/downloads). 

![Selezionare AS, IS, RS](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)



## <a name="ssdt-for-vs-2017-standalone-installer"></a>SSDT per Visual Studio 2017 (programma di installazione autonomo)

[![download](../ssdt/media/download.png) Download di SSDT per Visual Studio 2017 (15.8.2) ](https://go.microsoft.com/fwlink/?linkid=2038031) 

> [!IMPORTANT]
> - Prima di installare SSDT per Visual Studio 2017 (15.8.2), disinstallare le estensioni *Progetti di Analysis Services* e *Progetti di Reporting Services*, se già installate, e chiudere tutte le istanze di Visual Studio.
> - È stato risolto un problema relativo alla distribuzione di progetti SSIS contenenti pacchetti con Attività script/Destinazione file flat in Azure-SSIS che impedisce l'esecuzione dei pacchetti in Azure-SSIS.
> - SSDT per Visual Studio 2017 (15.8.2) non supporta gli strumenti per la progettazione contenenti un'origine/destinazione Oracle/Teradata. Usare SSDT per Visual Studio 2017 (15.8).



**Informazioni sulla versione**  
  
Numero di versione: 15.8.2  
Numero di build: 14.0.16182.0  
Data versione: 5 novembre 2018  

Per un elenco completo delle modifiche, vedere il [log delle modifiche](changelog-for-sql-server-data-tools-ssdt.md).

SSDT per Visual Studio 2017 ha gli stessi [requisiti di sistema](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs) di Visual Studio.  

### <a name="available-languages---ssdt-for-vs-2017"></a>Lingue disponibili - SSDT per VS 2017

Questa versione di **SSDT per VS 2017** può essere installata nelle lingue seguenti:  

[Cinese (semplificato)]( https://go.microsoft.com/fwlink/?linkid=2038031&clcid=0x804) | 
[Cinese (tradizionale)]( https://go.microsoft.com/fwlink/?linkid=2038031&clcid=0x404) | 
[Inglese (Stati Uniti)]( https://go.microsoft.com/fwlink/?linkid=2038031&clcid=0x409) | 
[Francese]( https://go.microsoft.com/fwlink/?linkid=2038031&clcid=0x40c)  
[Tedesco]( https://go.microsoft.com/fwlink/?linkid=2038031&clcid=0x407) | 
[Italiano]( https://go.microsoft.com/fwlink/?linkid=2038031&clcid=0x410) | 
[Giapponese]( https://go.microsoft.com/fwlink/?linkid=2038031&clcid=0x411) | 
[Coreano]( https://go.microsoft.com/fwlink/?linkid=2038031&clcid=0x412) | 
[Portoghese (Brasile)]( https://go.microsoft.com/fwlink/?linkid=2038031&clcid=0x416) | 
[Russo]( https://go.microsoft.com/fwlink/?linkid=2038031&clcid=0x419) | 
[Spagnolo]( https://go.microsoft.com/fwlink/?linkid=2038031&clcid=0x40a)  


## <a name="offline-install"></a>Eseguire l'installazione offline

Per installare SSDT quando non si è connessi a Internet, seguire la procedura descritta in questa sezione. Per altre informazioni, vedere [Creare un'installazione di rete di Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/create-a-network-installation-of-visual-studio).

Per prima cosa, completare la procedura seguente mentre si è connessi:

1. [Scaricare il programma di installazione autonomo di SSDT](#ssdt-for-vs-2017-standalone-installer).
2. [Scaricare vs_sql.exe](https://aka.ms/vs/15/release/vs_sql.exe).
3. Mentre si è ancora online, eseguire uno dei comandi seguenti per scaricare tutti i file necessari per l'installazione offline. L'uso dell'opzione `--layout` è fondamentale, scaricherà i file effettivi per l'installazione offline. Sostituire <filepath> con il tracciato di layout effettivo in cui salvare i file.

   
   A.   Per una lingua specifica, passare le impostazioni locali: `vs_sql.exe --layout c:\<filepath> --lang en-us` (una sola lingua corrisponde a circa 1 GB)  
   B. Per tutte le lingue, omettere l'argomento `--lang`: `vs_sql.exe --layout c:\<filepath>` (tutte le lingue corrispondono a circa 3,9 GB).

4. Eseguire `SSDT-Setup-ENU.exe /layout c:\<filepath>` per estrarre il payload SSDT nella stessa posizione `<filepath>` in cui sono stati scaricati i file di VS2017. Ciò garantisce che tutti i file di entrambe le cartelle vengano combinati in una cartella di layout singola.

Dopo aver completato questa procedura, quanto segue può essere eseguito offline:

1. Eseguire `vs_setup.exe --NoWeb` per installare la shell di Visual Studio 2017 e il progetto di dati di SQL Server.
2. Dalla cartella di layout eseguire `SSDT-Setup-ENU.exe /install` e selezionare SSIS/SSRS/SSAS.

   - Oppure, per un'installazione automatica, eseguire `SSDT-Setup-ENU.exe /INSTALLALL[:vsinstances] /passive`  

Per le opzioni disponibili, eseguire `SSDT-Setup-ENU.exe /help`

## <a name="supported-sql-versions"></a>Versioni di SQL supportate
  
|Modelli di progetto|Piattaforme SQL supportate|  
|-------------------|--------------------|  
Database relazionali|  SQL Server 2005* - SQL Server 2017<br> (usare SSDT 17.x o SSDT per Visual Studio 2017 per la connessione a [SQL Server in Linux](../linux/sql-server-linux-overview.md))<br /><br />Database SQL di Azure<br /><br />Azure SQL Data Warehouse (supporta solo query, i progetti di database non sono ancora supportati)<br /><br />  * Il supporto per SQL Server 2005 è deprecato<br /><br /> e si consiglia di passare a una versione di SQL supportata ufficialmente|
  |Modelli di Analysis Services<br /><br />Report di Reporting Services | SQL Server 2008 - SQL Server 2017|
  |pacchetti di Integration Services| SQL Server 2012 - SQL Server 2017    |
  
## <a name="dacfx"></a>DacFx
SSDT per Visual Studio 2015 e SSDT per Visual Studio 2017 usano entrambi DacFx 17.4.1: [scaricare Data-Tier Application Framework (DacFx) 17.4.1](https://www.microsoft.com/download/details.aspx?id=56508).

## <a name="previous-versions"></a>Versioni precedenti

Per scaricare e installare SSDT per Visual Studio 2015 o una versione precedente di SSDT, vedere [Versioni precedenti di SQL Server Data Tools (SSDT e SSDT-BI)](previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md).



## <a name="next-steps"></a>Passaggi successivi  
Dopo l'installazione di SSDT, consultare queste esercitazioni per imparare a creare database, pacchetti, modelli di dati e report mediante SSDT:  

- [Sviluppo di database offline orientato ai progetti](project-oriented-offline-database-development.md)  
- [Esercitazione SSIS: Creare un pacchetto ETL semplice](../integration-services/ssis-how-to-create-an-etl-package.md)  
- [Esercitazioni su Analysis Services](../analysis-services/analysis-services-tutorials-ssas.md)  
- [Creare un report tabella semplice (esercitazione su SSRS)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]


## <a name="see-also"></a>Vedere anche  
[Forum MSDN di SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[Blog del Team di SSDT](https://blogs.msdn.com/b/ssdt/)  
[Riferimento all'API DACFx](https://msdn.microsoft.com/library/dn645454.aspx)  
[Scaricare SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
