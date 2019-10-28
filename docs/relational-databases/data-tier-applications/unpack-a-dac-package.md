---
title: Decompressione di un pacchetto di applicazione livello dati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- wizard [DAC], unpack
- data-tier application [SQL Server], unpack
- How to [DAC], unpack
- unpack DAC
ms.assetid: 697b69b3-f157-4e22-ac4e-f65c5fc2d0ad
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5e2be902c241403ec044b3d348f90dc85327b8ad
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909528"
---
# <a name="unpack-a-dac-package"></a>Decompressione di un pacchetto di applicazione livello dati
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Utilizzare la finestra di dialogo per la decompressione dell'applicazione livello dati per decomprimere gli script e i file da un pacchetto di applicazioni livello dati (DAC). Gli script e i file vengono copiati in una cartella dove è possibile controllarli prima che il pacchetto venga utilizzato per distribuire l'applicazione del livello dati in un sistema di produzione. È inoltre possibile confrontare il contenuto di un pacchetto di applicazione livello dati con il contenuto di un altro pacchetto decompresso in un'altra cartella.  
  
1.  **Prima di iniziare:**  [Sicurezza](#Security)  
  
2.  **Per decomprimere un'applicazione livello dati tramite la**  [Finestra di dialogo per la decompressione dell'applicazione livello dati](#UnpackDACDial), [Verifica del contenuto di un pacchetto di applicazione livello dati](#ExamDACPack)  

##  <a name="Security"></a> Sicurezza  
 È consigliabile evitare di distribuire un pacchetto di applicazione livello dati proveniente da origini sconosciute o non attendibili. Tali pacchetti DAC possono contenere codice dannoso che potrebbe eseguire codice [!INCLUDE[tsql](../../includes/tsql-md.md)] indesiderato o causare errori modificando lo schema. Prima di utilizzare un pacchetto di applicazione livello dati proveniente da un'origine sconosciuta o non attendibile, distribuirlo in un'istanza di prova isolata del [!INCLUDE[ssDE](../../includes/ssde-md.md)], decomprimere il pacchetto di applicazione livello dati ed esaminare il codice, ad esempio stored procedure o altro codice definito dall'utente.  
  
##  <a name="UnpackDACDial"></a> la finestra di dialogo per la decompressione dell'applicazione livello dati  
 **Per decomprimere un file del pacchetto di applicazione livello dati**  
  
-   In **Esplora risorse**passare al percorso di un file del pacchetto di applicazione livello dati (con estensione dacpac).  
  
-   Utilizzare uno di questi due metodi per aprire la finestra di dialogo per la decompressione dell'applicazione livello dati:  
  
    1.  Fare clic con il pulsante destro del mouse sul file del pacchetto di applicazione livello dati (con estensione dacpac) e scegliere **Decomprimi**.  
  
    2.  Fare doppio clic sul file del pacchetto di applicazione livello dati.  
  
-   Completare le finestre di dialogo:  
  
    -   [Decomprimi file di pacchetto DAC di Microsoft SQL Server](#Unpack)  
  
    -   [Sfoglia cartella](#Browse)  
  
###  <a name="Unpack"></a> Decomprimi file di pacchetto DAC di Microsoft SQL Server  
 Utilizzare questa pagina per specificare la cartella di destinazione nella quale copiare i file decompressi, quindi eseguire l'operazione di decompressione.  
  
 **I file verranno decompressi nella cartella seguente** : consente di specificare il percorso completo della cartella per i file decompressi. Se la cartella esiste e se ne conosce il percorso completo, digitare il percorso nella casella. In caso contrario, fare clic sul pulsante **Sfoglia** per passare a una cartella o crearne una nuova.  
  
 **Sfoglia** : apre la pagina **Sfoglia cartella** in cui è possibile scegliere una cartella spostandosi all'interno della gerarchia dei file oppure creare una nuova cartella.  
  
 **Decomprimi** : avvia l'operazione di decompressione.  
  
 **Annulla** : chiude la finestra di dialogo senza decomprimere il pacchetto di applicazione livello dati.  
  
###  <a name="Browse"></a> Sfoglia cartella  
 Utilizzare questa pagina per scegliere la cartella di destinazione per l'operazione di decompressione. Facoltativamente, è inoltre possibile creare una nuova cartella.  
  
 **Elenco di cartelle** : visualizza la gerarchia dei file per il computer. Espandere i nodi per passare alla cartella nella quale decomprimere il pacchetto DAC. Fare clic sulla cartella e quindi scegliere **OK**.  
  
 **Crea nuova cartella** : apre una finestra di dialogo nella quale è possibile specificare il nome per una nuova cartella da creare nella cartella attualmente selezionata nella gerarchia di cartelle.  
  
 **OK** : imposta il percorso della cartella selezionato nella casella **I file verranno decompressi nella cartella seguente** della pagina **Decomprimi file pacchetto DAC** e torna a tale pagina.  
  
 **Annulla** : chiude la finestra di dialogo senza selezionare una cartella.  
  
##  <a name="ExamDACPack"></a> la verifica del contenuto di un pacchetto di applicazione livello dati  
 Dopo aver decompresso il pacchetto, è possibile esaminare i file generati dalla finestra di dialogo per la **decompressione dell'applicazione livello dati** . Tramite questa finestra di dialogo è possibile compilare i file seguenti nella cartella di destinazione selezionata:  
  
1.  Uno script Transact-SQL contenente le istruzioni per la creazione degli oggetti definiti nell'applicazione livello dati. Il nome del file è *NomeDAC*.sql, dove *NomeDAC* indica il nome del pacchetto DAC.  
  
2.  Tutti i file XML del pacchetto.  
  
3.  Tutti i file della sezione Extra Files dell'applicazione livello dati, quali i file di pre-distribuzione o di post-distribuzione dell'applicazione livello dati.  
  
 Per altre informazioni, vedere [Validate a DAC Package](../../relational-databases/data-tier-applications/validate-a-dac-package.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Distribuire un'applicazione livello dati](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Aggiornare un'applicazione livello dati](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)  
  
  
