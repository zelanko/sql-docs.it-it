---
title: Backup della chiave di crittografia (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.backupencryptionkey.F1
ms.assetid: eb8c82be-323b-4d86-ab10-c1bf69a4abe3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c8524cdc2c4efb03e2a285c815ca58391045062f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045509"
---
# <a name="backup-encryption-key-ssrs-native-mode"></a>Backup della chiave di crittografia (modalità nativa SSRS)
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene utilizzata una chiave di crittografia per proteggere dati sensibili archiviati nel database del server di report. Disporre di un backup di questa chiave è essenziale per assicurare accesso continuo a stringhe di connessione e credenziali crittografate. È necessario disporre di una copia di backup di questa chiave se si sposta il database del server di report in un altro computer o si modifica il nome utente o la password dell'account del servizio del server di report. Per entrambe le operazioni è necessario ripristinare la chiave da una copia di backup creata in precedenza.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità nativa.  
  
 Per aprire la finestra di dialogo Backup della chiave di crittografia fare clic su **Chiavi di crittografia** nel riquadro di navigazione di Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , quindi fare clic su **Backup**. Questa finestra di dialogo viene visualizzata anche quando si aggiorna l'account del servizio utilizzando la pagina Account servizio di Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per ulteriori informazioni sulla [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, vedere [Reporting Services Configuration Manager &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opzioni  
 **Percorso file**  
 Consente di specificare un nome e un percorso per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nella chiave simmetrica. La chiave simmetrica non viene mai archiviata in testo non crittografato. Per la protezione del file, è necessario digitare una password.  
  
 **Password**  
 Consente di digitare una password per proteggere il file dall'accesso non autorizzato. Solo gli utenti che conoscono la password saranno in grado di ripristinare la chiave bloccata nel file. In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] vengono applicati criteri password complessi. La password deve contenere almeno 8 caratteri e includere una combinazione di caratteri alfanumerici maiuscoli e minuscoli e almeno un simbolo.  
  
 **Conferma password**  
 Consente di digitare nuovamente la password immessa.  
  
## <a name="see-also"></a>Vedere anche  
 [Reporting Services Configuration Manager argomenti della Guida F1 &#40;modalità nativa di SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Eseguire il backup e il ripristino delle chiavi di crittografia Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Eliminare e ricreare le chiavi di crittografia &#40;Configuration Manager SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Inizializzare un server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Archiviare i dati crittografati del server di report &#40;Gestione configurazione SSRS &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Chiavi di crittografia &#40;modalità nativa SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
