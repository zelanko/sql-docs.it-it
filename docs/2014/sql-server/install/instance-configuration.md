---
title: Configurazione istanza | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66329d4c25a23a6b3dbc3570723bab8aecfa3d4a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68190962"
---
# <a name="instance-configuration"></a>Configurazione istanza
  Utilizzare la pagina **Configurazione dell'istanza** dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per specificare se creare un'istanza predefinita oppure un'istanza denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è già installata, verrà creata un'istanza predefinita a meno che non si specifichi un'istanza denominata.  
  
 Ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è costituita da un set distinto di servizi con impostazioni specifiche per le regole di confronto e le altre opzioni. La struttura della directory, la struttura del Registro di sistema e i nomi dei servizi riflettono il nome dell'istanza e un ID di istanza specifico creato durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Un'istanza può essere l'istanza predefinita oppure un'istanza denominata. Il nome dell'istanza predefinita è MSSQLSERVER. Non è necessario che un client specifichi il nome dell'istanza per stabilire una connessione. Un'istanza denominata è determinata dall'utente durante l'installazione. È possibile installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come istanza denominata senza prima installare l'istanza predefinita. Indipendentemente dalla versione, l'istanza predefinita può essere costituita solo da un'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per volta.  
  
 **Avviso!** Con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep è possibile specificare il nome dell'istanza quando si completa un'istanza predisposta nella pagina **Configurazione dell'istanza**. È possibile scegliere di configurare l'istanza predisposta che si sta completando come istanza predefinita se non è presente alcuna istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul computer.  
  
## <a name="multiple-instances"></a>Più istanze  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un singolo server o processore, ma solo un'istanza può costituire l'istanza predefinita, mentre tutte le altre istanze devono essere istanze denominate. Un computer può eseguire più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] simultaneamente e ciascuna di esse viene eseguita in modo indipendente dalle altre.  
  
 Per ulteriori informazioni, vedere la pagina relativa alle [specifiche di capacità massima per SQL Server](../maximum-capacity-specifications-for-sql-server.md).  
  
## <a name="options"></a>Opzioni  
 Solo istanze del cluster di failover: specificare il nome di rete del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo nome identifica l'istanza del cluster di failover nella rete.  
  
 Istanza predefinita o denominata: nel determinare se installare un'istanza predefinita o denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tenere presenti le informazioni seguenti:  
  
-   Se si intende installare una singola istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un server di database, l'istanza deve essere predefinita.  
  
-   Utilizzare un'istanza denominata nei casi in cui si prevede di installare più istanze nello stesso computer. Un server può contenere una sola istanza predefinita.  
  
-   In qualsiasi applicazione che prevede l'installazione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , questo deve essere installato come istanza denominata. In questo modo è possibile ridurre al minimo i conflitti quando più applicazioni sono installate nello stesso computer.  
  
 **Istanza predefinita**  
 Selezionare questa opzione per installare un'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un computer può ospitare una sola istanza predefinita. Tutte le altre istanze devono essere denominate. Se, tuttavia, è installata un'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è possibile aggiungere un'istanza predefinita di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nello stesso computer.  
  
 **Istanza denominata**  
 Selezionare questa opzione per creare una nuova istanza denominata. Quando si assegna il nome a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tenere presenti le considerazioni seguenti:  
  
-   Per i nomi delle istanze non viene fatta distinzione tra maiuscole e minuscole.  
  
-   I nomi delle istanze non possono iniziare né terminare con un carattere di sottolineatura (_).  
  
-   I nomi delle istanze non possono contenere il termine "Default" o altre parole chiave riservate. Se nel nome di un'istanza viene utilizzata una parola chiave riservata, si verificherà un errore di installazione. Per altre informazioni, vedere [parole chiave riservate &#40;&#41;Transact-SQL ](/sql/t-sql/language-elements/reserved-keywords-transact-sql).  
  
-   Se si specifica MSSQLServer per il nome di istanza, verrà creata un'istanza predefinita.  
  
-   Un'installazione di [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] viene sempre eseguita come un'istanza denominata di "PowerPivot". Non è possibile specificare un nome di istanza diverso per questo ruolo caratteristica.  
  
-   I nomi delle istanze devono essere costituiti al massimo da 16 caratteri.  
  
-   Il primo carattere del nome dell'istanza deve essere una lettera. Le lettere consentite sono quelle definite dallo standard Unicode 2.0 e includono i caratteri latini a-z, A-Z e i caratteri corrispondenti a lettere di altre lingue.  
  
-   I caratteri successivi possono essere costituiti dalle lettere definite dallo standard Unicode 2.0, dai numeri decimali inclusi negli script Latino di base o in altri script nazionali, il simbolo del dollaro ($) o un carattere di sottolineatura (_).  
  
-   Nei nomi di istanza non sono consentiti spazi interni o altri caratteri speciali. La barra rovesciata (\\), la virgola (,) i due punti (:), il punto e virgola (;), la virgoletta singola ('), la e commerciale (&), il segno meno (-) e la chiocciola (@) rappresentano altri caratteri non consentiti.  
  
-   **Solo i caratteri validi nella tabella codici di Windows corrente possono essere utilizzati nei nomi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di istanza. Se viene utilizzato un carattere Unicode non supportato, si verificherà un errore di installazione.**  
  
 **Istanze e funzionalità rilevate**  
 È possibile visualizzare un elenco dei componenti e delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installati sul computer su cui viene eseguito il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **ID istanza** : per impostazione predefinita, il nome dell'istanza viene usato come ID istanza. Tale nome viene utilizzato per identificare le directory di installazione e le chiavi del Registro di sistema per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si tratta del caso delle istanze predefinite e delle istanze denominate. Per un'istanza predefinita, il nome di istanza e l'ID istanza sono MSSQLSERVER. Per utilizzare un ID istanza non predefinito, specificarlo nel campo **ID istanza** .  
  
> [!IMPORTANT]  
>  Con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep, l'ID istanza visualizzato in questa pagina è quello specificato durante il passaggio relativo alla preparazione dell'immagine del processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep. Non sarà possibile specificare un ID istanza diverso durante il passaggio relativo al completamento dell'immagine.  
  
> [!NOTE]  
>  Gli ID delle istanze che iniziano con un carattere di sottolineatura (_) o che contengono il simbolo del cancelletto (#) o del dollaro ($) non sono supportati.  
  
 Per ulteriori informazioni su directory, percorsi di file e nomi di ID istanza, vedere [percorsi dei file per le istanze predefinite e denominate di SQL Server](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md).  
  
 Tutti i componenti di un'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono gestiti come unità. Tutti i Service Pack e gli aggiornamenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno applicati a ogni componente di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Tutti i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che condividono lo stesso nome di istanza devono soddisfare i criteri seguenti:  
  
-   **Stessa versione**  
  
-   **Stessa edizione**  
  
-   **Impostazioni della stessa lingua**  
  
-   **Stesso stato cluster**  
  
    > [!NOTE]  
    >  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non riesce a interagire con i cluster.  
  
-   **Stesso sistema operativo**  
  
  
