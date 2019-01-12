---
title: 'Aggiungere SQLRUserGroup come un accesso SQL Server: SQL Server Machine Learning Services'
description: Per le connessioni loopback tramite autenticazione implicita, aggiungere SQLRUserGroup come un account di accesso di SQL Server in modo che un account di lavoro possa accedere al server, per la conversione di identità all'utente chiama.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0bc84a7a4cfae14ea19491c42e828d0a93cdfba7
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143421"
---
# <a name="add-sqlrusergroup-as-a-sql-server-login"></a>Aggiungere SQLRUserGroup come un account di accesso di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Creare un account di accesso di SQL Server per [SQLRUserGroup](../concepts/security.md#sqlrusergroup) quando un [ciclo connessione loopback](../../advanced-analytics/concepts/security.md#implied-authentication) nello script specifica un *connessione trusted*e l'identità usata per eseguire un oggetto contiene il codice è un account utente di Windows.

Attendibili le connessioni sono quelli con `Trusted_Connection=True` nella stringa di connessione. Quando SQL Server riceve una richiesta che specifica una connessione trusted, controlla se l'identità dell'utente Windows corrente dispone di un account di accesso. Per i processi esterni in esecuzione come un account di lavoro (ad esempio MSSQLSERVER01 dal **SQLRUserGroup**), la richiesta ha esito negativo perché tali account non dispongono di un account di accesso per impostazione predefinita.

È possibile risolvere l'errore di connessione, assegnando **SQLServerRUserGroup** un account di accesso di SQL Server. Per altre informazioni su identità e i processi esterni, vedere [Panoramica sulla sicurezza per il framework di estendibilità](../concepts/security.md).

> [!Note]
>  Verificare che l'opzione **SQLRUserGroup** disponga delle autorizzazioni "Consenti accesso locale". Per impostazione predefinita, questo diritto viene assegnato a tutti i nuovi utenti locali, ma in alcune organizzazioni i criteri di gruppo più rigorosi potrebbero disabilitare questo diritto.

## <a name="create-a-login"></a>Crea un accesso

1. In Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]espandere la cartella **Sicurezza**, fare clic con il pulsante destro del mouse su **Account di accesso**e quindi scegliere **Nuovo account di accesso**.

2. Nel **account di accesso - nuovo** finestra di dialogo **ricerca**. (Non digitare qualsiasi elemento nella finestra di ancora).
    
     ![Fare clic su Cerca per aggiungere nuovi account di accesso per machine learning](media/implied-auth-login1.png "fare clic su Cerca per aggiungere nuovi account di accesso per machine learning")

3. Nel **Seleziona utente o gruppo** fare clic sui **tipi di oggetto** pulsante.

     ![Cerca tipi di oggetto per aggiungere nuovi account di accesso per machine learning](media/implied-auth-login2.png "Cerca tipi di oggetto per aggiungere nuovi account di accesso per machine learning")

4. Nel **tipi di oggetti** finestra di dialogo **gruppi**. Deselezionare tutte le altre caselle di controllo.

     ![Selezionare i gruppi nella finestra di dialogo tipi di oggetti](media/implied-auth-login3.png "Seleziona gruppi nella finestra di dialogo tipi di oggetto")

4. Fare clic su **avanzate**, verificare che la posizione in cui cercare il computer corrente e quindi fare clic su **trova ora**.

     ![Fare clic su Trova per ottenere l'elenco dei gruppi](media/implied-auth-login4.png "fare clic su Trova per ottenere l'elenco dei gruppi")

5. Scorrere l'elenco degli account di gruppo nel server fino a individuare che inizia con `SQLRUserGroup`.
    
    + Il nome del gruppo di cui è associato il servizio Launchpad per il _istanza predefinita_ è sempre **SQLRUserGroup**, indipendentemente dal fatto che sia installata di R o Python oppure entrambi. Selezionare questo account per solo l'istanza predefinita.
    + Se si usa un' _istanza denominata_, il nome dell'istanza viene aggiunto al nome del nome del gruppo ruolo di lavoro predefinito, `SQLRUserGroup`. Ad esempio, se l'istanza è denominata "MLTEST", il nome di gruppo utente predefinito per questa istanza sarà **SQLRUserGroupMLTest**.
 
 ![Esempio di gruppi nel server](media/implied-auth-login5.png "esempio di gruppi sul server")
   
5. Fare clic su **OK** per chiudere la finestra di dialogo di ricerca avanzata.

    > [!IMPORTANT]
    > Assicurarsi di che aver selezionato l'account corretto per l'istanza. Ogni istanza può usare solo il proprio servizio Launchpad e il gruppo creato per tale servizio. Le istanze non possono condividere un account di servizio o di lavoro di Launchpad.

6. Fare clic su **OK** ancora una volta per chiudere la **Seleziona utente o gruppo** nella finestra di dialogo.

7. Nel **account di accesso - nuovo** finestra di dialogo, fare clic su **OK**. Per impostazione predefinita, l'account di accesso viene assegnato al ruolo **public** e dispone dell'autorizzazione per connettersi al motore di database.

## <a name="next-steps"></a>Passaggi successivi

+ [Panoramica della sicurezza](../concepts/security.md)
+ [Framework di estendibilità](../concepts/extensibility-framework.md)
