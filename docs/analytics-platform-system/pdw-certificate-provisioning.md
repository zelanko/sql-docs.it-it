---
title: Provisioning del certificato PDW - sistema di piattaforma Analitica | Microsoft Docs
description: La pagina di Provisioning del certificato PDW di Analitica piattaforma di sistema di Configuration Manager Importa o rimuove il certificato usato dall'area PDW.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4876b890067bd851167bc1e3e3c355c9701569d5
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52405096"
---
# <a name="pdw-certificate-provisioning---analytics-platform-system"></a>Provisioning del certificato PDW - sistema di piattaforma Analitica
Il **Provisioning del certificato PDW** pagina del sistema di piattaforma Analitica **Configuration Manager** Importa o rimuove il certificato usato dall'area PDW. L'uso, un certificato per crittografare le connessioni consente una comunicazione protetta il nodo di controllo tramite client di SQL Server, gli strumenti che utilizzano i driver di SQL Server PDW, il [Console di amministrazione](monitor-the-appliance-by-using-the-admin-console.md), e carica di Integration Services.  
  
## <a name="prerequisites"></a>Prerequisiti  
Prima di installare il certificato, eseguire le operazioni seguenti:  
  
1.  Ottenere un certificato protetto. Per altre informazioni su come ottenere un certificato protetto, contattare il supporto tecnico Microsoft.  
  
2.  Salvare il certificato al nodo di controllo in un file PFX protetto da password.  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>Per motivi di sicurezza, ottenere un certificato attendibile  
SQL Server PDW supporta l'utilizzo di un certificato per crittografare le connessioni al nodo di controllo; incluse le connessioni per il **Console di amministrazione**.  
  
Per impostazione predefinita, il **Console di amministrazione** include un certificato autofirmato che fornisce privacy, ma non l'autenticazione del server. Questo può rendere vulnerabile ad attacchi man-in-the-middle le comunicazioni. Quando un utente si connette alla Console di amministrazione tramite il certificato autofirmato, Internet Explorer restituisce l'errore: "Si è verificato un problema con il certificato di sicurezza di questo sito Web".  
  
Anche se la connessione tramite il certificato autofirmato crittografa i dati in transito tra il client e server, la connessione è ancora soggetta a rischi da utenti malintenzionati.  
  
> [!WARNING]  
> Gli amministratori di Appliance devono acquisire immediatamente un certificato concatenato a un'autorità di certificazione attendibile riconosciuta dal client, allo scopo di avere una connessione sicura e rimuovere l'errore che segnala di Internet Explorer.  
  
Il percorso di certificazione deve contenere il nome di dominio completo che viene eseguito il mapping al nodo di controllo indirizzo IP del Cluster (scelta consigliata) o il nome che gli utenti digitano nella loro barre di indirizzi del browser per accedere al **Console di amministrazione**.  
  
Utilizzare il sistema di piattaforma Analitica**Configuration Manager** per aggiungere o rimuovere il certificato attendibile. Direttamente usando lo strumento di configurazione certificato di servizi di Microsoft Windows HTTP (**winHttpCertCfg.exe**) per gestire il certificato non è supportata.  
  
## <a name="import-or-remove-the-certificate"></a>Importare o rimuovere il certificato  
Le istruzioni seguenti illustrano come importare o rimuovere il certificato del dispositivo.  
  
### <a name="to-import-the-certificate"></a>Per importare il certificato  
  
1.  Avviare il **Configuration Manager**. Per altre informazioni, vedere [avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md).  
  
2.  Nel riquadro sinistro della finestra di **Configuration Manager**, espandere **Parallel Data Warehouse topologia**, quindi fare clic su **certificati**.  
  
3.  Selezionare **importare un certificato e configurare l'appliance per usarlo**, quindi fare clic su **Sfoglia** per individuare e selezionare il file del certificato.  
  
4.  Immettere la password per il certificato nella **Password** campo.  
  
5.  Fare clic su **applica** per configurare il certificato per l'appliance.  
  
SQL Server PDW non crittograferà connessione corrente usando il certificato importato, ma userà il certificato per le nuove connessioni.  
  
### <a name="to-remove-the-previously-imported-certificate"></a>Per rimuovere il certificato precedentemente importato  
  
1.  Avviare il **Configuration Manager**. Per altre informazioni, vedere [avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md).  
  
2.  Nel riquadro sinistro della finestra di **Configuration Manager**, espandere **Parallel Data Warehouse topologia**, quindi fare clic su **certificati**.  
  
3.  Selezionare **rimuovere qualsiasi certificato di provisioning nell'appliance**.  
  
4.  Fare clic su **applica** per rimuovere il certificato precedentemente importato dall'appliance.  
  
SQL Server PDW continueranno a crittografare le connessioni correnti, ma non utilizzerà la rimozione del certificato per le nuove connessioni.  
  
![Certificato PDW strumento DWConfig](./media/pdw-certificate-provisioning/SQL_Server_PDW_DWConfig_ApplPDWCert.png "SQL_Server_PDW_DWConfig_ApplPDWCert")  
  
## <a name="see-also"></a>Vedere anche  
[Avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md)  
<!-- MISSING LINKS [HDInsight Certificate Provisioning &#40;Analytics Platform System&#41;](hdinsight-certificate-provisioning.md)  -->  
  
