---
title: Scelta destinazione (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3ebfc24eef8919ffa43824447ae32773d106158f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65723972"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>Scelta destinazione (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 Dopo aver fornito informazioni sull'origine dei dati e su come connettersi a tale origine, nell'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene visualizzata l'opzione **Scegliere una destinazione**. In questa pagina fornire informazioni sulla destinazione per i dati e su come connettersi a tale destinazione.
  
Per informazioni sulle destinazioni di dati che è possibile usare, vedere [Quali origini e destinazioni di dati è possibile usare?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources). 

## <a name="screen-shot-of-the-destination-page"></a>Screenshot della pagina Destinazione
Lo screenshot seguente mostra la prima parte della pagina **Scegliere una destinazione** della procedura guidata. Il resto della pagina presenta un numero variabile di opzioni che variano a seconda della destinazione scelta qui.

![Scegli destinazione](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>Scegliere una destinazione
 **Destinazione**  
 Specificare la destinazione selezionando il provider di dati che può importare i dati nella destinazione.
 
-   **Il provider di dati necessario risulta in genere chiaro dal nome**, perché il nome del provider contiene di solito il nome della destinazione, ad esempio *Destinazione file flat*, Microsoft *Excel*, Microsoft *Access*, Provider di dati .NET Framework per *SQL Server*, Provider di dati .NET Framework per *Oracle*.

-   **Se si ha un driver ODBC per la destinazione**, selezionare Provider di dati .NET Framework per ODBC, quindi immettere le informazioni specifiche del driver. I driver ODBC non sono presenti nell'elenco a discesa delle destinazioni. Il provider di dati .Net Framework per ODBC funge da wrapper per il driver ODBC. Per altre informazioni, vedere [Connettersi a un'origine dati ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Possono essere disponibili più provider per la destinazione.** In genere, è possibile selezionare qualsiasi provider che funziona con la destinazione. Ad esempio, per connettersi a Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile usare il provider di dati .NET Framework per SQL Server o il driver ODBC di SQL Server. Nell'elenco sono presenti anche altri provider che però non sono più supportati. 

## <a name="my-destination-isnt-in-the-list"></a>La destinazione non è nell'elenco
-   **Può essere necessario scaricare il provider di dati** da Microsoft o da terze parti. L'elenco dei provider di dati disponibili nell'elenco **Destinazione** include solo i provider installati nel computer. Per informazioni sulle destinazioni che è possibile usare, vedere [Quali origini e destinazioni è possibile usare?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **È disponibile un driver ODBC per la destinazione?** I driver ODBC non sono presenti nell'elenco a discesa delle destinazioni. Se si ha un driver ODBC per la destinazione, selezionare Provider di dati .NET Framework per ODBC, quindi immettere le informazioni specifiche del driver. Il provider di dati .Net Framework per ODBC funge da wrapper per il driver ODBC. Per altre informazioni, vedere [Connettersi a un'origine dati ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Provider a 32 bit e a 64 bit.** Se è in esecuzione la procedura guidata a 64 bit, non vengono visualizzate le destinazioni per cui è installato solo un provider a 32 bit e viceversa.

> [!NOTE]
> Per usare la versione a 64 bit per l'importazione e l'esportazione guidate di SQL Server, è necessario installare SQL Server. SQL Server Data Tools (SSDT) e SQL Server Management Studio (SSMS) sono applicazioni a 32 bit e installano solo i file a 32 bit, inclusa la versione a 32 bit della procedura guidata.

## <a name="after-you-choose-a-destination"></a>Dopo aver scelto una destinazione
Dopo aver scelto una destinazione, il resto della pagina **Scegliere una destinazione** ha un numero variabile di opzioni che dipendono dal provider di dati scelto.

Per connettersi a una destinazione di uso comune, vedere una delle pagine seguenti.
-   [Connettersi a SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Connettersi a Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Connettersi a file flat (file di testo)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Connettersi a Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Connettersi ad Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Connettersi con ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Connettersi ad Archiviazione BLOB di Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Connettersi a PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Connettersi a MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

Per informazioni su come connettersi a una destinazione non elencata qui, vedere [The Connection Strings Reference](https://www.connectionstrings.com/). Questo sito di terze parti contiene stringhe di connessione di esempio e altre informazioni sui provider di dati e sulle informazioni di connessione richieste dai provider.

## <a name="whats-next"></a>Quali sono le operazioni successive?  
 Dopo aver fornito informazioni sulla destinazione dei dati e su come connettersi a tale destinazione, la pagina successiva è **Impostazione copia tabella o query**. In questa pagina è possibile specificare se si vuole copiare un'intera tabella o solo alcune righe. Per altre informazioni, vedere [Impostazione copia tabella o query](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Vedere anche
[Iniziare con questo semplice esempio dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


