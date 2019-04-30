---
title: Modalità alternative di acquisizione di una connessione dati (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: aebc5f3d-97d5-4d54-b525-753fed073a9a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e98be6ed17cebe6c06033b7230fbbdcdde18dd66
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233527"
---
# <a name="alternative-ways-to-get-a-data-connection-report-builder"></a>Modalità alternative di acquisizione di una connessione dati (Generatore report)
  Una connessione dati contiene le informazioni necessarie per connettersi a un'origine dati esterna, ad esempio un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . In genere, le informazioni di connessione e il tipo di credenziali da utilizzare vengono fornite dal proprietario dell'origine dati.  
  
 Per specificare una connessione dati, è possibile utilizzare un'origine dati condivisa dal server di report o creare un'origine dati incorporata che venga utilizzata solo in un report specifico.  
  
 Nella maggior parte delle esercitazioni vengono utilizzate origini dati incorporate. Se tuttavia si dispone dell'accesso a origini dati condivise, sarà invece possibile utilizzarle.  
  
## <a name="getting-a-data-connection-from-a-shared-data-source"></a>Recupero di una connessione dati da un'origine dati condivisa  
 Se nel server di report è disponibile un'origine dati condivisa e si dispone delle autorizzazioni necessarie per utilizzarla, sarà possibile utilizzare tale origine dati anziché un'origine dati incorporata. Nelle procedure riportate di seguito viene illustrato come individuare le origini dati condivise e fornire tutte le credenziali necessarie per l'utilizzo.  
  
 Per utilizzare un'origine dati condivisa, è necessario selezionare un server di report e un'origine dati. L'URL del server di report può essere in genere recuperato dall'amministratore del server di report.  
  
#### <a name="to-specify-a-data-connection-from-a-list-of-shared-data-sources"></a>Per specificare una connessione dati da un elenco di origini dati condivise  
  
1.  Nella pagina **Scegliere un set di dati** selezionare **Crea un set di dati**, quindi fare clic su **Avanti**. Verrà visualizzata la pagina **Scegliere una connessione a un'origine dei dati** .  
  
2.  Nell'elenco delle origini dati selezionare un'origine dati per la quale si dispone delle autorizzazioni di accesso.  
  
3.  Per verificare che la connessione all'origine dati avvenga correttamente, fare clic su **Test connessione**. Verrà visualizzato il messaggio "Creazione connessione completata". [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  Scegliere **Avanti**.  
  
     Se necessario, immettere le credenziali. Per salvare in locale le credenziali, selezionare **Salva password con la connessione**. Se non si seleziona questa opzione, le credenziali verranno richieste ogni volta che si esegue il report.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-specify-a-data-connection-by-browsing-to-a-shared-data-source-on-a-report-server"></a>Per specificare una connessione dati selezionando il percorso a un'origine dati condivisa nel server di report  
  
1.  Nella pagina **Scegliere un set di dati** selezionare **Crea un set di dati**, quindi fare clic su **Avanti**. Verrà visualizzata la pagina **Scegliere una connessione a un'origine dei dati** .  
  
2.  Fare clic su **Sfoglia**. Verrà visualizzata la finestra di dialogo **Seleziona origine dati** .  
  
3.  Nell'elenco a discesa **Cerca in** selezionare **Siti e server recenti**. Nel riquadro dell'origine dati fare clic sull'URL del server, quindi fare clic su **Apri**.  
  
     Verrà visualizzato l'elenco delle origini dati o dei modelli.  
  
4.  In alternativa, in **Nome**digitare l'URL del server di report. Fare clic su **Apri**.  
  
     Verrà stabilita la connessione al server di report e verranno caricate le origini dati disponibili in corrispondenza della cartella radice.  
  
5.  Passare a una cartella che contiene un'origine dati per la quale sono disponibili sufficienti autorizzazioni di connessione, selezionare l'origine dati, quindi fare clic su **Apri**.  
  
     Verrà visualizzata di nuovo la pagina **Scegliere una connessione a un'origine dei dati** .  
  
6.  Per verificare che la connessione all'origine dati avvenga correttamente, fare clic su **Test connessione**.  
  
     Verrà visualizzato il messaggio "Creazione connessione completata". [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Scegliere **Avanti**.  
  
8.  Se viene richiesto un nome utente e una password, immettere le credenziali. Per salvare in locale le credenziali, selezionare **Salva password con la connessione**.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Esercitazioni su &#40;Generatore Report&#41;](report-builder-tutorials.md)  
  
  
