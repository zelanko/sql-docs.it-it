---
title: Distribuire un cluster Big Data di SQL Server in modalità Active Directory
titleSuffix: Deploy SQL Server Big Data Cluster in Active Directory mode
description: Informazioni su come aggiornare un cluster Big Data di SQL Server in un dominio di Active Directory.
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: eab7fa5a123f6370686cae5feaf36d458748ea7a
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844306"
---
# <a name="deploy-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-in-active-directory-mode"></a>Distribuire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in modalità Active Directory

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come distribuire un cluster Big Data di SQL Server 2019 in modalità di autenticazione di Active Directory, operazione in cui viene usato un dominio di Active Directory esistente per l'autenticazione.

## <a name="background"></a>Informazioni preliminari

Per abilitare l'autenticazione di Active Directory, il cluster Big Data crea automaticamente gli utenti, i gruppi, gli account computer e i nomi dell'entità servizio (SPN) necessari per i vari servizi nel cluster. Per assicurare una certa indipendenza per questi account e consentire autorizzazioni di ambito, durante la distribuzione indicare un'unità organizzativa in cui verranno creati tutti gli oggetti di Active Directory correlati al cluster Big Data. Creare questa unità organizzativa prima della distribuzione del cluster.

Per creare automaticamente tutti gli oggetti necessari in Active Directory, il cluster Big Data necessita di un account Active Directory durante la distribuzione. Questo account deve avere le autorizzazioni necessarie per la creazione di utenti, gruppi e account computer all'interno dell'unità organizzativa specificata.

La procedura seguente presuppone l'esistenza di un controller di dominio Active Directory. Se non è presente alcun controller di dominio, la [guida](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx) seguente include alcuni passaggi che possono essere utili.

## <a name="create-ad-objects"></a>Creare oggetti di Active Directory

Prima di distribuire un cluster Big Data con l'integrazione di Active Directory, eseguire le operazioni seguenti:

1. Creare un'unità organizzativa (OU), in cui verranno archiviati tutti gli oggetti di Active Directory del cluster Big Data. È anche possibile scegliere di indicare un'unità organizzativa esistente in fase di distribuzione.
1. Creare un account Active Directory per il cluster Big Data oppure usarne uno esistente e fornire a questo account le autorizzazioni appropriate.

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>Creare un utente in Active Directory per l'account del servizio di dominio del cluster Big Data

Il cluster Big Data deve avere un account con autorizzazioni specifiche. Prima di continuare, assicurarsi che sia già presente un account Active Directory oppure crearne uno nuovo, che può essere usato dal cluster Big Data per configurare gli oggetti necessari.

Per creare un nuovo utente in Active Directory, è possibile fare clic con il pulsante destro del mouse sul dominio o sull'unità organizzativa e scegliere **Nuovo** > **Utente**:

![immagine12](./media/deploy-active-directory/image12.png)

Questo utente verrà definito *account del servizio di dominio del cluster Big Data* in questo articolo.

### <a name="creating-an-ou"></a>Creazione di un'unità organizzativa

Nel controller di dominio aprire **Utenti e computer di Active Directory**. Nel pannello sinistro fare clic con il pulsante destro del mouse sulla directory in cui si vuole creare l'unità organizzativa e scegliere Nuovo -\> **Unità organizzativa** e quindi seguire le istruzioni della procedura guidata per creare l'unità organizzativa. In alternativa, è possibile creare un'unità organizzativa con PowerShell:

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

Negli esempi contenuti in questo articolo, l'unità organizzativa è denominata `bdc`

![immagine13](./media/deploy-active-directory/image13.png)

![immagine14](./media/deploy-active-directory/image14.png)

### <a name="setting-permissions-the-bdc-ad-account"></a>Impostazione delle autorizzazioni per l'account Active Directory del cluster Big Data

Se è stato creato un nuovo utente di Active Directory o se ne usa uno esistente, l'utente deve avere determinate autorizzazioni. Questo account è l'account utente che verrà usato dal controller del cluster Big Data per l'aggiunta del cluster ad Active Directory.

L'account del servizio di dominio del cluster Big Data deve essere in grado di creare utenti, gruppi e account computer nell'unità organizzativa. Nei passaggi seguenti l'account del servizio di dominio del cluster Big Data è denominato `bdcDSA`. È possibile scegliere qualsiasi nome per l'account.

1. Nel controller di dominio aprire **Utenti e computer di Active Directory**

1. Nel pannello sinistro passare al dominio, quindi all'unità organizzativa che verrà usata da `bdc`

1. Fare clic con il pulsante destro del mouse sull'unità organizzativa e quindi scegliere **Proprietà**.

1. Passare alla scheda Sicurezza, assicurandosi di aver selezionato **Funzionalità avanzate**, di avere fatto clic con il pulsante destro del mouse sull'unità organizzativa e quindi di avere scelto **Visualizza**

    ![immagine15](./media/deploy-active-directory/image15.png)

1. Fare clic su **Aggiungi** e aggiungere l'utente **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA**

    ![immagine16](./media/deploy-active-directory/image16.png)

    ![immagine17](./media/deploy-active-directory/image17.png)

1. Selezionare l'utente **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA** e deselezionare tutte le autorizzazioni, quindi fare clic su **Avanzate**

1. Fare clic su **Aggiungi**

    ![immagine18](./media/deploy-active-directory/image18.png)

    - Fare clic su **Selezionare un'entità**, immettere **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA** e fare clic su OK

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
       - **Create User objects** (Crea oggetti utente)

    - Fare clic su **OK**.

- Fare clic su **Aggiungi**

    - Fare clic su **Selezionare un'entità**, immettere **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA** e fare clic su OK

    - Impostare **Tipo** su **Consenti**

    - Impostare **Si applica a** su **Descendant Computer objects** (Oggetti computer discendenti)

    - Scorrere fino alla fine e fare clic su **Cancella tutto**

    - Tornare all'inizio e selezionare **Reimposta password**

    - Fare clic su **OK**.

- Fare clic su **Aggiungi**

    - Fare clic su **Selezionare un'entità**, immettere **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA** e fare clic su OK

    - Impostare **Tipo** su **Consenti**

    - Impostare **Si applica a** su **Descendant User objects** (Oggetti utente discendenti)

    - Scorrere fino alla fine e fare clic su **Cancella tutto**

    - Tornare all'inizio e selezionare **Reimposta password**

    - Fare clic su **OK**.

- Fare clic su **OK** altre due volte per chiudere le finestre di dialogo aperte

## <a name="prepare-deployment"></a>Preparare la distribuzione

Per la distribuzione di un cluster Big Data con l'integrazione di Active Directory, è necessario fornire alcune informazioni aggiuntive per la creazione degli oggetti correlati al cluster Big Data in Active Directory.

Usando il profilo `kubeadm-prod`, verranno automaticamente immessi i segnaposto per le informazioni relative alla sicurezza e all'endpoint necessarie per l'integrazione di Active Directory.

Inoltre, è necessario fornire le credenziali che verranno usate da [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] per creare gli oggetti necessari in Active Directory. Queste credenziali vengono fornite come variabili di ambiente.

## <a name="set-security-environment-variables"></a>Impostare le variabili di ambiente di sicurezza

Le variabili di ambiente seguenti forniscono le credenziali per l'account del servizio di dominio del cluster Big Data, che verrà usato per configurare l'integrazione di Active Directory. Questo account viene usato anche dal cluster Big Data per mantenere gli oggetti di Active Directory correlati al cluster Big Data stesso in futuro.

```bash
export DOMAIN_SERVICE_ACCOUNT_USERNAME=<AD principal account name>
export DOMAIN_SERVICE_ACCOUNT_PASSWORD=<AD principal password>
```

## <a name="provide-security-and-endpoint-parameters"></a>Fornire parametri di sicurezza e dell'endpoint

Oltre alle variabili di ambiente per le credenziali, è necessario fornire anche le informazioni sulla sicurezza e sull'endpoint per il funzionamento dell'integrazione di Active Directory. I parametri necessari fanno automaticamente parte del [profilo di distribuzione](deployment-guidance.md#configfile) `kubeadm-prod`.

Per l'integrazione di Active Directory sono necessari i parametri seguenti. Aggiungere questi parametri ai file `control.json` e `bdc.json` usando i comandi `config replace` mostrati più avanti in questo articolo. Tutti gli esempi seguenti usano il dominio di esempio `contoso.local`.

- `security.ouDistinguishedName`: nome distinto di un'unità organizzativa (OU) in cui verranno aggiunti tutti gli account Active Directory creati tramite la distribuzione del cluster. Se il dominio è denominato `contoso.local`, il nome distinto dell'unità organizzativa è: `OU=BDC,DC=contoso,DC=local`.

- `security.dnsIpAddresses`: elenco di indirizzi IP dei controller di dominio

- `security.domainControllerFullyQualifiedDns`: elenco di nomi di dominio completi del controller di dominio. Il nome di dominio completo contiene il nome computer/host del controller di dominio. Se sono presenti più controller di dominio, è possibile fornirne un elenco qui. Esempio: `HOSTNAME.CONTOSO.LOCAL`

- **Parametro facoltativo** `security.realm`: nella maggior parte dei casi, l'area di autenticazione è uguale al nome di dominio. Per i casi in cui non sono uguali, usare questo parametro per definire il nome dell'area di autenticazione, ad esempio `CONTOSO.LOCAL`.

- `security.domainDnsName`: Nome del dominio, ad esempio `contoso.local`.

- `security.clusterAdmins`: questo parametro accetta *un* gruppo di Active Directory. I membri di questo gruppo otterranno autorizzazioni di amministratore nel cluster. Questo significa che avranno autorizzazioni sysadmin in SQL Server, autorizzazioni utente con privilegi avanzati in HDFS e autorizzazioni di amministratore nel controller.

- `security.clusterUsers`: elenco dei gruppi di Active Directory che sono utenti normali (senza autorizzazioni di amministratore) nel cluster Big Data.

- **Parametro facoltativo** `security.appOwners`: elenco dei gruppi di Active Directory che hanno le autorizzazioni necessarie per creare, eliminare ed eseguire qualsiasi applicazione.

- **Parametro facoltativo** `security.appReaders`: elenco degli utenti o dei gruppi di Active Directory che hanno le autorizzazioni necessarie per eseguire qualsiasi applicazione. 

Se il file di configurazione della distribuzione non è stato ancora inizializzato, è possibile eseguire questo comando per ottenere una copia della configurazione.

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

Per impostare i parametri precedenti nel file `control.json`, usare i comandi `azdata` seguenti. I comandi sostituiscono la configurazione e forniscono i valori personalizzati prima della distribuzione.

L'esempio seguente sostituisce i valori relativi ad Active Directory nella configurazione della distribuzione. I dettagli del dominio riportati di seguito sono valori di esempio.

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterAdmins=[\"bdcadmins\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterUsers=[\"bdcusers1\,bdcusers2\"]"
```

Oltre alle informazioni precedenti, è necessario fornire anche i nomi DNS per i diversi endpoint del cluster. In fase di distribuzione verranno automaticamente create le voci DNS che usano i nomi DNS specificati nel server DNS. Questi nomi verranno usati durante la connessione ai diversi endpoint del cluster. Se, ad esempio, il nome DNS per l'istanza master di SQL Server è `mastersql`, si userà `mastersql.contoso.local,31433` per connettersi all'istanza master dagli strumenti.

> [!NOTE]
> Assicurarsi di creare voci DNS nel server DNS per i nomi definiti di seguito. Per le distribuzioni `kubeadm`, ad esempio, è possibile usare l'indirizzo IP del nodo master Kubernetes durante la creazione delle voci DNS.

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[1].dnsName=<monitoring services DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=<SQL Master Primary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=<SQL Master Secondary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=<Gateway (Knox) DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=<app proxy DNS name>.<Domain name. e.g. contoso.local>"
```

Qui è possibile trovare uno script di esempio per la [distribuzione di un cluster Big Data di SQL Server in un cluster Kubernetes a nodo singolo (kubeadm) con l'integrazione di AD](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm-ad).

A questo punto, sono stati impostati tutti i parametri necessari per una distribuzione del cluster Big Data con l'integrazione di Active Directory.

Per la documentazione completa su come distribuire [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)], fare riferimento alla [documentazione ufficiale](deployment-guidance.md).

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

È possibile connettersi all'endpoint controller tramite `azdata` e l'autenticazione di Active Directory.

```bash
kinit <username>@<domain name>
azdata login -e https://<controller DNS name>:30080 --auth ad
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

**È bene considerare alcune limitazioni in questa versione:**

- Attualmente, il dashboard Ricerca log e il dashboard Metriche non supportano l'autenticazione di Active Directory. Il supporto di Active Directory per questo endpoint sarà disponibile in una versione futura. Per l'autenticazione a questi dashboard è possibile usare il nome utente e la password di base impostati in fase di distribuzione. Tutti gli altri endpoint del cluster supportano l'autenticazione di Active Directory.

- La modalità Active Directory sicura funziona attualmente solo negli ambienti di distribuzione `kubeadm` e non nel servizio Azure Kubernetes. Il profilo di distribuzione `kubeadm-prod` include le sezioni di sicurezza per impostazione predefinita.

- Attualmente è consentito un solo cluster Big Data per dominio. L'abilitazione di più cluster Big Data per dominio verrà introdotta in una versione futura.
