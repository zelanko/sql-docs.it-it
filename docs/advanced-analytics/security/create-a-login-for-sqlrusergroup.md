---
title: Creare un account di accesso per SQLRUserGroup
description: Per le connessioni loopback che usano l'autenticazione implicita, creare un account di accesso in SQL Server per SQLRUserGroup, in modo che un account di lavoro possa accedere al server per la conversione di identità nell'utente chiamante.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a5194f251b7ea47e0d9485446b8957e96037ded0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "68714966"
---
# <a name="create-a-login-for-sqlrusergroup"></a>Creare un account di accesso per SQLRUserGroup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Creare un [account di accesso in SQL Server](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login) per [SQLRUserGroup](../concepts/security.md#sqlrusergroup) quando una [connessione loopback](../../advanced-analytics/concepts/security.md#implied-authentication) nello script specifica una *connessione trusted* e l'identità usata per eseguire un oggetto che contiene il codice è un account utente di Windows.

Le connessioni trusted sono quelle con `Trusted_Connection=True` nella stringa di connessione. Quando SQL Server riceve una richiesta che specifica una connessione trusted, verifica se l'identità dell'utente di Windows corrente ha un account di accesso. Per i processi esterni eseguiti come account di lavoro (ad esempio MSSQLSERVER01 da **SQLRUserGroup**), la richiesta ha esito negativo perché questi account non hanno un account di accesso per impostazione predefinita.

Per risolvere l'errore di connessione, è possibile creare un account di accesso per **SQLServerRUserGroup**. Per altre informazioni sulle identità e i processi esterni, vedere [Panoramica della sicurezza per il framework di estendibilità](../concepts/security.md).

> [!Note]
> Verificare che **SQLRUserGroup** abbia le autorizzazioni "Consenti accesso locale". Per impostazione predefinita, questo diritto viene concesso a tutti i nuovi utenti locali, ma potrebbe essere disabilitato da Criteri di gruppo più restrittivi di alcune organizzazioni.

## <a name="create-a-login"></a>Crea un accesso

1. In Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]espandere la cartella **Sicurezza**, fare clic con il pulsante destro del mouse su **Account di accesso**e quindi scegliere **Nuovo account di accesso**.

2. Nella finestra di dialogo **Account di accesso - Nuovo** selezionare **Cerca**. (Non digitare ancora nulla nella casella.)
    
     ![Fare clic su Cerca per aggiungere un nuovo account di accesso per Machine Learning](media/implied-auth-login1.png "Fare clic su Cerca per aggiungere un nuovo account di accesso per Machine Learning")

3. Nella casella **Seleziona utente o gruppo** fare clic sul pulsante **Tipi di oggetto**.

     ![Cercare i tipi di oggetto per aggiungere un nuovo account di accesso per Machine Learning](media/implied-auth-login2.png "Cercare i tipi di oggetto per aggiungere un nuovo account di accesso per Machine Learning")

4. Nella finestra di dialogo **Tipi di oggetto** selezionare **Gruppi**. Deselezionare tutte le altre caselle di controllo.

     ![Selezionare Gruppi nella finestra di dialogo Tipi di oggetto](media/implied-auth-login3.png "Selezionare Gruppi nella finestra di dialogo Tipi di oggetto")

4. Fare clic su **Avanzata**, verificare che il percorso in cui eseguire la ricerca sia il computer corrente e quindi fare clic su **Trova ora**.

     ![Fare clic su Trova ora per ottenere un elenco di gruppi](media/implied-auth-login4.png "Fare clic su Trova ora per ottenere un elenco di gruppi")

5. Scorrere l'elenco degli account di gruppo nel server fino a quando non ne viene individuato uno che inizia con `SQLRUserGroup`.
    
    + Il nome del gruppo associato al servizio Launchpad per l'_istanza predefinita_ è sempre **SQLRUserGroup**, indipendentemente dal fatto che siano installati R o Python o entrambi. Selezionare questo account solo per l'istanza predefinita.
    + Se si usa un'_istanza denominata_, il nome dell'istanza viene aggiunto al nome del gruppo di lavoro predefinito, `SQLRUserGroup`. Ad esempio, se l'istanza è denominata "MLTEST", il nome del gruppo di utenti predefinito per questa istanza sarà **SQLRUserGroupMLTest**.
 
    ![Esempio di gruppi nel server](media/implied-auth-login5.png "Esempio di gruppi nel server")
   
5. Fare clic su **OK** per chiudere la finestra di dialogo di ricerca avanzata.

    > [!IMPORTANT]
    > Assicurarsi di aver selezionato l'account corretto per l'istanza. Ogni istanza può usare solo il proprio servizio Launchpad e il gruppo creato per tale servizio. Le istanze non possono condividere un servizio Launchpad o account di lavoro.

6. Fare clic su **OK** ancora una volta per chiudere la finestra di dialogo **Seleziona utente o gruppo**.

7. Nella finestra di dialogo **Account di accesso - Nuovo** fare clic su **OK**. Per impostazione predefinita, l'account di accesso viene assegnato al ruolo **public** e dispone dell'autorizzazione per connettersi al motore di database.

## <a name="next-steps"></a>Passaggi successivi

+ [Panoramica della sicurezza](../concepts/security.md)
+ [Framework di estendibilità](../concepts/extensibility-framework.md)
