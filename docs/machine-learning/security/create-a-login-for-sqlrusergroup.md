---
title: Creare un account di accesso per SQLRUserGroup
description: Creare un account di accesso in SQL Server per SQLRUserGroup, usando l'autenticazione implicita per accedere al server, per riconvertire l'identità nell'utente chiamante.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/25/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fcdb8353abe029291352f031d5261849514ef8fd
ms.sourcegitcommit: 894c1a23e922dc29b82c1d2c34c7b0ff28b38654
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/01/2020
ms.locfileid: "92195755"
---
# <a name="create-a-login-for-sqlrusergroup"></a>Creare un account di accesso per SQLRUserGroup
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Creare un [account di accesso in SQL Server](../../relational-databases/security/authentication-access/create-a-login.md) per [SQLRUserGroup](../concepts/security.md#sqlrusergroup) quando una [connessione loopback](../../machine-learning/concepts/security.md#implied-authentication) nello script specifica una *connessione trusted* e l'identità usata per eseguire un oggetto che contiene il codice è un account utente di Windows.

Le connessioni trusted sono quelle con `Trusted_Connection=True` nella stringa di connessione. Quando SQL Server riceve una richiesta che specifica una connessione trusted, verifica se l'identità dell'utente di Windows corrente ha un account di accesso. Per i processi esterni eseguiti come account di lavoro (ad esempio MSSQLSERVER01 da **SQLRUserGroup** ), la richiesta ha esito negativo perché questi account non hanno un account di accesso per impostazione predefinita.

Per risolvere l'errore di connessione, è possibile creare un account di accesso per **SQLServerRUserGroup**. Per altre informazioni sulle identità e i processi esterni, vedere [Panoramica della sicurezza per il framework di estendibilità](../concepts/security.md).

> [!Note]
> Verificare che **SQLRUserGroup** abbia le autorizzazioni "Consenti accesso locale". Per impostazione predefinita, questo diritto viene concesso a tutti i nuovi utenti locali, ma potrebbe essere disabilitato da Criteri di gruppo più restrittivi di alcune organizzazioni.

## <a name="create-a-login"></a>Crea un accesso

1. In Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]espandere la cartella **Sicurezza** , fare clic con il pulsante destro del mouse su **Account di accesso** e quindi scegliere **Nuovo account di accesso**.

2. Nella finestra di dialogo **Account di accesso - Nuovo** selezionare **Cerca**. (Non digitare ancora nulla nella casella.)
    
     ![Fare clic su Cerca per aggiungere un nuovo account di accesso per Machine Learning](media/implied-auth-login1.png "Fare clic su Cerca per aggiungere un nuovo account di accesso per Machine Learning")

3. Nella casella **Seleziona utente o gruppo** fare clic sul pulsante **Tipi di oggetto**.

     ![Cercare i tipi di oggetto per aggiungere un nuovo account di accesso per Machine Learning](media/implied-auth-login2.png "Cercare i tipi di oggetto per aggiungere un nuovo account di accesso per Machine Learning")

4. Nella finestra di dialogo **Tipi di oggetto** selezionare **Gruppi**. Deselezionare tutte le altre caselle di controllo.

     ![Selezionare Gruppi nella finestra di dialogo Tipi di oggetto](media/implied-auth-login3.png "Selezionare Gruppi nella finestra di dialogo Tipi di oggetto")

4. Fare clic su **Avanzata** , verificare che il percorso in cui eseguire la ricerca sia il computer corrente e quindi fare clic su **Trova ora**.

     ![Fare clic su Trova ora per ottenere un elenco di gruppi](media/implied-auth-login4.png "Fare clic su Trova ora per ottenere un elenco di gruppi")

5. Scorrere l'elenco degli account di gruppo nel server fino a quando non ne viene individuato uno che inizia con `SQLRUserGroup`.
    
    + Il nome del gruppo associato al servizio Launchpad per l' _istanza predefinita_ è sempre **SQLRUserGroup** , indipendentemente dal fatto che siano installati R o Python o entrambi. Selezionare questo account solo per l'istanza predefinita.
    + Se si usa un' _istanza denominata_ , il nome dell'istanza viene aggiunto al nome del gruppo di lavoro predefinito, `SQLRUserGroup`. Ad esempio, se l'istanza è denominata "MLTEST", il nome del gruppo di utenti predefinito per questa istanza sarà **SQLRUserGroupMLTest**.
 
    ![Esempio di gruppi nel server](media/implied-auth-login5.png "Esempio di gruppi nel server")
   
5. Fare clic su **OK** per chiudere la finestra di dialogo di ricerca avanzata.

    > [!IMPORTANT]
    > Assicurarsi di aver selezionato l'account corretto per l'istanza. Ogni istanza può usare solo il proprio servizio Launchpad e il gruppo creato per tale servizio. Le istanze non possono condividere un servizio Launchpad o account di lavoro.

6. Fare clic su **OK** ancora una volta per chiudere la finestra di dialogo **Seleziona utente o gruppo**.

7. Nella finestra di dialogo **Account di accesso - Nuovo** fare clic su **OK**. Per impostazione predefinita, l'account di accesso viene assegnato al ruolo **public** e dispone dell'autorizzazione per connettersi al motore di database.

## <a name="next-steps"></a>Passaggi successivi

+ [Panoramica della sicurezza](../concepts/security.md)
+ [Framework di estendibilità](../concepts/extensibility-framework.md)