---
title: Connettersi a origini dati e condivisioni file con autenticazione di Windows | Microsoft Docs
description: Informazioni su come configurare il catalogo SSIS nel database SQL di Azure e nel runtime di integrazione Azure-SSIS per eseguire pacchetti che usano l'autenticazione di Windows per connettersi a origini dati e condivisioni file.
ms.date: 10/11/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 61d4d29b0dfc7fe67097c6cb61547c1c65dd79f1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52411878"
---
# <a name="connect-to-data-sources-and-file-shares-with-windows-authentication-from-ssis-packages-in-azure"></a>Connettersi a origini dati e condivisioni file con l'autenticazione di Windows da pacchetti SSIS in Azure
È possibile usare l'autenticazione di Windows per connettersi alle origini dati e alle condivisioni file nella stessa rete virtuale del runtime di integrazione Azure-SSIS, sia in locale che nelle macchine virtuali di Azure e in File di Azure. Esistono tre metodi per la connessione alle origini dati e alle condivisioni file con l'autenticazione di Windows da pacchetti SSIS in esecuzione nel runtime di integrazione Azure-SSIS:

| Metodo di connessione | Ambito effettivo | Passaggio di configurazione | Metodo di accesso nei pacchetti | Numero di set di credenziali e risorse connesse | Tipo di risorse connesse | 
|---|---|---|---|---|---|
| Rendere persistenti le credenziali tramite il comando `cmdkey` | Per ogni runtime di integrazione Azure-SSIS | Eseguire il comando `cmdkey` in uno script di installazione personalizzato (`main.cmd`) durante il provisioning o la riconfigurazione del runtime di integrazione Azure-SSIS, ad esempio `cmdkey /add:fileshareserver /user:xxx /pass:yyy`.<br/><br/> Per altre informazioni, vedere [Customize setup for Azure-SSIS IR](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup) (Personalizzare l'installazione per il runtime di integrazione Azure-SSIS). | Accedere alle risorse direttamente nei pacchetti tramite un percorso UNC, ad esempio, `\\fileshareserver\folder` | Sono supportati più set di credenziali per risorse connesse diverse | - Condivisioni file in macchine virtuali locali/di Azure<br/><br/> - File di Azure, vedere [Montare una condivisione file di Azure](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) <br/><br/> - SQL Server con l'autenticazione di Windows<br/><br/> - Altre risorse con l'autenticazione di Windows |
| Configurazione di un contesto di esecuzione a livello di catalogo | Per ogni runtime di integrazione Azure-SSIS | Eseguire la stored procedure SSISDB `catalog.set_execution_credential` per configurare un contesto di "esecuzione come".<br/><br/> Per altre informazioni, vedere il resto di questo articolo. | Accedere alle risorse direttamente nei pacchetti | È supportato un solo set di credenziali per tutte le risorse connesse | - Condivisioni file in macchine virtuali locali/di Azure<br/><br/> - File di Azure, vedere [Montare una condivisione file di Azure](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) <br/><br/> - SQL Server con l'autenticazione di Windows<br/><br/> - Altre risorse con l'autenticazione di Windows | 
| Montaggio di unità in fase di esecuzione del pacchetto (senza persistenza) | Per pacchetto | Eseguire il comando `net use` nell'attività Esegui processo aggiunta all'inizio del flusso di controllo nei pacchetti, ad esempio, `net use D: \\fileshareserver\sharename` | Accedere alle condivisioni file tramite unità mappate | Sono supportate più unità per condivisioni file diverse | - Condivisioni file in macchine virtuali locali/di Azure<br/><br/> - File di Azure, vedere [Montare una condivisione file di Azure](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) |
|||||||

> [!WARNING]
> Se non si usa uno dei metodi sopra riportati per la connessione a origini dati e condivisioni file con l'autenticazione di Windows, i pacchetti che dipendono dall'autenticazione di Windows non saranno in grado di connettersi e causeranno errori in fase di esecuzione. 

Il resto di questo articolo descrive come configurare il catalogo SSIS nel database SQL di Azure per eseguire pacchetti che usano l'autenticazione di Windows per connettersi a origini dati e condivisioni file. 

## <a name="you-can-only-use-one-set-of-credentials"></a>È possibile usare un solo set di credenziali
Quando si usa l'autenticazione di Windows in un pacchetto SSIS, è possibile usare un solo set di credenziali in un pacchetto. Le credenziali del dominio specificate quando si esegue la procedura illustrata in questo articolo sono valide per tutte le esecuzioni di pacchetti interattive o pianificate nel runtime di integrazione Azure-SSIS, finché non si modificano o rimuovono le credenziali. Se il pacchetto deve connettersi a più origini dati e condivisioni file con set di credenziali diversi, potrebbe essere necessario prendere in considerazione i metodi alternativi descritti in precedenza.

## <a name="provide-domain-credentials-for-windows-authentication"></a>Fornire le credenziali di dominio per l'autenticazione di Windows
Per specificare le credenziali del dominio che consentono ai pacchetti che usano l'autenticazione di Windows di connettersi alle origini dati locali e alle condivisioni file, seguire questa procedura:

1.  Con SQL Server Management Studio (SSMS) o un altro strumento connettersi al database SQL che ospita il database del catalogo SSIS (SSISDB). Per altre informazioni, vedere [Connettersi al database del catalogo SSIS (SSISDB) in Azure](ssis-azure-connect-to-catalog-database.md).

2.  Con SSISDB come database corrente, aprire una finestra di query.

3.  Eseguire la seguente stored procedure e specificare le credenziali del dominio appropriate:

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```

4.  Eseguire i pacchetti SSIS. I pacchetti usano le credenziali specificate per connettersi alle origini dati locali e alle condivisioni file con l'autenticazione di Windows.

### <a name="view-domain-credentials"></a>Visualizzare le credenziali del dominio
Per visualizzare le credenziali del dominio attive, eseguire queste operazioni:

1.  Con SQL Server Management Studio (SSMS) o un altro strumento connettersi al database SQL che ospita il database del catalogo SSIS (SSISDB).

2.  Con SSISDB come database corrente, aprire una finestra di query.

3.  Eseguire la stored procedure seguente e controllare l'output:

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

### <a name="clear-domain-credentials"></a>Cancellare le credenziali del dominio
Per cancellare e rimuovere le credenziali specificate come descritto in questo articolo, eseguire queste operazioni:

1.  Con SQL Server Management Studio (SSMS) o un altro strumento connettersi al database SQL che ospita il database del catalogo SSIS (SSISDB).

2.  Con SSISDB come database corrente, aprire una finestra di query.

3.  Eseguire la stored procedure seguente:

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-an-on-premises-sql-server"></a>Connettersi a SQL Server locale
Per verificare se è possibile connettersi a un'istanza di SQL Server locale, eseguire le operazioni seguenti:

1.  Per eseguire questo test, cercare un computer non appartenente al dominio.

2.  Nel computer non appartenente al dominio eseguire il comando riportato di seguito per avviare SQL Server Management Studio (SSMS) con le credenziali del dominio che si vuole usare:

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  Controllare da SSMS se è possibile connettersi all'istanza di SQL Server locale che si prevede di usare.

### <a name="prerequisites"></a>Prerequisites
Per connettersi a SQL Server locale da un pacchetto in esecuzione in Azure, è necessario abilitare i prerequisiti seguenti:

1.  In Gestione configurazione SQL Server abilitare il protocollo TCP/IP.
2.  Consentire l'accesso a un programma attraverso Windows Firewall. Per altre informazioni, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](https://docs.microsoft.com/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access).
3.  Per connettersi con l'autenticazione di Windows, verificare che il runtime di integrazione Azure-SSIS appartenga a una rete virtuale che include anche SQL Server locale.  Per altre informazioni, vedere [Aggiungere un runtime di integrazione SSIS di Azure a una rete virtuale](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network). Usare quindi `catalog.set_execution_credential` per fornire le credenziali, come illustrato in questo articolo.

## <a name="connect-to-an-on-premises-file-share"></a>Connettersi a una condivisione file locale
Per testare se è possibile connettersi a una condivisione file locale, seguire questa procedura:

1.  Per eseguire questo test, cercare un computer non appartenente al dominio.

2.  Nel computer non appartenente al dominio eseguire questo comando. Il comando apre una finestra del prompt dei comandi con le credenziali del dominio che si vuole usare, quindi verifica la connettività della condivisione file recuperando un elenco di directory.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  Verificare se viene restituito l'elenco di directory per la condivisione file locale che si vuole usare.

## <a name="connect-to-a-file-share-on-an-azure-vm"></a>Connettersi a una condivisione file in una VM di Azure
Per connettersi a una condivisione file in una macchina virtuale di Azure, seguire questa procedura:

1.  Con SQL Server Management Studio (SSMS) o un altro strumento connettersi al database SQL che ospita il database del catalogo SSIS (SSISDB).

2.  Con SSISDB come database corrente, aprire una finestra di query.

3.  Eseguire la stored procedure `catalog.set_execution_credential` come descritto nelle opzioni seguenti:

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="connect-to-a-file-share-in-azure-files"></a>Connettersi a una condivisione file in File di Azure
Per altre informazioni sui file di Azure, vedere [File di Azure](https://azure.microsoft.com/services/storage/files/).

Per connettersi a una condivisione file in File di Azure, seguire questa procedura:

1.  Con SQL Server Management Studio (SSMS) o un altro strumento connettersi al database SQL che ospita il database del catalogo SSIS (SSISDB).

2.  Con SSISDB come database corrente, aprire una finestra di query.

3.  Eseguire la stored procedure `catalog.set_execution_credential` come descritto nelle opzioni seguenti:

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>Passaggi successivi
- Distribuire un pacchetto. Per altre informazioni, vedere [Distribuire un progetto SSIS con SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md).
- Eseguire un pacchetto. Per altre informazioni, vedere [Eseguire un pacchetto SSIS con SQL Server Management Studio (SSMS)](../ssis-quickstart-run-ssms.md).
- Pianificare un pacchetto. Per altre informazioni, vedere [Pianificare i pacchetti SSIS in Azure](ssis-azure-schedule-packages.md).
