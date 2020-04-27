---
title: Scelta origine dati (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b6e399cf6c145f36febd9b32ae7a84c54741bb43
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62893596"
---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>Scelta origine dati (Importazione/Esportazione guidata SQL Server)
  Utilizzare la pagina **scegliere un'origine dati** per specificare l'origine dei dati che si desidera copiare.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [SQL Server importazione/esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per informazioni sulle opzioni per avviare la procedura guidata e sulle autorizzazioni necessarie per eseguire la procedura guidata, vedere [eseguire l'importazione/esportazione guidata SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo dell'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste nel copiare i dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
 **Origine dati**  
 Selezionare il provider di dati corrispondente al formato di archiviazione dell'origine. Potrebbero essere disponibili più provider per l'origine dati. Ad esempio, con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, il .NET Framework provider di dati per SQL Server o il Provider Microsoft OLE DB per SQL Server.  
  
 La proprietà **origine dati** presenta un numero variabile di opzioni che dipendono dai provider installati nel computer. Nelle tabelle seguenti vengono elencate le opzioni disponibili per alcune destinazioni utilizzate frequentemente. Per altri provider, consultare la documentazione specifica.  
  
## <a name="dynamic-options"></a>Opzioni dinamiche  
 Nelle sezioni seguenti vengono descritte le opzioni disponibili per diverse origini dei dati. Non tutte le origini dei dati disponibili nell'elenco a discesa Origine dati sono descritte in queste sezioni.  
  
### <a name="data-source--sql-server-native-client-and-microsoft-ole-db-provider-for-sql-server"></a>Origine dati = SQL Server Native Client e Provider Microsoft OLE DB per SQL Server  
 **Nome server**  
 Consente di digitare il nome del server che contiene i dati o di scegliere un server dall'elenco.  
  
 **Usa autenticazione di Windows**  
 Consente di specificare se per l'accesso al database del pacchetto deve essere utilizzata l'autenticazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Per una maggiore sicurezza è consigliabile utilizzare l'autenticazione di Windows.  
  
 **Usa autenticazione SQL Server**  
 Consente di specificare se per l'accesso al database del pacchetto deve essere utilizzata l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario specificare un nome utente e una password.  
  
 **Nome utente**  
 Consente di specificare un nome utente per la connessione al database quando si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Password**  
 Consente di specificare una password per la connessione al database quando si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Database**  
 Consente di selezionare uno dei database nell'elenco nell'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Aggiorna**  
 Consente di ripristinare l'elenco dei database disponibili facendo clic su **Aggiorna**.  
  
### <a name="data-source--net-framework-data-provider-for-sql-server"></a>Origine dati = Provider di dati .NET Framework per SQL Server  
 In questa pagina viene visualizzato un elenco in ordine alfabetico delle opzioni per il provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le opzioni più importanti sono elencate nella tabella seguente.  
  
 **Origine dati**  
 Consente di digitare il nome del server che contiene i dati o di scegliere un server dall'elenco.  
  
 **Catalogo iniziale**  
 Consente di digitare il nome del database di origine.  
  
 **Sicurezza integrata**  
 Consente di specificare `True` per stabilire la connessione tramite l'autenticazione integrata di Windows, che rappresenta la soluzione consigliata, oppure `False` per stabilire la connessione tramite l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si specifica `False`, è necessario immettere un ID utente e una password. Il valore predefinito è `False`.  
  
 **ID utente**  
 Consente di specificare un nome utente per la connessione al database quando si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Password**  
 Consente di specificare una password per la connessione al database quando si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Le altre opzioni che vengono elencate quando si seleziona questo provider non sono necessarie per stabilire correttamente la connessione al database di origine di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per una descrizione di tali opzioni, vedere la documentazione per il provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel Software Development Kit di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
### <a name="data-source--microsoft-excel"></a>Origine dati = Microsoft Excel  
  
> [!NOTE]  
>  Selezionare **Microsoft Excel** solo se si desidera connettersi a un'origine dati che utilizza Excel 2003 o versioni precedenti. Per connettersi a un'origine dati che utilizza Excel 2007, selezionare **Microsoft Office 12,0 accesso motore di database Provider OLE DB**, fare clic su **Proprietà**e quindi nella **scheda tutte** della finestra di dialogo **proprietà di data link** immettere `Excel 12.0` come valore per **proprietà estese**.  
  
 **Percorso file di Excel**  
 Consente di specificare il percorso e il nome file del foglio di calcolo dal quale si importano i dati. Ad esempio, **C:\MyData.xls, \\\Sales\Database\Northwind.xls**. In alternativa, fare clic su **Sfoglia**.  
  
 **Sfoglia**  
 Consente di individuare il foglio di calcolo tramite la finestra di dialogo **Apri**.  
  
 **Versione di Excel**  
 Consente di selezionare la versione di Excel utilizzata per l'archiviazione dei dati di origine.  
  
> [!NOTE]  
>  Quando si importano dati da un'origine [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)], nella procedura guidata viene utilizzato il componente Origine Excel di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Per informazioni sulle considerazioni sull'utilizzo e problemi noti, vedere [Origine Excel](../data-flow/excel-source.md).  
  
### <a name="data-source--microsoft-access"></a>Origine dati = Microsoft Access  
  
> [!NOTE]  
>  Selezionare **Microsoft Access** solo se si desidera connettersi a un database che utilizza Access 2003 o versione precedente. Per connettersi a un database che usa Access 2007, selezionare invece **12,0 Microsoft Office OLE DB motore di database di accesso provider** .  
  
 **Nome file**  
 Consente di specificare il percorso e il nome del file di database dal quale si importano i dati. Ad esempio, **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**. In alternativa, fare clic su **Sfoglia**.  
  
 **Sfoglia**  
 Consente di individuare il file di database tramite la finestra di dialogo **Apri**.  
  
 **Nome utente**  
 Consente di specificare un nome utente valido per la connessione al database quando un file di informazioni sul gruppo di lavoro corrente è associato al database.  
  
 **Password**  
 Consente di specificare la password dell'utente per la connessione al database quando un file di informazioni sul gruppo di lavoro corrente è associato al database. Tuttavia, se il database è protetto con un'unica password per tutti gli utenti, è necessario specificare questo valore nella finestra di dialogo **proprietà di data link** , a cui è possibile accedere facendo clic su **Avanzate**.  
  
 **Avanzate**  
 Si consiglia di specificare opzioni avanzate, ad esempio la password del database o un file di informazioni sul gruppo di lavoro non predefinito, utilizzando la finestra di dialogo **proprietà di data link** . Per ulteriori informazioni sulle proprietà del provider OLE DB, eseguire una ricerca nella sezione relativa all'accesso ai dati di [MSDN Library](https://go.microsoft.com/fwlink/?linkid=62553).  
  
### <a name="data-source--flat-file-source"></a>Origine dati = Origine file flat  
 Per informazioni sulle opzioni per un'origine dei dati flat file, vedere gli argomenti seguenti.  
  
 [Editor gestione connessione file flat &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
 [Editor gestione connessione file flat &#40;pagina Colonne&#41;](../flat-file-connection-manager-editor-columns-page.md)  
  
 [Editor gestione connessione file flat &#40;pagina Avanzate&#41;](../flat-file-connection-manager-editor-advanced-page.md)  
  
 [Editor gestione connessione file flat &#40;pagina Anteprima&#41;](../flat-file-connection-manager-editor-preview-page.md)  
  
  
