---
title: Accetta condizioni di licenza | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- license terms
helpviewer_keywords:
- Registration Information page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Registration Information page
ms.assetid: 08dd739d-5817-4418-bcff-74ab7f8bbd33
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 6d41879b84d98f72e570b00a61341a53d2e6187a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85046447"
---
# <a name="accept-license-terms"></a>Accettazione delle condizioni di licenza
  Usare la pagina **Condizioni di Licenza** dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per accettare le condizioni di licenza per la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in uso.  
  
 È possibile stampare il contratto di licenza o copiarlo negli Appunti. Per continuare, accettare le condizioni di licenza, quindi scegliere **Avanti**. Per chiudere l'installazione, fare clic su **Annulla**.  
  
## <a name="customer-experience-improvement-program-ceip"></a>Customer Experience Improvement Program (CEIP)  
 Se si abilita la segnalazione CEIP, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene configurato per l'invio periodico di un report a [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Nei report verranno incluse informazioni sulla configurazione hardware in uso e sulle modalità di utilizzo dei componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . I dati relativi all'utilizzo delle caratteristiche verranno utilizzati da [!INCLUDE[msCoName](../../includes/msconame-md.md)] per migliorare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tra i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] monitorati da questa caratteristica sono inclusi quelli indicati di seguito:  
  
-   Il [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Replica  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Installazione  
  
 Le informazioni relative all'utilizzo delle caratteristiche vengono inviate a [!INCLUDE[msCoName](../../includes/msconame-md.md)]e archiviate con diritti di accesso limitati.  
  
 Per disabilitare la segnalazione analisi utilizzo software al termine dell'installazione, utilizzare lo strumento ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] segnalazione errori e utilizzo** funzionalità nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] menu **strumenti di configurazione** .  
  
 Per le azioni di installazione quali aggiornamento, ripristino, installazione e così via, le informazioni vengono raccolte e caricate solo durante l'esecuzione del programma di installazione  
  
 Per tutti gli altri componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , le informazioni vengono raccolte una volta al giorno per tutte le istanze abilitate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per impostazione predefinita, la raccolta viene eseguita a mezzanotte per ridurre il carico del server. Se si desidera cambiare l'ora di raccolta, è possibile modificare manualmente la chiave del Registro di sistema che la controlla. È disponibile una chiave del Registro di sistema specifica per ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
 \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<INSTANCEID> HKLM\Software \CPE\TimeofReporting  
  
 Il valore della chiave del Registro di sistema include l'ora di esecuzione della raccolta espressa in numero di minuti a partire da 00.00 (mezzanotte). Ad esempio, se il valore immesso è 60 la raccolta verrà eseguita alla 1.00, mentre se il valore immesso è 1200 la raccolta verrà eseguita alle 20.00 e così via.  
  
## <a name="error-reporting"></a>Segnalazione errori  
 Usare la pagina **Impostazioni segnalazione errori e utilizzo funzionalità** dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per abilitare la funzionalità di segnalazione degli errori e dell'utilizzo delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="options"></a>Opzioni  
 La segnalazione degli errori e la raccolta dei dati di utilizzo delle funzionalità sono disabilitate per impostazione predefinita in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e nei relativi in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Segnalazione errori  
 Se si abilita la funzionalità Segnalazione errori, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene configurato per l'invio automatico di un report a [!INCLUDE[msCoName](../../includes/msconame-md.md)] in caso si verifichi un errore irreversibile in uno dei componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seguenti:  
  
-   Il [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Replica  
  
 Le segnalazioni degli errori sono considerate riservate e vengono utilizzate da [!INCLUDE[msCoName](../../includes/msconame-md.md)] per migliorare le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Le informazioni relative agli errori vengono inviate mediante una connessione protetta (https) a [!INCLUDE[msCoName](../../includes/msconame-md.md)]e archiviate con diritti di accesso limitati. In alternativa, le segnalazioni possono essere inviate al server interno per la segnalazione degli errori (Corporate Error Reporting).  
  
 Nelle segnalazioni degli errori sono incluse le informazioni seguenti:  
  
-   La condizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel momento in cui si è verificato il problema.  
  
-   La versione del sistema operativo e le informazioni sull'hardware del computer.  
  
-   L'ID digitale del prodotto che non viene utilizzato per l'identificazione della licenza.  
  
-   L'indirizzo IP di rete del computer o del server proxy.  
  
-   Le informazioni ricavate dalla memoria o dai file del processo che ha generato l'errore.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] non raccoglie intenzionalmente file, nomi, indirizzi, indirizzi di posta elettronica o qualsiasi altra forma di informazioni personali. È tuttavia possibile che la segnalazione degli errori contenga informazioni personali ricavate dalla memoria o dai file del processo che ha generato l'errore. Le informazioni raccolte possono contenere dati personali. Tuttavia, tali informazioni non saranno utilizzate da [!INCLUDE[msCoName](../../includes/msconame-md.md)] in alcun modo per identificare l'utente.  
  
 Per altre informazioni sui criteri di raccolta dei dati e l'informativa sulla privacy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Informativa sulla privacy di Microsoft SQL Server](../../../2014/getting-started/microsoft-sql-server-privacy-statement.md).  
  
 Se dopo avere abilitato la funzionalità Segnalazione errori si verifica un errore irreversibile, è possibile che venga visualizzata una risposta da [!INCLUDE[msCoName](../../includes/msconame-md.md)] nel registro eventi di Windows con un collegamento a un articolo della [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base relativo all'errore specifico.  
  
 Per disabilitare le funzionalità di segnalazione degli errori e dell'utilizzo delle funzionalità per tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e per i relativi componenti dopo l'installazione, aprire la finestra di dialogo **Impostazioni segnalazione errori e utilizzo funzionalità** e deselezionare le caselle di controllo relative a **Utilizzo funzionalità**. Se la **segnalazione errori** è abilitata per più componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (i [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] componenti condivisi,, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e), è possibile disabilitare la segnalazione errori per ogni istanza di un singolo componente, nonché per i componenti condivisi, elencati come **altri**.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulle condizioni di licenza di SQL Server](../../../2014/getting-started/about-the-sql-server-license-terms.md)  
  
  
