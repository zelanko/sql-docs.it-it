---
title: Scelta destinazione (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 50c9419911f83c98fba5baf0f995ffbeafb916ad
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965651"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>Scelta destinazione (Importazione/Esportazione guidata SQL Server)
  Utilizzare la pagina **scegliere una destinazione** per specificare la destinazione dei dati che si desidera copiare.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [SQL Server importazione/esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per informazioni sulle opzioni di avvio della procedura guidata, nonché sulle autorizzazioni necessarie per eseguire la procedura guidata, vedere [eseguire l'importazione/esportazione guidata SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo dell'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste nel copiare i dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="static-options"></a>Opzioni statiche  
 **Destinazione**  
 Consente di scegliere il provider di dati corrispondente al formato di archiviazione dei dati della destinazione. Potrebbero essere disponibili più provider per l'origine dati. Ad esempio, con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client, il .NET Framework provider di dati per SQL Server o il Provider Microsoft OLE DB per SQL Server.  
  
> [!NOTE]  
>  Per salvare i dati in una destinazione ODBC, selezionare Provider di dati .NET Framework per ODBC.  
  
 La proprietà **origine dati** presenta un numero variabile di opzioni che variano a seconda dei provider installati nel computer. Nella tabella seguente vengono illustrate le opzioni relative ad alcune destinazioni comunemente utilizzate. Per altri provider, consultare la documentazione specifica.  
  
## <a name="dynamic-options"></a>Opzioni dinamiche  
 Nelle sezioni seguenti vengono descritte le opzioni disponibili per diverse origini dei dati. Non sono descritte tutte le destinazioni disponibili nell'elenco a discesa Destinazione.  
  
### <a name="destination--sql-server-native-client-or-microsoft-ole-db-provider-for-sql-server"></a>Destinazione = SQL Server Native Client o Provider Microsoft OLE DB per SQL Server  
 **Nome server**  
 Consente di digitare il nome del server di destinazione dei dati oppure di sceglierne uno nell'elenco.  
  
 **Usa autenticazione di Windows**  
 Consente di specificare se il pacchetto deve utilizzare l'autenticazione di Microsoft Windows per l'accesso al database. Per una maggiore sicurezza è consigliabile utilizzare l'autenticazione di Windows.  
  
 **Usa autenticazione SQL Server**  
 Consente di specificare se per l'accesso al database del pacchetto deve essere utilizzata l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario specificare un nome utente e una password.  
  
 **Nome utente**  
 Consente di specificare un nome utente per la connessione al database quando si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Password**  
 Consente di specificare una password per la connessione al database quando si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Database**  
 Consente di selezionare dall'elenco di database nell'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure di creare un nuovo database facendo clic su **nuovo**.  
  
 **Refresh** (Aggiornamento)  
 Consente di ripristinare l'elenco dei database disponibili facendo clic su **Aggiorna**.  
  
 **Nuovo**  
 Consente di creare un nuovo database di destinazione utilizzando la finestra di dialogo **Crea database** .  
  
### <a name="destination--flat-file-destination"></a>Destinazione = Destinazione file flat  
 **Nome file**  
 Consente di specificare il percorso e il nome del file in cui archiviare i dati. In alternativa, è possibile fare clic su **Sfoglia** per individuare un file.  
  
 **Sfoglia**  
 Consente di individuare un file tramite la finestra di dialogo **Apri**.  
  
 **Locale**  
 Consente di specificare l'ID delle impostazioni locali (LCID) che definisce il tipo di ordinamento dei caratteri e i formati di data e ora.  
  
 **Unicode**  
 Indica se utilizzare il formato Unicode. Se si utilizza il formato Unicode, non è necessario specificare una tabella codici.  
  
 **Tabella codici**  
 Consente di specificare la tabella codici per la lingua che si desidera utilizzare.  
  
 **Formato**  
 Consente di indicare se utilizzare la formattazione non allineata a destra, a larghezza fissa o delimitata.  
  
|valore|Description|  
|-----------|-----------------|  
|Delimitato|Le colonne sono separate da un delimitatore specificato nella pagina **Colonne** .|  
|File a larghezza fissa|Le colonne hanno una larghezza fissa.|  
|Non allineato a destra|I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa ad eccezione dell'ultima, per la quale viene utilizzato il delimitatore di riga.|  
  
 **Qualificatore di testo**  
 Consente di impostare il qualificatore di testo da utilizzare. È possibile, ad esempio, specificare che ogni colonna di testo sia racchiusa tra virgolette.  
  
 **Nomi di colonne nella prima riga di dati**  
 Consente di indicare se si desidera visualizzare i nomi delle colonne nella prima riga di dati.  
  
### <a name="destination--microsoft-excel"></a>Destinazione = Microsoft Excel  
  
> [!NOTE]  
>  Selezionare **Microsoft Excel** solo se si desidera connettersi a un'origine dati che utilizza Excel 2003 o versioni precedenti. Per connettersi a un'origine dati che utilizza Excel 2007, selezionare **Microsoft Office 12,0 accesso motore di database Provider OLE DB**, fare clic su **Proprietà**e quindi nella scheda **tutte** della finestra di dialogo **proprietà di data link** , per **proprietà estese**, immettere `Excel 12.0` .  
  
 **Percorso file di Excel**  
 Specificare il percorso e il nome file per la cartella di lavoro in cui archiviare i dati, ad esempio C:\MyData.xls \\\Sales\Database\Northwind.xls. In alternativa, è possibile fare clic su **Sfoglia** per individuare una cartella di lavoro.  
  
 **Sfoglia**  
 Individuare una cartella di lavoro di Excel utilizzando la finestra di dialogo **Apri** .  
  
 **Versione di Excel**  
 Consente di selezionare la versione di Excel utilizzata dalla cartella di lavoro di destinazione.  
  
> [!NOTE]  
>  Quando si esportano dati in una destinazione [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] , nella procedura guidata viene utilizzato il componente Destinazione Excel di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per informazioni su alcune considerazioni sull'utilizzo e sui problemi noti, vedere [Excel Destination](../data-flow/excel-destination.md).  
  
### <a name="destination--microsoft-access"></a>Destinazione = Microsoft Access  
  
> [!NOTE]  
>  Selezionare **Microsoft Access** solo se si desidera connettersi a un database che utilizza Access 2003 o versione precedente. Per connettersi a un database che usa Access 2007, selezionare **Microsoft Office 12,0 access motore di database OLE DB provider**.  
  
 **Nome file**  
 Specificare il percorso e il nome del file di database in cui archiviare i dati, ad esempio C:\MyData.mdb, \\ \Sales\Database\Northwind.mdb. In alternativa, è possibile fare clic su **Sfoglia** per individuare un file di database.  
  
 **Sfoglia**  
 Individuare il file di database utilizzando la finestra di dialogo **Apri** .  
  
 **Nome utente**  
 Consente di specificare un nome utente valido per la connessione al database quando un file di informazioni sul gruppo di lavoro corrente è associato al database.  
  
 **Password**  
 Consente di specificare la password dell'utente per la connessione al database quando un file di informazioni sul gruppo di lavoro corrente è associato al database. Se tuttavia il database è protetto con un'unica password valida per tutti gli utenti, è necessario specificare tale valore nella finestra di dialogo **Proprietà di Data Link** a cui è possibile accedere facendo clic sul pulsante **Avanzate** .  
  
 **Avanzate**  
 Consente di specificare le opzioni avanzate, ad esempio la password del database o un file di informazioni sul gruppo di lavoro diverso da quello predefinito, mediante la finestra di dialogo **Proprietà di Data Link**. Per ulteriori informazioni sulle proprietà del provider OLE DB, vedere la sezione relativa all'accesso ai dati di MSDN Library all'indirizzo [MSDN Library](https://go.microsoft.com/fwlink/?linkid=62553).  
  
  
