---
title: Gestione connessione Hadoop | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopconn.f1
ms.assetid: 8bb15b97-9827-46bc-aca6-068534ab18c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4cf042d2ab9c2d3e7c492fa008282cbcbe730f8e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85735106"
---
# <a name="hadoop-connection-manager"></a>Gestione connessione Hadoop

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Gestione connessione Hadoop consente al pacchetto SQL Server Integration Services (SSIS) di connettersi a un cluster Hadoop usando i valori specificati per le proprietà.  
  
## <a name="configure-the-hadoop-connection-manager"></a>Configurare la gestione connessione Hadoop  
  
1.  Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare **Hadoop** > **Aggiungi**. Verrà visualizzata la finestra di dialogo **Editor gestione connessione Hadoop** .  
  
2.  Per configurare le informazioni del cluster Hadoop correlate, scegliere la scheda **WebHCat** o **WebHDFS** nel riquadro a sinistra.
  
3.  Se si abilita l'opzione **WebHCat** per richiamare un processo Hive o Pig in Hadoop, seguire questa procedura: 
  
    1.  Per **Host WebHCat**, immettere il server che ospita il servizio WebHCat.  
  
    2.  Per **Porta WebHCat**, immettere la porta del servizio WebHCat, che per impostazione predefinita è 50111.  
  
    3.  Selezionare il metodo di **Autenticazione** per accedere al servizio WebHCat. I valori disponibili sono **Base** e **Kerberos**.  
  
         ![Screenshot dell'Editor gestione connessione Hadoop con autenticazione di base](../../integration-services/connection-manager/media/hadoop-cm-basic.png "Editor gestione connessione Hadoop con autenticazione di base")  
  
         ![Screenshot dell'Editor gestione connessione Hadoop con autenticazione Kerberos](../../integration-services/connection-manager/media/hadoop-cm-kerberos.png "Editor gestione connessione Hadoop con autenticazione Kerberos")  
  
    4.  Per **Utente WebHCat**immettere l' **Utente** autorizzato ad accedere a WebHCat.  
  
    5.  Se si seleziona l'autenticazione **Kerberos** , immettere la **Password** e il **Dominio**dell'utente.  
  
4.  Se si abilita l'opzione **WebHDFS** per copiare i dati da o a HDFS, seguire questa procedura: 
  
    1.  Per **Host WebHDFS**, immettere il server che ospita il servizio WebHDFS.  
  
    2.  Per **Porta WebHDFS**, immettere la porta del servizio WebHDFS, che per impostazione predefinita è 50070.  
  
    3.  Selezionare il metodo di **Autenticazione** per accedere al servizio WebHDFS. I valori disponibili sono **Base** e **Kerberos**.  
  
    4.  Per **Utente WebHDFS**immettere l'utente autorizzato ad accedere a HDFS.  
  
    5.  Se si seleziona l'autenticazione **Kerberos** , immettere la **Password** e il **Dominio**dell'utente.  
  
5.  Selezionare **Test connessione**. (verrà testata solo la connessione abilitata).  
  
6.  Selezionare **OK** per chiudere la finestra di dialogo.  

## <a name="connect-with-kerberos-authentication"></a>Connettersi con l'autenticazione Kerberos
Esistono due opzioni per configurare l'ambiente locale per poter usare l'autenticazione Kerberos con Gestione connessione Hadoop. È possibile scegliere l'opzione che meglio si adatta alle circostanze.
-   Opzione 1: [Aggiungere il computer SSIS all'area di autenticazione Kerberos](#kerberos-join-realm)
-   Opzione 2: [Abilitare il trust reciproco tra il dominio Windows e l'area di autenticazione Kerberos](#kerberos-mutual-trust)

### <a name="option-1-join-the-ssis-computer-to-the-kerberos-realm"></a><a name="kerberos-join-realm"></a>Opzione 1: Aggiungere il computer SSIS all'area di autenticazione Kerberos

#### <a name="requirements"></a>Requisiti:

-   Il computer gateway deve essere aggiunto all'area di autenticazione Kerberos e non può essere aggiunto a domini Windows.

#### <a name="how-to-configure"></a>Modalità di configurazione:

Nel computer SSIS:

1.  Eseguire l'utilità **Ksetup** per configurare l'area di autenticazione e il server Centro distribuzione chiavi (KDC) Kerberos.

    Il computer deve essere configurato come membro di un gruppo di lavoro, perché un'area di distribuzione Kerberos è diversa da un dominio Windows. Impostare l'area di autenticazione Kerberos e aggiungere un server KDC, come illustrato nell'esempio seguente. Sostituire `REALM.COM` con la propria rispettiva area di autenticazione, se necessario.

    ```console
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    ```

    Dopo aver eseguito questi comandi, riavviare il computer.

2.  Verificare la configurazione con il comando **Ksetup**. L'output dovrebbe avere un aspetto simile all'esempio seguente:

    ```console
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
    ```

### <a name="option-2-enable-mutual-trust-between-the-windows-domain-and-the-kerberos-realm"></a><a name="kerberos-mutual-trust"></a>Opzione 2: Abilitare il trust reciproco tra il dominio Windows e l'area di autenticazione Kerberos

#### <a name="requirements"></a>Requisiti:
-   Il computer gateway deve fare parte di un dominio Windows.
-   È necessaria l'autorizzazione per aggiornare le impostazioni del controller di dominio.

#### <a name="how-to-configure"></a>Modalità di configurazione:

> [!NOTE]
> Sostituire `REALM.COM` e `AD.COM` nell'esercitazione seguente con la propria area di autenticazione e il proprio controller di dominio, se necessario.

Nel server KDC:

1.  Modificare la configurazione KDC nel file **krb5.conf**. Consentire a KDC di considerare attendibile il dominio Windows facendo riferimento al modello di configurazione seguente. Per impostazione predefinita, la configurazione si trova in **/etc/krb5.conf**.

    ```console
    [logging]
    default = FILE:/var/log/krb5libs.log
    kdc = FILE:/var/log/krb5kdc.log
    admin_server = FILE:/var/log/kadmind.log

    [libdefaults]
    default_realm = REALM.COM
    dns_lookup_realm = false
    dns_lookup_kdc = false
    ticket_lifetime = 24h
    renew_lifetime = 7d
    forwardable = true

    [realms]
    REALM.COM = {
        kdc = node.REALM.COM
        admin_server = node.REALM.COM
        }
    AD.COM = {
        kdc = windc.ad.com
        admin_server = windc.ad.com
        }

    [domain_realm]
    .REALM.COM = REALM.COM
    REALM.COM = REALM.COM
    .ad.com = AD.COM
    ad.com = AD.COM

    [capaths]
    AD.COM = {
        REALM.COM = .
        }
    ```

    Dopo la configurazione, riavviare il servizio KDC.

2.  Preparare un'entità denominata **krbtgt/REALM.COM\@AD.COM** nel server KDC. Usare il comando seguente:

    `Kadmin> addprinc krbtgt/REALM.COM@AD.COM`

3.  Nel file di configurazione del servizio HDFS **hadoop.security.auth_to_local** aggiungere `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.

Nel controller di dominio:

1.  Eseguire i comandi **Ksetup** seguenti per aggiungere una voce dell'area di autenticazione:

    ```console
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

2.  Stabilire il trust dal dominio Windows all'area di autenticazione Kerberos. Nell'esempio seguente `[password]` è la password per l'entità di sicurezza **krbtgt/REALM.COM\@AD.COM**.

    `C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /password:[password]`

3.  Selezionare un algoritmo di crittografia da usare con Kerberos.

    1. Andare a **Server Manager** > **Gestione Criteri di gruppo** > **Dominio**. Andare quindi a **Oggetti Criteri di gruppo** > **Default or Active Domain Policy** (Criteri dominio predefiniti o attivi) > **Modifica**.

    2. Nella finestra popup **Editor Gestione Criteri di gruppo** andare a **Configurazione computer** > **Criteri** > **Impostazioni di Windows**. Andare quindi a **Impostazioni di sicurezza** > **Criteri locali** > **Opzioni di sicurezza**. Configurare **Sicurezza di rete: configura tipi di crittografia consentiti per Kerberos**.

    3. Selezionare l'algoritmo di crittografia che si vuole usare per connettersi al Centro distribuzione chiavi. È in genere possibile selezionare qualsiasi opzione.

        ![Screenshot dei tipi di crittografia per Kerberos](media/hadoop-connection-manager/config-encryption-types-for-kerberos.png)

    4. Usare il comando **Ksetup** per specificare l'algoritmo di crittografia da usare nell'area di autenticazione specifica.

        `C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96`

4.  Per usare l'entità di sicurezza Kerberos nel dominio Windows, creare il mapping tra l'account di dominio e l'entità di sicurezza Kerberos.

    1. Andare a **Strumenti di amministrazione** > **Utenti e computer di Active Directory**.

    2. Configurare le funzionalità avanzate selezionando **Visualizza** > **Funzionalità avanzate**.

    3. Individuare l'account a cui si vuole creare i mapping, fare clic con il pulsante destro del mouse per visualizzare **Mapping nomi** e quindi scegliere la scheda **Nomi Kerberos**.

    4. Aggiungere un'entità di sicurezza dall'area di autenticazione.

        ![Screenshot della finestra di dialogo Mapping identità di sicurezza](media/hadoop-connection-manager/map-security-identity.png)

Nel computer del gateway:

Eseguire i comandi **Ksetup** seguenti per aggiungere una voce dell'area di autenticazione.

```console
C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
```

## <a name="see-also"></a>Vedere anche  
 [Attività Hive Hadoop](../../integration-services/control-flow/hadoop-hive-task.md)   
 [Attività Pig Hadoop](../../integration-services/control-flow/hadoop-pig-task.md)   
 [Attività File system Hadoop](../../integration-services/control-flow/hadoop-file-system-task.md)  
  
  
