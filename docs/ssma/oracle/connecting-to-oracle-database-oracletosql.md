---
title: Connessione a Oracle Database (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: fc25c36a0d0133975414f4c7270da2974b552f40
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266193"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>Connessione a un database Oracle (OracleToSQL)
Per eseguire la migrazione dei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]database Oracle a, è necessario connettersi al database Oracle di cui si desidera eseguire la migrazione. Quando si esegue la connessione, SSMA ottiene i metadati relativi a tutti gli schemi Oracle e quindi li Visualizza nel riquadro Oracle Metadata Explorer. SSMA archivia le informazioni sul server di database, ma non archivia le password.  
  
La connessione al database rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi se si desidera una connessione attiva al database.  
  
I metadati relativi al database Oracle non vengono aggiornati automaticamente. Se invece si desidera aggiornare i metadati in Oracle Metadata Explorer, è necessario aggiornarli manualmente. Per ulteriori informazioni, vedere la sezione "aggiornamento dei metadati Oracle" più avanti in questo argomento.  
  
## <a name="required-oracle-permissions"></a>Autorizzazioni Oracle obbligatorie  
L'account utilizzato per la connessione al database Oracle deve disporre almeno delle autorizzazioni **Connect** . Ciò consente a SSMA di ottenere i metadati dagli schemi di proprietà dell'utente che si connette. Per ottenere i metadati per gli oggetti di altri schemi e quindi convertire gli oggetti in tali schemi, l'account deve disporre delle autorizzazioni seguenti:  
  
-   CREA QUALSIASI ROUTINE  
  
-   ESEGUIRE QUALSIASI PROCEDURA  
  
-   SELEZIONA UNA TABELLA  
  
-   SELEZIONA QUALSIASI SEQUENZA  
  
-   CREA QUALSIASI TIPO  
  
-   CREA QUALSIASI TRIGGER  
  
-   SELEZIONA UN DIZIONARIO  
  
## <a name="establishing-a-connection-to-oracle"></a>Stabilire una connessione a Oracle  
Quando ci si connette a un database, SSMA legge i metadati del database e quindi aggiunge questi metadati al file di progetto. Questi metadati vengono usati da SSMA quando converte gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintassi e quando esegue la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile esplorare questi metadati nel riquadro di Esplora metadati Oracle ed esaminare le proprietà dei singoli oggetti di database.  
  
> [!IMPORTANT]  
> Prima di provare a connettersi, verificare che il server di database sia in esecuzione e che sia in grado di accettare le connessioni.  
  
**Per connettersi a Oracle**  
  
1.  Scegliere **Connetti a Oracle**dal menu **file** .  
  
    Se in precedenza è stata effettuata la connessione a Oracle, il nome del comando verrà **riconnesso a Oracle**.  
  
2.  Nella casella **provider** selezionare **provider client Oracle** o **provider OLE DB**, a seconda del provider installato. Il valore predefinito è Oracle client.  
  
3.  Nella casella **modalità** selezionare la modalità **standard**, la modalità **TNSNAME**o la **modalità stringa di connessione**.  
  
    Utilizzare la modalità standard per specificare il nome e la porta del server. Utilizzare la modalità nome servizio per specificare manualmente il nome del servizio Oracle. Utilizzare la modalità stringa di connessione per fornire una stringa di connessione completa.  
  
4.  Se si seleziona la **modalità standard**, fornire i valori seguenti:  
  
    1.  Nella casella **nome server** immettere o selezionare il nome o l'indirizzo IP del server di database.  
  
    2.  Se il server di database non è configurato per accettare le connessioni sulla porta predefinita (1521), immettere il numero di porta utilizzato per le connessioni Oracle nella casella **porta server** .  
  
    3.  Nella casella **Oracle SID** immettere l'identificatore di sistema.  
  
    4.  Nella casella **nome utente** immettere un account Oracle con le autorizzazioni necessarie.  
  
    5.  Nella casella **password** immettere la password per il nome utente specificato.  
  
5.  Se si seleziona la **modalità TNSNAME**, specificare i valori seguenti:  
  
    1.  Nella casella **identificatore di connessione** immettere identificatore di connessione (ID TNS) del database.  
  
    2.  Nella casella **nome utente** immettere un account Oracle con le autorizzazioni necessarie.  
  
    3.  Nella casella **password** immettere la password per il nome utente specificato.  
  
6.  Se si seleziona la **modalità stringa di connessione**, specificare una stringa di connessione nella casella **stringa di connessione** .  
  
    Nell'esempio seguente viene illustrata una stringa di connessione OLE DB:  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    Nell'esempio seguente viene illustrata una stringa di connessione del client Oracle che utilizza la sicurezza integrata:  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    Per altre informazioni, vedere [connettersi a Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).  
  
## <a name="reconnecting-to-oracle"></a>Riconnessione a Oracle  
La connessione al server di database rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi se si desidera una connessione attiva al database. È possibile lavorare offline fino a quando non si desidera aggiornare i metadati, caricare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]oggetti di database in ed eseguire la migrazione dei dati.  
  
## <a name="refreshing-oracle-metadata"></a>Aggiornamento dei metadati Oracle  
I metadati relativi al database Oracle non vengono aggiornati automaticamente. I metadati in Oracle Metadata Explorer sono uno snapshot dei metadati al momento della prima connessione oppure l'ultima volta che i metadati sono stati aggiornati manualmente. È possibile aggiornare manualmente i metadati per tutti gli schemi, un singolo schema o singoli oggetti di database.  
  
**Per aggiornare i metadati**  
  
1.  Assicurarsi di essere connessi al database.  
  
2.  In Esplora metadati Oracle selezionare la casella di controllo accanto a ogni schema o oggetto di database che si desidera aggiornare.  
  
3.  Fare clic con il pulsante destro del mouse su **schemi**oppure sul singolo schema o oggetto di database, quindi scegliere **Aggiorna da database**.  
  
    Se non si dispone di una connessione attiva, in SSMA viene visualizzata la finestra **di dialogo Connetti a Oracle in** cui è possibile connettersi.  
  
4.  Nella finestra di dialogo Aggiorna da database specificare gli oggetti da aggiornare.  
  
    -   Per aggiornare un oggetto, fare clic sul campo **attivo** adiacente all'oggetto fino a quando non viene visualizzata una freccia.  
  
    -   Per impedire l'aggiornamento di un oggetto, fare clic sul campo **attivo** adiacente all'oggetto fino a quando non viene visualizzata una **X** .  
  
    -   Per aggiornare o rifiutare una categoria di oggetti, fare clic sul campo **attivo** accanto alla cartella Category.  
  
    Per visualizzare le definizioni della codifica dei colori, fare clic sul pulsante **Legenda** .  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>passaggio successivo  
  
-   Il passaggio successivo del processo di migrazione consiste nel [connettersi a un'istanza di SQL Server](connecting-to-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione di database Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
