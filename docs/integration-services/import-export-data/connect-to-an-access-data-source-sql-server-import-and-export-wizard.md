---
title: Connettersi a un'origine dati Access (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: dca8a4f49a8c7ffbef251a90d72bdd13395185e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114600"
---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>Connettersi a un'origine dati Access (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Questo argomento illustra come connettersi a un'origine dati **Microsoft Access** dalla pagina **Scelta origine dati** o **Scelta destinazione** dell'Importazione/Esportazione guidata SQL Server.

La schermata seguente mostra una connessione di esempio a un database Microsoft Access. In questo esempio non è necessario immettere un nome utente e una password perché il database di destinazione non usa un file di informazioni sul gruppo di lavoro.

![Connettersi ad Access](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>Opzioni da specificare

> [!NOTE]
> Le opzioni di connessione per il provider di dati sono le stesse sia nel caso in cui Access rappresenti l'origine sia nel caso in cui rappresenti la destinazione. Ovvero, le opzioni visualizzate sono le stesse in entrambe le pagine **Scelta origine dati** e **Scelta destinazione** della procedura guidata.

**Origine dati**  
L'elenco dei provider di dati può contenere diverse voci per Microsoft Access. Selezionare la versione installata più recente o la versione che corrisponde alla versione di Access che ha creato il file di database.

|Origine dati|Versione di Office|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access (Motore di database di Microsoft Access)|Office 2010 e Office 2007|
|Microsoft Access (Motore di database Microsoft Jet)|Versioni di Office precedenti alla versione Office 2007|

> [!IMPORTANT]
> Per connettersi ai database Access, può essere necessario scaricare e installare file aggiuntivi. Per altre informazioni, vedere [Ottenere i file necessari per connettersi ad Access](#officeDownloads) in questa pagina.

 **Nome file**  
Specificare il percorso e il nome del file Access. Ad esempio, **C:\\MyData.mdb** per un file nel computer locale o **\\\\Sales\\Database\\Northwind.mdb** per un file in una condivisione di rete. In alternativa, fare clic su **Sfoglia**. 

> [!NOTE]
> Se si fa clic su **Sfoglia** per individuare il file Access, la finestra di dialogo **Apri** applica per impostazione predefinita un filtro per i file con formato ed estensione di file MDB. Il provider di dati è in grado tuttavia di aprire anche i file con il nuovo formato ed estensione di file ACCDB.
  
 **Sfoglia**  
 Consente di individuare il file di database tramite la finestra di dialogo **Apri**.  
  
 **User name**  
Se un file di informazioni sul gruppo di lavoro è associato al database, specificare un nome utente valido.  
  
 **Password**  
Se un file di informazioni sul gruppo di lavoro è associato al database, specificare la password dell'utente.
 
Se il database è protetto con un'unica password per tutti gli utenti, vedere [File di database protetto da password](#database_password).
  
 **Advanced**  
Specificare le opzioni avanzate, ad esempio la password del database o un file di informazioni sul gruppo di lavoro diverso da quello predefinito, nella finestra di dialogo **Proprietà di Data Link**.  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>Access non è incluso nell'elenco delle origini dati
Se Access non è incluso nell'elenco delle origini dati, controllare se è in esecuzione la procedura guidata a 64 bit. I provider per Excel e Access sono in genere a 32 bit e non sono visibili nella procedura guidata a 64 bit. Eseguire la procedura guidata a 32 bit.

> [!NOTE]
> Per usare la versione a 64 bit dell'Importazione/Esportazione guidata SQL Server, è necessario installare SQL Server. SQL Server Data Tools (SSDT) e SQL Server Management Studio (SSMS) sono applicazioni a 32 bit e installano solo i file a 32 bit, inclusa la versione a 32 bit della procedura guidata.

## <a name="officeDownloads"></a>Ottenere i file necessari per connettersi ad Access  
Se non sono già stati installati, potrebbe essere necessario scaricare i componenti di connettività per le origini dati Microsoft Office, incluse le origini dati Access ed Excel. Scaricare la versione più recente dei componenti di connettività per i file Excel e Access qui: [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920).
  
La versione più recente dei componenti può aprire file creati da versioni precedenti di Access.

Se il computer ha una versione a 32 bit di Office, è necessario installare la versione a 32 bit dei componenti e verificare anche di eseguire il pacchetto in modalità a 32 bit.

Se si ha un abbonamento a Office 365, assicurarsi di scaricare Access Database Engine 2016 Redistributable e non Microsoft Access 2016 Runtime. Durante l'esecuzione del programma di installazione potrebbe essere visualizzato un messaggio di errore che indica non è possibile installare il download in modalità affiancata con i componenti di Office A portata di clic. Per ignorare questo messaggio di errore, eseguire l'installazione in modalità non interattiva aprendo una finestra del prompt dei comandi ed eseguendo il file con estensione EXE scaricato con l'opzione `/quiet`. Esempio:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a> File di database protetto da password
In alcuni casi il database Access è protetto da password ma non usa alcun file di informazioni sul gruppo di lavoro. È necessario che tutti gli utenti immettano la stessa password ma non è necessario che immettano un nome utente. Per specificare una password di database, eseguire le operazioni seguenti.

1.  Nella pagina **Scelta origine dati** o **Scelta destinazione** fare clic sul pulsante **Avanzate** per aprire la finestra di dialogo **Proprietà di Data Link**.  
2.  Nella finestra di dialogo **Proprietà di Data Link** selezionare la scheda **Tutte**.  
3.  Nell'elenco di proprietà e valori selezionare **Jet OLEDB:Database Password**.   
    
    ![Specificare la password di Access, schermata 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  Fare clic su **Modifica valore** per aprire la finestra di dialogo **Modifica valore proprietà**.  
    
    ![Specificare la password di Access, schermata 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  Nella finestra di dialogo **Modifica valore proprietà** immettere la password del database.
6.  Fare clic su **OK** in ogni finestra di dialogo per tornare alla pagina **Scelta origine dati** o **Scelta destinazione** della procedura guidata e continuare.

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>Mantenere i valori di numerazione automatica durante l'esportazione da Access
Per consentire l'inserimento dei valori di identità esistenti nei dati di origine all'interno di una colonna Identity della tabella di destinazione, scegliere l'opzione **Consenti IDENTITY_INSERT** nella finestra di dialogo **Mapping colonne**. Per impostazione predefinita, la colonna Identity di destinazione in genere non consente di inserire valori esistenti. Per visualizzare la finestra di dialogo **Mapping colonne**, selezionare **Modifica mapping** nella pagina **Seleziona tabelle e viste di origine** della procedura guidata. Per visualizzare le pagine, vedere [Seleziona tabelle e viste di origine](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) e [Mapping colonne](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

Se le chiavi primarie esistenti si trovano in una colonna Identity, in una contatore o nell'equivalente, in genere è necessario selezionare questa opzione per mantenere i valori di chiave primaria esistenti. In caso contrario la colonna Identity di destinazione assegna in genere nuovi valori.

## <a name="see-also"></a>Vedere anche
[Scelta origine dati](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Scelta destinazione](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

