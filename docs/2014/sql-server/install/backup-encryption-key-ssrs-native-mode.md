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
manager: craigg
ms.openlocfilehash: a0b2c2e597ef7069bcc51fb885a2e810871bfbb5
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952655"
---
# <a name="backup-encryption-key-ssrs-native-mode"></a>Backup della chiave di crittografia (modalità nativa SSRS)
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene utilizzata una chiave di crittografia per proteggere dati sensibili archiviati nel database del server di report. Disporre di un backup di questa chiave è essenziale per assicurare accesso continuo a stringhe di connessione e credenziali crittografate. È necessario disporre di una copia di backup di questa chiave se si sposta il database del server di report in un altro computer o si modifica il nome utente o la password dell'account del servizio del server di report. Per entrambe le operazioni è necessario ripristinare la chiave da una copia di backup creata in precedenza.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Per aprire la finestra di dialogo Backup della chiave di crittografia fare clic su **Chiavi di crittografia** nel riquadro di navigazione di Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , quindi fare clic su **Backup**. Questa finestra di dialogo viene visualizzata anche quando si aggiorna l'account del servizio utilizzando la pagina Account servizio di Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per ulteriori informazioni sul Configuration Manager [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Reporting Services Configuration Manager &#40;modalità&#41;nativa](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opzioni  
 **Percorso del file**  
 Consente di specificare un nome e un percorso per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nella chiave simmetrica. La chiave simmetrica non viene mai archiviata in testo non crittografato. Per la protezione del file, è necessario digitare una password.  
  
 **Password**  
 Consente di digitare una password per proteggere il file dall'accesso non autorizzato. Solo gli utenti che conoscono la password saranno in grado di ripristinare la chiave bloccata nel file. In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] vengono applicati criteri password complessi. La password deve contenere almeno 8 caratteri e includere una combinazione di caratteri alfanumerici maiuscoli e minuscoli e almeno un simbolo.  
  
 **Conferma password**  
 Consente di digitare nuovamente la password immessa.  
  
## <a name="see-also"></a>Vedere anche  
 [Reporting Services Configuration Manager argomenti &#40;della Guida F1 @no__t modalità&#41;nativa SSRS](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)-3  
 [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Eliminare e ricreare chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Inizializzare un server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Archiviare i dati crittografati del server di report &#40;Gestione configurazione SSRS &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Chiavi &#40;di crittografia modalità nativa SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
