---
title: Distribuire in modalità Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Informazioni su come aggiornare un cluster Big Data di SQL Server in un dominio di Active Directory.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 037c8bd26249ab3dc2cb3d0d8f4adf718f56000e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243072"
---
# <a name="deploy-big-data-clusters-2019-in-active-directory-mode"></a>Distribuire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in modalità Active Directory

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Questo documento descrive come distribuire un cluster Big Data (BDC) di SQL Server in modalità di autenticazione di Active Directory. Il cluster usa un dominio di Active Directory esistente per l'autenticazione.

>[!Note]
>Prima di SQL Server 2019 CU5, i cluster Big Data prevedevano una restrizione per cui era possibile distribuire un solo cluster in un dominio di Active Directory. Questa restrizione è stata rimossa con la versione CU5. Per informazioni dettagliate sulle nuove funzionalità, vedere [Concetto: distribuire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in modalità Active Directory](active-directory-deployment-background.md). Gli esempi in questo articolo sono stati modificati per adattarsi a entrambi i casi d'uso di distribuzione.

## <a name="background"></a>Background

Per abilitare l'autenticazione di Active Directory, il cluster Big Data crea automaticamente gli utenti, i gruppi, gli account computer e i nomi dell'entità servizio (SPN) necessari per i vari servizi nel cluster. Per assicurare una certa indipendenza per questi account e consentire autorizzazioni di ambito, durante la distribuzione scegliere un'unità organizzativa in cui verranno creati tutti gli oggetti di Active Directory correlati al cluster Big Data. Creare questa unità organizzativa prima della distribuzione del cluster.

Per creare automaticamente tutti gli oggetti necessari in Active Directory, il cluster Big Data necessita di un account Active Directory durante la distribuzione. Questo account deve avere le autorizzazioni necessarie per la creazione di utenti, gruppi e account computer all'interno dell'unità organizzativa specificata.

La procedura seguente presuppone l'esistenza di un controller di dominio Active Directory. Se non è presente alcun controller di dominio, la [guida](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx) seguente include alcuni passaggi che possono essere utili.

Per un elenco di account e gruppi di Active Directory, vedere [Oggetti di Active Directory generati automaticamente](active-directory-objects.md).

## <a name="create-ad-objects"></a>Creare oggetti di Active Directory

Prima di distribuire un cluster Big Data con l'integrazione di Active Directory, eseguire le operazioni seguenti:

1. Creare un'unità organizzativa (OU), in cui verranno archiviati tutti gli oggetti di Active Directory del cluster Big Data. In alternativa, è possibile scegliere un'unità organizzativa esistente in fase di distribuzione.
1. Creare un account Active Directory per il cluster Big Data oppure usarne uno esistente e fornire a questo account le autorizzazioni appropriate.

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>Creare un utente in Active Directory per l'account del servizio di dominio del cluster Big Data

Il cluster Big Data deve avere un account con autorizzazioni specifiche. Prima di continuare, assicurarsi che sia già presente un account Active Directory oppure crearne uno nuovo, che può essere usato dal cluster Big Data per configurare gli oggetti necessari.

Per creare un nuovo utente in Active Directory, è possibile fare clic con il pulsante destro del mouse sul dominio o sull'unità organizzativa e scegliere **Nuovo** > **Utente**:

![immagine12](./media/deploy-active-directory/image12.png)

Questo utente verrà definito *account del servizio di dominio del cluster Big Data* in questo articolo.

### <a name="create-an-ou"></a>Creare un'unità organizzativa

Nel controller di dominio aprire **Utenti e computer di Active Directory**. Nel pannello di sinistra fare clic con il pulsante destro del mouse sulla directory in cui si vuole creare l'unità organizzativa e scegliere **Nuovo** \> **Unità organizzativa**, quindi seguire le istruzioni della procedura guidata per creare l'unità organizzativa. In alternativa, è possibile creare un'unità organizzativa con PowerShell:

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

Gli esempi in questo articolo usano `bdc` per il nome dell'unità organizzativa.

![immagine13](./media/deploy-active-directory/image13.png)

![immagine14](./media/deploy-active-directory/image14.png)

### <a name="set-permissions-for-an-ad-account"></a>Impostare le autorizzazioni per un account di AD 

Se è stato creato un nuovo utente di Active Directory o se ne usa uno esistente, l'utente deve avere determinate autorizzazioni. Questo account è l'account utente che verrà usato dal controller del cluster Big Data per l'aggiunta del cluster ad Active Directory.

L'account del servizio di dominio del cluster Big Data deve essere in grado di creare utenti, gruppi e account computer nell'unità organizzativa. Nei passaggi seguenti l'account del servizio di dominio del cluster Big Data è denominato `bdcDSA`. È possibile scegliere qualsiasi nome per l'account.

1. Nel controller di dominio aprire **Utenti e computer di Active Directory**

1. Nel pannello sinistro passare al dominio, quindi all'unità organizzativa che verrà usata da `bdc`

1. Fare clic con il pulsante destro del mouse sull'unità organizzativa e scegliere **Proprietà**.

1. Passare alla scheda Sicurezza, assicurandosi di aver selezionato **Funzionalità avanzate**, di avere fatto clic con il pulsante destro del mouse sull'unità organizzativa e quindi di avere scelto **Visualizza**

    ![immagine15](./media/deploy-active-directory/image15.png)

1. Fare clic su **Aggiungi** e aggiungere l'utente **bdcDSA**

    ![immagine16](./media/deploy-active-directory/image16.png)

    ![immagine17](./media/deploy-active-directory/image17.png)

1. Selezionare l'utente **bdcDSA** e deselezionare tutte le autorizzazioni, quindi fare clic su **Avanzate**

1. Fare clic su **Aggiungi**

    ![immagine18](./media/deploy-active-directory/image18.png)

    - Fare clic su **Selezionare un'entità**, immettere **bdcDSA** e fare clic su OK

    - Impostare **Tipo** su **Consenti**

    - Impostare **Si applica a** su **Questo oggetto e tutti i discendenti**

        ![immagine19](./media/deploy-active-directory/image19.png)

    - Scorrere fino alla fine e fare clic su **Cancella tutto**

    - Scorrere di nuovo verso l'alto e selezionare:
       - **Leggi tutte le proprietà**
       - **Scrivi tutte le proprietà**
       - **Crea oggetti computer**
       - **Delete Computer objects** (Elimina oggetti computer)
       - **Create Group objects** (Crea oggetti di gruppo)
       - **Delete Group objects** (Elimina oggetti di gruppo)
       - **Create User objects** (Crea oggetti utente)
       - **Elimina oggetti utente**

    - Fare clic su **OK**.

- Fare clic su **Aggiungi**

    - Fare clic su **Selezionare un'entità**, immettere **bdcDSA** e fare clic su OK

    - Impostare **Tipo** su **Consenti**

    - Impostare **Si applica a** su **Descendant Computer objects** (Oggetti computer discendenti)

    - Scorrere fino alla fine e fare clic su **Cancella tutto**

    - Tornare all'inizio e selezionare **Reimposta password**

    - Fare clic su **OK**.

- Fare clic su **Aggiungi**

    - Fare clic su **Selezionare un'entità**, immettere **bdcDSA** e fare clic su OK

    - Impostare **Tipo** su **Consenti**

    - Impostare **Si applica a** su **Descendant User objects** (Oggetti utente discendenti)

    - Scorrere fino alla fine e fare clic su **Cancella tutto**

    - Tornare all'inizio e selezionare **Reimposta password**

    - Fare clic su **OK**.

- Fare clic su **OK** altre due volte per chiudere le finestre di dialogo aperte

## <a name="prepare-deployment"></a>Preparare la distribuzione

Per la distribuzione di un cluster Big Data con l'integrazione di Active Directory, è necessario fornire alcune informazioni aggiuntive per la creazione degli oggetti correlati al cluster Big Data in Active Directory.

Usando il profilo `kubeadm-prod` (o `openshift-prod` a partire dalla versione CU5), verranno automaticamente immessi i segnaposto per le informazioni relative alla sicurezza e all'endpoint necessarie per l'integrazione di Active Directory.

Inoltre, è necessario fornire le credenziali che verranno usate da [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] per creare gli oggetti necessari in Active Directory. Queste credenziali vengono fornite come variabili di ambiente.

## <a name="set-security-environment-variables"></a>Impostare le variabili di ambiente di sicurezza

Le variabili di ambiente seguenti forniscono le credenziali per l'account del servizio di dominio del cluster Big Data, che verrà usato per configurare l'integrazione di Active Directory. Questo account viene usato anche dal cluster Big Data per mantenere gli oggetti di Active Directory correlati al cluster Big Data stesso in futuro.

```bash
export DOMAIN_SERVICE_ACCOUNT_USERNAME=<AD principal account name>
export DOMAIN_SERVICE_ACCOUNT_PASSWORD=<AD principal password>
```

## <a name="provide-security-and-endpoint-parameters"></a>Fornire parametri di sicurezza e dell'endpoint

Oltre alle variabili di ambiente per le credenziali, è necessario fornire anche le informazioni sulla sicurezza e sull'endpoint per il funzionamento dell'integrazione di Active Directory. I parametri necessari sono inclusi automaticamente nel [profilo di distribuzione](deployment-guidance.md#configfile) `kubeadm-prod`/`openshift-prod`.

Per l'integrazione di Active Directory sono necessari i parametri seguenti. Aggiungere questi parametri ai file `control.json` e `bdc.json` usando i comandi `config replace` mostrati più avanti in questo articolo. Tutti gli esempi seguenti usano il dominio di esempio `contoso.local`.

- `security.activeDirectory.ouDistinguishedName`: nome distinto di un'unità organizzativa (OU) in cui verranno aggiunti tutti gli account Active Directory creati tramite la distribuzione del cluster. Se il dominio è denominato `contoso.local`, il nome distinto dell'unità organizzativa è: `OU=BDC,DC=contoso,DC=local`.

- `security.activeDirectory.dnsIpAddresses`: contiene l'elenco di indirizzi IP dei server DNS del dominio. 

- `security.activeDirectory.domainControllerFullyQualifiedDns`: elenco di nomi di dominio completi del controller di dominio. Il nome di dominio completo contiene il nome computer/host del controller di dominio. Se sono presenti più controller di dominio, è possibile fornirne un elenco qui. Esempio: `HOSTNAME.CONTOSO.LOCAL`.

  > [!IMPORTANT]
  > Quando più controller di dominio gestiscono un dominio, usare il controller di dominio primario (PDC) come prima voce nell'elenco `domainControllerFullyQualifiedDns` della configurazione di sicurezza. Per ottenere il nome del PDC, digitare `netdom query fsmo` al prompt dei comandi e quindi premere **INVIO**.

- `security.activeDirectory.realm` **Parametro facoltativo**: nella maggior parte dei casi, l'area di autenticazione è uguale al nome di dominio. Per i casi in cui non sono uguali, usare questo parametro per definire il nome dell'area di autenticazione, ad esempio `CONTOSO.LOCAL`. Il valore specificato per questo parametro deve essere completo.

- `security.activeDirectory.domainDnsName`: nome del dominio DNS che verrà usato per il cluster, ad esempio `contoso.local`.

- `security.activeDirectory.clusterAdmins`: questo parametro accetta un solo gruppo di AD. L'ambito del gruppo di AD deve essere universale o globale. I membri di questo gruppo avranno il ruolo del cluster *bdcAdmin* che concederà autorizzazioni di amministratore nel cluster. Questo significa che avranno [autorizzazioni `sysadmin` in SQL Server](../relational-databases/security/authentication-access/server-level-roles.md#fixed-server-level-roles), [autorizzazioni `superuser` in HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#The_Super-User) e autorizzazioni di amministratore quando connessi all'endpoint del controller.

  >[!IMPORTANT]
  >Creare questo gruppo in AD prima dell'avvio della distribuzione. Se l'ambito di questo gruppo di AD è il dominio, la distribuzione locale ha esito negativo.

- `security.activeDirectory.clusterUsers`: elenco dei gruppi di Active Directory che sono utenti normali (senza autorizzazioni di amministratore) nel cluster Big Data. L'elenco può includere gruppi di AD che hanno come ambito gruppi globali o universali. Non possono essere gruppi locali di dominio.

I gruppi di AD in questo elenco sono associati al ruolo del cluster Big Data *bdcUser* e necessitano dell'accesso a SQL Server (vedere [Autorizzazioni di SQL Server](../relational-databases/security/permissions-hierarchy-database-engine.md)) o HDFS (vedere [Guida alle autorizzazioni per HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#:~:text=Permission%20Checks%20%20%20%20Operation%20%20,%20%20N%2FA%20%2029%20more%20rows%20)). Quando sono connessi all'endpoint del controller, questi utenti possono elencare solo gli endpoint disponibili nel cluster usando il comando *azdata bdc endpoint list*.

Per informazioni dettagliate su come aggiornare i gruppi di AD per queste impostazioni, vedere [Gestire l'accesso al cluster Big Data in modalità Active Directory](manage-user-access.md).

  >[!IMPORTANT]
  >Creare questi gruppi in AD prima che venga avviata la distribuzione. Se l'ambito per uno di questi gruppi di AD è locale al dominio, la distribuzione non riesce.

  >[!IMPORTANT]
  >Se gli utenti del dominio hanno un numero elevato di appartenenze ai gruppi, è consigliabile modificare i valori per l'impostazione del gateway *httpserver.requestHeaderBuffer* (il valore predefinito è *8192*) e l'impostazione HDFS *hadoop.security.group.mapping.ldap.search.group.hierarchy.levels* (il valore predefinito è *10*), usando il file di configurazione della distribuzione *bdc.json* personalizzato. Si tratta di una procedura consigliata per evitare i timeout di connessione al gateway e/o le risposte HTTP con un codice di stato 431 (*Campi intestazione richiesta troppo grandi*). Di seguito è riportata una sezione del file di configurazione che mostra come definire i valori di queste impostazioni e quali sono i valori consigliati per un numero maggiore di appartenenze ai gruppi: 

```json
{
    ...
    "spec": {
        "resources": {
            ...
            "gateway": {
                "spec": {
                    "replicas": 1,
                    "endpoints": [{...}],
                    "settings": {
                        "gateway-site.gateway.httpserver.requestHeaderBuffer": "65536"
                    }
                }
            },
            ...
        },
        "services": {
            ...
            "hdfs": {
                "resources": [...],
                "settings": {
                  "core-site.hadoop.security.group.mapping.ldap.search.group.hierarchy.levels": "4"
                }
            },
            ...
        }
    }
}
```

  >[!IMPORTANT]
  >Creare i gruppi specificati per le impostazioni di seguito in Active Directory prima che venga avviata la distribuzione. Se l'ambito per uno di questi gruppi di AD è locale al dominio, la distribuzione non riesce.

- `security.activeDirectory.appOwners` **Parametro facoltativo**: elenco dei gruppi di AD che hanno le autorizzazioni necessarie per creare, eliminare ed eseguire qualsiasi applicazione. L'elenco può includere gruppi di AD che hanno come ambito gruppi globali o universali. Non possono essere gruppi locali di dominio.

- `security.activeDirectory.appReaders` **Parametro facoltativo**: elenco dei gruppi di AD che hanno le autorizzazioni necessarie per eseguire qualsiasi applicazione. L'elenco può includere gruppi di AD che hanno come ambito gruppi globali o universali. Non possono essere gruppi locali di dominio.

La tabella seguente mostra il modello di autorizzazione per la gestione delle applicazioni:

|   Ruoli autorizzati   |   Comando azdata   |
|----------------------|--------------------|
|   appOwner           | azdata app create  |
|   appOwner           | azdata app update  |
|   appOwner, appReader| azdata app list    |
|   appOwner, appReader| azdata app describe|
|   appOwner           | azdata app delete  |
|   appOwner, appReader| azdata app run     |

- `security.activeDirectory.subdomain`: **Parametro facoltativo**: questo parametro è stato introdotto in SQL Server 2019 CU5 per supportare la distribuzione di più cluster Big Data nello stesso dominio. Usando questa impostazione, è possibile specificare nomi DNS diversi per ogni cluster Big Data distribuito. Se il valore di questo parametro non è specificato nella sezione relativa ad Active Directory del file `control.json`, per impostazione predefinita verrà usato il nome del cluster Big Data (uguale al nome dello spazio dei nomi Kubernetes) per calcolare il valore dell'impostazione del sottodominio. 

  >[!NOTE]
  >Il valore passato tramite l'impostazione del sottodominio non è un nuovo dominio di Active Directory, ma solo un dominio DNS usato dal cluster BDC internamente.

  >[!IMPORTANT]
  >È necessario installare o aggiornare la versione più recente dell'**interfaccia della riga di comando di azdata** a partire da SQL Server 2019 CU5 per sfruttare queste nuove funzionalità e distribuire più cluster Big Data nello stesso dominio.

  Per altri dettagli sulla distribuzione di più cluster Big Data nello stesso dominio di Active Directory, vedere [Concetto: distribuire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in modalità Active Directory](active-directory-deployment-background.md).

- `security.activeDirectory.accountPrefix`: **Parametro facoltativo**: questo parametro è stato introdotto in SQL Server 2019 CU5 per supportare la distribuzione di più cluster Big Data nello stesso dominio. Questa impostazione garantisce l'univocità dei nomi degli account per vari servizi dei cluster Big Data, che devono essere diversi tra due cluster. La personalizzazione del nome del prefisso dell'account è facoltativa. Per impostazione predefinita, come prefisso dell'account viene usato il nome del sottodominio. Se il nome del sottodominio supera i 12 caratteri, come prefisso dell'account vengono usati i primi 12 caratteri del nome del sottodominio.  

  >[!NOTE]
  >Active Directory impone il limite di 20 caratteri per i nomi degli account. Il cluster BDC deve usare 8 caratteri per distinguere pod e StatefulSet. Rimangono così al massimo 12 caratteri per il prefisso dell'account.

[Controllare l'ambito del gruppo AD](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps) per determinare se è DomainLocal.

Se il file di configurazione della distribuzione non è stato ancora inizializzato, è possibile eseguire questo comando per ottenere una copia della configurazione. Gli esempi seguenti usano il profilo `kubeadm-prod`, ma la stessa procedura è applicabile a `openshift-prod`.

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

Per impostare i parametri precedenti nel file `control.json`, usare i comandi `azdata` seguenti. I comandi sostituiscono la configurazione e forniscono i valori personalizzati prima della distribuzione.

> [!IMPORTANT]
> Nella versione SQL Server 2019 CU2 la struttura della sezione relativa alla configurazione della sicurezza nel profilo di distribuzione è cambiata leggermente e tutte le impostazioni di Active Directory correlate si trovano nella nuova sezione *activeDirectory* nell'albero json in *security* nel file *control.json*.

>[!NOTE]
> Oltre a fornire valori diversi per il sottodominio come descritto in questa sezione, è necessario usare anche numeri di porta diversi per gli endpoint BDC quando si distribuiscono più BDC nello stesso cluster Kubernetes. Questi numeri di porta sono configurabili in fase di distribuzione tramite i profili di [configurazione della distribuzione](deployment-custom-configuration.md).

L'esempio seguente si basa sull'uso di SQL Server 2019 CU2. Illustra come sostituire i valori di parametri correlati ad Active Directory nella configurazione della distribuzione. I dettagli del dominio riportati di seguito sono valori di esempio.

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

Facoltativamente, solo a partire da SQL Server 2019 CU5, è possibile sostituire i valori predefiniti per le impostazioni `subdomain` e `accountPrefix`.

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.subdomain=[\"bdctest\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.accountPrefix=[\"bdctest\"]"
```

Analogamente, nelle versioni precedenti a SQL Server 2019 CU2, è possibile eseguire:

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

Oltre alle informazioni precedenti, è necessario fornire anche i nomi DNS per i diversi endpoint del cluster. In fase di distribuzione verranno automaticamente create le voci DNS che usano i nomi DNS specificati nel server DNS. Questi nomi verranno usati durante la connessione ai diversi endpoint del cluster. Ad esempio, se il nome DNS per l'istanza master SQL è `mastersql` e considerando che il sottodominio usi il valore predefinito del nome del cluster in *control.json*, sarà possibile usare `mastersql.contoso.local,31433` o `mastersql.mssql-cluster.contoso.local,31433` (a seconda dei valori specificati nei file di configurazione della distribuzione per i nomi DNS degli endpoint) per connettersi all'istanza master dagli strumenti. 

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[1].dnsName=<monitoring services DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=<SQL Master Primary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=<SQL Master Secondary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=<Gateway (Knox) DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=<app proxy DNS name>.<Domain name. e.g. contoso.local>"
```

> [!IMPORTANT]
> È possibile usare nomi DNS degli endpoint personalizzati purché siano completi e non siano in conflitto tra due cluster Big Data distribuiti nello stesso dominio. Facoltativamente, è possibile usare il valore del parametro `subdomain` per assicurarsi che i nomi DNS siano diversi tra i cluster. Ad esempio:

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.<subdomain e.g. mssql-cluster>.contoso.local"
```

Qui è possibile trovare uno script di esempio per la [distribuzione di un cluster Big Data di SQL Server in un cluster Kubernetes a nodo singolo (kubeadm) con l'integrazione di AD](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm-ad).

> [!Note]
> Il nuovo parametro `subdomain` introdotto con l'aggiornamento potrebbe non essere utilizzabile in alcuni scenari, ad esempio quando è necessario distribuire una versione precedente alla CU5 ed è già stato eseguito l'aggiornamento dell'**interfaccia della riga di comando di azdata**. Questo scenario è altamente improbabile, ma se è necessario ripristinare il comportamento precedente alla versione CU5, è possibile impostare il parametro `useSubdomain` su `false` nella sezione relativa ad Active Directory di `control.json`.  Il comando da usare è il seguente:

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.useSubdomain=false"
```

A questo punto, sono stati impostati tutti i parametri necessari per una distribuzione del cluster Big Data con l'integrazione di Active Directory.

È ora possibile distribuire il cluster BDC integrato con Active Directory usando il comando `azdata` e il profilo di distribuzione kubeadm-prod. Per la documentazione completa su come distribuire [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)], vedere [Come distribuire cluster Big Data di SQL Server in Kubernetes](deployment-guidance.md).

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>Verificare la voce DNS inversa per il controller di dominio

Assicurarsi che sia presente una voce DNS inversa (record PTR) per il controller di dominio stesso, registrata nel server DNS. A questo scopo, è possibile eseguire `nslookup` del nome di dominio nel controller di dominio per verificare che possa essere risolto nell'indirizzo IP del controller di dominio.

## <a name="connect-to-cluster-endpoints-in-ad-mode"></a>Connettersi agli endpoint del cluster in modalità Active Directory

Accedere all'istanza master di SQL Server tramite l'autenticazione di Active Directory.

Per verificare le connessioni di Active Directory all'istanza di SQL Server, connettersi all'istanza master di SQL Server con `sqlcmd`. Gli account di accesso vengono creati automaticamente per i gruppi specificati in fase di distribuzione (`clusterUsers` e `clusterAdmins`).

Se si usa Linux, eseguire prima `kinit` come utente di Active Directory, quindi eseguire `sqlcmd`. Se si usa Windows, è sufficiente accedere come utente desiderato da un **computer client aggiunto al dominio**.

### <a name="connect-to-master-instance-from-linuxmac"></a>Connettersi all'istanza master da Linux/Mac

```bash
kinit <username>@<domain name>
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="connect-to-master-instance-from-windows"></a>Connettersi all'istanza master da Windows

```cmd
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="log-in-to-sql-server-master-instance-using-azure-data-studio-or-ssms"></a>Accedere all'istanza master di SQL Server tramite Azure Data Studio o SSMS

Da un client aggiunto a un dominio è possibile aprire SSMS o Azure Data Studio e connettersi all'istanza master. Si tratta di un'esperienza identica a quella di connessione a qualsiasi istanza di SQL Server tramite l'autenticazione di Active Directory.

Da SSMS:

![immagine23](./media/deploy-active-directory/image23.png)

Da Azure Data Studio:

![immagine24](./media/deploy-active-directory/image24.png)}

### <a name="log-in-to-controller-with-ad-authentication"></a>Accedere al controller tramite l'autenticazione di Active Directory

#### <a name="connect-to-controller-with-ad-authentication-from-linuxmac"></a>Connettersi al controller tramite l'autenticazione di Active Directory da Linux/Mac

Sono disponibili due opzioni per connettersi all'endpoint controller tramite `azdata` e l'autenticazione di Active Directory. È possibile usare il parametro *--endpoint/-e*:

```bash
kinit <username>@<domain name>
azdata login -e https://<controller DNS name>:30080 --auth ad
```

In alternativa, è possibile connettersi usando il parametro *--namespace/-n*, che corrisponde al nome del cluster Big Data:

```bash
kinit <username>@<domain name>
azdata login -n <clusterName> --auth ad
```

#### <a name="connect-to-controller-with-ad-authentication-from-windows"></a>Connettersi al controller tramite l'autenticazione di Active Directory da Windows

```cmd
azdata login -e https://<controller DNS name>:30080 --auth ad
```

### <a name="use-ad-authentication-to-knox-gateway-webhdfs"></a>Usare l'autenticazione di Active Directory per il gateway Knox (webHDFS)

È anche possibile emettere comandi HDFS usando curl attraverso l'endpoint del gateway Knox. A questo scopo, è necessaria l'autenticazione di Active Directory per Knox. Il comando curl seguente effettua una chiamata REST webHDFS tramite il gateway Knox per creare una directory denominata `products`

```bash
curl -k -v --negotiate -u : https://<Gateway DNS name>:30443/gateway/default/webhdfs/v1/products?op=MKDIRS -X PUT
```

## <a name="known-issues-and-limitations"></a>Problemi noti e limitazioni

**Limitazioni da tenere presenti in SQL Server 2019 CU5**

- Attualmente, il dashboard Ricerca log e il dashboard Metriche non supportano l'autenticazione di Active Directory. Per l'autenticazione a questi dashboard è possibile usare il nome utente e la password di base impostati in fase di distribuzione. Tutti gli altri endpoint del cluster supportano l'autenticazione di Active Directory.

- La modalità Active Directory sicura funziona attualmente solo negli ambienti di distribuzione `kubeadm` e `openshift` e non nel servizio Azure Kubernetes o in Azure Red Hat OpenShift. I profili di distribuzione `kubeadm-prod` e `openshift-prod` includono le sezioni di sicurezza per impostazione predefinita.

- Prima di SQL Server 2019 CU5, era consentito un solo BDC per dominio (Active Directory). L'abilitazione di più BDC per dominio è una funzionalità disponibile a partire dalla versione CU5.

- Nessuno dei gruppi AD specificati nelle configurazioni di sicurezza può avere l'ambito DomainLocal. È possibile controllare l'ambito di un gruppo di Active Directory seguendo [queste istruzioni](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps).

- L'account AD che può essere usato per accedere al BDC è consentito dallo stesso dominio configurato per il BDC. L'abilitazione di account di accesso da altri domini attendibili non è supportata.

## <a name="next-steps"></a>Passaggi successivi

[Risolvere i problemi di integrazione di Active Directory di cluster Big Data di SQL Server](troubleshoot-active-directory.md)

[Concetto: distribuire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in modalità Active Directory](active-directory-deployment-background.md)
