---
title: Gestire l'accesso al cluster Big Data in modalità Active Directory
description: Gestire l'accesso al cluster Big Data
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9f9cca7e761b8f8ec3f5b87e9a195a0eb8b5da6d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "76259459"
---
# <a name="manage-big-data-cluster-access-in-active-directory-mode"></a>Gestire l'accesso al cluster Big Data in modalità Active Directory

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo spiega come aggiornare i gruppi di Active Directory resi disponibili durante la distribuzione per clusterAdmins e clusterUsers.

## <a name="two-overarching-roles-in-the-big-data-cluster"></a>Due ruoli globali nel cluster Big Data

I gruppi di Active Directory possono essere specificati nella sezione sicurezza del profilo di distribuzione come parte di due ruoli globali per l'autorizzazione all'interno del cluster Big Data:

* `clusterAdmins`: Questo parametro accetta un gruppo di Active Directory. I membri di questo gruppo ottengono le autorizzazioni con privilegi di amministratore per l'intero cluster. Hanno autorizzazioni *sysadmin* in SQL Server, autorizzazioni *superuser* in Hadoop Distributed File System (HDFS) e Spark e diritti di *amministratore* nel controller.

* `clusterUsers`: Questi gruppi di Active Directory sono utenti normali senza autorizzazioni con privilegi di amministratore nel cluster. Sono autorizzati ad accedere all'istanza master di SQL Server ma, per impostazione predefinita, non hanno autorizzazioni per gli oggetti o i dati.

Un modo per concedere ulteriori autorizzazioni ai gruppi di Active Directory per il cluster Big Data dopo la distribuzione consiste nell'aggiungere altri utenti e gruppi ai gruppi già nominati durante la distribuzione. 

Tuttavia, può non essere sempre possibile per gli amministratori modificare le appartenenze ai gruppi all'interno Active Directory. Per concedere autorizzazioni aggiuntive ai gruppi di Active Directory senza modificare le appartenenze ai gruppi all'interno Active Directory, completare le procedure descritte nelle sezioni successive.

## <a name="grant-administrator-permissions-to-additional-active-directory-groups"></a>Concedere le autorizzazioni con privilegi di amministratore ad altri gruppi di Active Directory

>[!IMPORTANT]
>Questa procedura non concede l'accesso con privilegi di amministratore a ulteriori gruppi di Active Directory per i componenti di Hadoop, ad esempio HDFS e Spark, nel cluster Big Data. Questi componenti consentono un solo gruppo di Active Directory come gruppo superuser, ovvero con privilegi avanzati. La restrizione significa che il gruppo specificato in `clusterAdmins` durante la distribuzione rimane il gruppo superuser anche dopo questo passaggio.

Seguendo le procedure descritte in questa sezione, è possibile concedere l'accesso con privilegi di amministratore sia al controller che all'istanza master di SQL Server.

### <a name="create-a-login-for-the-active-directory-user-or-group-in-the-sql-server-master-instance"></a>Creare un account di accesso per l'utente o il gruppo di Active Directory nell'istanza master di SQL Server 

1. Connettersi all'endpoint SQL master usando il client SQL preferito. Usare qualsiasi account di accesso amministratore (ad esempio `AZDATA_USERNAME`, specificato durante la distribuzione). In alternativa, si può usare qualsiasi account Active Directory appartenente al gruppo di Active Directory indicato come `clusterAdmins` nella configurazione di sicurezza.

1. Per creare un account di accesso per l'utente o il gruppo di Active Directory, eseguire il comando TSQL seguente:

   ```sql
   CREATE LOGIN [<domain>\<principal>] FROM WINDOWS;
   ```

   Se si concedono autorizzazioni con privilegi di amministratore nell'istanza di SQL Server, concedere anche l'autorizzazione seguente:

   ```sql
   ALTER SERVER ROLE sysadmin ADD MEMBER [<domain>\<principal>];
   GO
   ```

### <a name="add-the-active-directory-user-or-group-to-the-roles-table-in-the-controller-database"></a>Aggiungere l'utente o il gruppo di Active Directory alla tabella dei ruoli nel database del controller 

1. Ottenere le credenziali SQL Server del controller eseguendo questi comandi:

   a. Eseguire questo comando come amministratore di Kubernetes:

   ```bash
   kubectl get secret controller-sa-secret -n <cluster name> -o yaml | grep password
   ```

   b. Decodificare in Base64 il segreto:

   ```bash
   echo <password from kubectl command>  | base64 --decode && echo
   ```

1. In una finestra di comando separata esporre la porta del server di database del controller:

   ```bash
   kubectl port-forward controldb-0 1433:1433 --address 0.0.0.0 -n <cluster name>
   ```

1. Usare la connessione precedente per inserire una riga nella tabella dei ruoli. Digitare il valore *REALM* in lettere maiuscole.

   Se si concedono autorizzazioni con privilegi di amministratore, usare il ruolo *bdcAdmin* nel *\<nome del ruolo>* . Per gli utenti non amministratori, usare il ruolo *bdcUser*.

   ```sql
   USE controller;
   GO

   INSERT INTO [controller].[auth].[roles] VALUES (N'<user or group name>@<REALM>', N'<role name>')
   GO
   ```

1. Verificare che i membri del gruppo aggiunto abbiano autorizzazioni con privilegi di amministratore per il cluster Big Data effettuando l'accesso all'endpoint del controller ed eseguendo il comando seguente:

   ```bash
   azdata bdc config show
   ```

1. Per gli utenti non amministratori, è possibile verificare l'accesso eseguendo l'autenticazione all'istanza master di SQL Server o al controller usando `azdata login`.

## <a name="next-steps"></a>Passaggi successivi

- [Concetti relativi alla sicurezza per i cluster Big Data di SQL Server 2019](concept-security.md)
